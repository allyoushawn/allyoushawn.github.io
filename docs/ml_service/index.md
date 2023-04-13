---
title: ML Service
has_children: true
layout: default
nav_order: 5
---
:raised_hands: Woo hoo! I made it! :raised_hands:

Although the spent time for this project alone is around half a year, some components are built more than three years ago.
It's basically a project combining my academia ML modeling knowledge with the backend and ML Ops skills I acquired 
from the industry as a ML Engineer. It's an awesome journey so far. :satisfied:

This project started with an idea during my shower (and yes, I would proudly admit 80% of my ideas came out
while I was taking a shower instead of working or studying...)

It started with building a ML model service with REST API. After finishing it on my Linux environment, I found there were issues
when I tried to deploy it on my Mac laptop, and therefore I turn to use Docker to make my life easier.

Since we were using Docker anyway, why not try GPU-enabled image and the side project `Machine Translation with Transformer` came in
handy.

Now I got two ML model services, it's time play with the microservice architecture.

It's cool to make it public and have family and friends test it. I started to wonder the qps that my desktop could handle.
I found JMeter could be a great tool for me.

Lastly, everything looks good on the backend side. However, when I tried to have my wife test it through the terminal,
she frowned at the black screen with some white text jumping around. All right, I got it, let's build a
more user-friendly interface. I built a crappy frontend interface allowing users could interact with the service through browsers.

I still have a lot of items I want to try. The best part as an ML Engineer is that we would need to take care of both backend and
modeling stuff. I would love to see how I could build a recommendation service with some streaming processing techniques
and things like feature store. Anyway, let's not stop here. Any comments or feedback are welcome! However, since it's a 
learning-based project, the reason why a weird component is there would probably be I just want to learn how to use it. :stuck_out_tongue:

Keep the ball rolling! 

