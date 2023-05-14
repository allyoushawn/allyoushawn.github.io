---
title: ML Model Service
parent: ML Service
layout: default
nav_order: 40
---
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>
---

# ML Model Service
In this document we introduce how the model service works.
The model service here we refer to a service that feed the query into a ML model and return the model's prediction.
This is the [Github Repo](https://github.com/allyoushawn/ml_model_service) that we build for ML model service.

# Microservice repo architecture
In the repo, we treat different ML model services as microservices and put them into one repo.
`base_microservice` would be used to define the shared functionality between microservices.
In `deployment`, we have different ML model's Docker files used for model deployment.

The query and response for the ML model service is defined in each service's own
[payloads](https://github.com/allyoushawn/ml_model_service/blob/main/sentiment_analysis_model_service/sentiment_analysis_model_service/api/payloads.py) 
and [responses](https://github.com/allyoushawn/ml_model_service/blob/main/sentiment_analysis_model_service/sentiment_analysis_model_service/api/responses.py).
The service endpoint could be defined in its 
[endpoints file](https://github.com/allyoushawn/ml_model_service/blob/main/sentiment_analysis_model_service/sentiment_analysis_model_service/api/endpoints/sentiment_service.py).
and [service_start.sh](https://github.com/allyoushawn/ml_model_service/blob/main/sentiment_analysis_model_service/service_start.sh#L12).

Finally, how the model works is defined in the
[model file](https://github.com/allyoushawn/ml_model_service/blob/main/sentiment_analysis_model_service/sentiment_analysis_model_service/model/sentiment_model.py).



# A standalone NLP service: Sentiment Analysis
Refer to the repo README for more information.  [Link](https://github.com/allyoushawn/ml_model_service/tree/main/sentiment_analysis_model_service)

The sentiment analysis service is a dictionary-based approach. 
It uses the package `Afinn`[[Repo]](https://github.com/fnielsen/afinn) for sentiment analysis. It does not involved with
any training and therefore is suitable for a POC here.

Following the following code to run the service:
```
cd /path/to/ml_model_service
docker build -t sentiment_analysis_model_service:prod --target prod -f deployment/sentiment_analysis_model_service/Dockerfile .
docker run --name sentiment_analysis_model_service_local -it -p 4460:4460 sentiment_analysis_model_service:prod
```

To stop and remove the container:
```
docker container stop sentiment_analysis_model_service_local && docker container rm sentiment_analysis_model_service_local
```


# A GPU-enabled service: Machine Translation

Refer to the repo README for more information. [Link](https://github.com/allyoushawn/ml_model_service/tree/main/mt_model_service)

If we want to train a deep learning model, we are very likely to use GPU for training and potentially for inference.
We also play with the GPU for building the ML model service. In this example, we trained a transformer-based 
machine translation model and use a GPU-enabled container to run it. The config and how the model is trained could be
found in the repo [transformer_mt](https://github.com/allyoushawn/transformer_mt). We use the repo to train 
an English-Mandarin translation model. 

Following the following code to run the service:
```
cd /path/to/ml_model_service
docker build -t mt_model_service:prod --target prod -f deployment/mt_model_service/Dockerfile .
docker run --name mt_model_service_local -it -p 4461:4461 mt_model_service:prod
```

To stop and remove the container:
```
docker container stop mt_model_service_local && docker container rm mt_model_service_local
```

### Run the service with GPU
1. Make sure the `MODEL_PATH` in paths.py is pointing to a GPU-trained model. You might need to make sure MANIFEST.in also specify the GPU-based model.
2. Change the corresponding docker cmds to the following and the service would use GPU.
```
docker build -t mt_model_service_gpu:prod --target prod -f deployment/mt_model_service/Dockerfile.gpu .
docker run --name mt_model_service_gpu_local --gpus all -it -p 4461:4461 mt_model_service_gpu:prod
docker container stop mt_model_service_gpu_local && docker container rm mt_model_service_gpu_local
```

# Next
The following article would introduce how these model services are called by a gateway service which would be queried by
users.