---
title: "DL Cloud GPU Server - JarvisLabs vs AWS EC2"
date: 2021-09-04T22:50:43+05:30
draft: false
---

As I started getting deeper into the Fast.ai course, I had to make a decision on what Cloud GPU service to use. In general, there are two possibilities as listed on https://course.fast.ai/.

 1. Notebook Server
 2. Full Linux Server
    
A notebook server is basically something that has a GPU but only exposes a notebook interface to you whereas a Full Linux server, will basically look like a remote machine in the cloud. But it will be a full fledged server. My preference is for a full linux server because of the flexibility.

There are many options that are listed for a full linux server on the fast.ai website. 
    1. Google Cloud
    2. AWS EC2
    3. Azure
    4. DataCrunch.io
    5. JarvisLabs.ai

I have decided to go with JarvisLabs.ai virtual server. I am trying to list down below the main advantages of it. This is as much for me as it is for anybody else, so I don't go down the rabbit hole of figuring out if I should explore another service.

## Cost
The table roughly lists the approximate cost assoicated with these.

| Name of the service | Minimum Cost                  |
|:--------------------|:------------------------------|
| Google Cloud        | $0.382/hr for T4 GPU/4 CPU    |
| AWS EC2             | $0.526/hr for T4 GPU/4 CPU    |
| Azure               | $0.40/hr for K80 GPU/6 CPU    |
| DataCrunch.io       | $0.52/hr for Tesla V100/6 CPU |
| JarvisLabs.ai       | $0.395/hr for RTX 5000/7 CPU  |

As is clear, JarvisLabs cost is very competitive especially for the HW provided. So from a cost perspective it is a no-brainer. But what about performance?

## Performance

In my very basic and unscientific benchmarking, it is 2x faster than the alternatives. Here is the screenshot that shows a Fast.ai run of sentiment analysis on it. You can see the speed difference very easily.

The image below shows how long the run took on an AWS EC2 server.

![AWS EC2 Sentiment Analysis Run](/posts/AWS_EC2.png)

And here are the statistics for the same run on JarvisLabs.ai

![JarvisLabs Sentiment Analysis Run](/posts/JarvisLabs.png)

JarvisLabs virtual server took 3'11" as against 07'32" for the AWS EC2 server. That is indeed 2x as fast.

## Hardware is better.

JarvisLabs has RTX5000 GPU, and AWS EC2 has T4 GPU. Both have 16 GB VRAM, so from a memory perspective (at least sizewise) they are the same. However RTX5000 has a much faster memory than T4. Also RTX 5000 runs much faster than T4. This is seen in the benchmark results too. 

## JarvisLabs is already setup for fast.ai

You don't have to configure the server for fast.ai. The server is already setup for fast.ai. So it has both the convenience of something like a notebook server, but also much faster to get started. The website is extremely simple and straightforward without you having to select a bazillion options so it is less confusing (at least for me.)


