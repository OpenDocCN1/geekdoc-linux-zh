# EC2 Monitoring, Auto Scaling, and Elastic Load Balancing

In this chapter, you will learn how to use three powerful Amazon EC2 features: monitoring, auto scaling, and elastic load balancing. You'll see how these features can be used separately or together to build scalable and powerful web applications. Along the way you'll also learn how to leverage the CloudFusion library to make use of these features. We'll then take a short detour to learn how to use the Apache JMeter application to generate a predictable test load. Finally, we'll wrap up the chapter by learning how to load test an actual application to make sure that it scales as desired.

# Introduction

The monitoring, auto scaling, and elastic load balancing features of the Amazon EC2 services give you easy on-demand access to capabilities that once required a complicated system architecture and a large hardware investment.

Any real-world web application must have the ability to scale. This can take the form of **vertical scaling**, where larger and higher capacity servers are rolled in to