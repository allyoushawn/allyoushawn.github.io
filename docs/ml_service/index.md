---
title: ML Service
has_children: true
layout: default
nav_order: 5
---
:raised_hands: Woo hoo! I made it! :raised_hands:




I can't believe this documentation takes more time than the project itself lol

Although the time spent for this project alone is around half a year, some components were built more than three years ago.
It's basically a project combining my academia ML modeling knowledge with the backend and ML Ops skills I acquired
from the industry as a ML Engineer. It's been an awesome journey so far. :satisfied:

This project started with an idea during my shower (and yes, I would proudly admit 80% of my ideas came out
while I was taking a shower instead of working or studying...)

It started with building a ML model service with REST API. After finishing it on my Linux environment, I found there were issues
when I tried to deploy it on my Mac laptop, and therefore I turned to Docker to make my life easier.

Since we were using Docker anyway, why not try GPU-enabled image and the side project `Machine Translation with Transformer` came in
handy.

After I included the machine translation model in this project, I got two ML model services. It's time to play with the microservice architecture.
I built a repository including multiple ML models and the goal is making the deployment and maintenance as easy as possible with `Makefile`.

It's cool to make it public and have family and friends test it. I started to wonder about the qps that my desktop could handle.
I found JMeter could be a great tool for me.

Finally, everything looks good on the backend side. However, when I tried to have my wife test it through the terminal,
she frowned at the black screen with some white text jumping around. All right, I got it, let's build a
more user-friendly interface. I built a crappy frontend interface allowing users to interact with the service through browsers.

I still have a lot of items I want to try. The best part as an ML Engineer is that we would need to take care of both backend and
modeling stuff. I would love to see how I could build a recommendation service with some streaming processing techniques
and things like Feature Store. Anyway, let's not stop here. Any comments or feedback are welcome! However, since it's a
learning-based project, the reason why a weird component is there would probably be I just want to learn how to use it. :stuck_out_tongue:

Keep the ball rolling!



