# Self-driving RC car

# Zheng Wang turns the tables on Google with his very fully-sustaining driving car

Where did the idea to develop a self-driving car come from? 
Believe it not, I actually did do this for a school project. All of my interests was machine learning. I decided to develop something that heavily involves machine learning and coding. I researched online and found a very inspiring Raspberry Pi project by David Singleton, which showed that it was possible to use an Arduino and a few other items. I was amazed to see that the RC car could drive itself without aid and I wondered if I could replicate a similar project.

Images received on the computer to be converted into grayscale and fed into a neural network to make predictions for the car, so as to turn left or right at the correct moment. These same images are used to control the car and the stop signs, while the Raspberry Pi alerts the system of distance to an obstacle. This is how my project is primarily learning.

help with measuring distance with the ultrasonic sensor, there were some handy tutorials on the web for enthusiasts and there's other material all over the place.

Can you tell me about the ultrasonic sensor? Can it detect 360 degrees?

I used my Raspberry Pi and made up mind try to build my own self-driving car that could do even more. I also wanted to add features like avoidance, stop and traffic light detection. It took me to develop the project longer than I had imagined, just because there are so many factors that needed to be considered.

For this project, I chose to use the HC-SR04 ultrasonic sensor, which is effective and has friendly pieces of kit on the market. It can be a bit tricky to set up from scratch, but I was able to solve the problem that I had. When I had a problem, I searched the internet and found a useful list that says detection is within 30 degrees, which would seem right about the right direction. There are numerous sensors on the market, so a complete 360-degree detection system would be possible if needed.

![](bbox=[0.823, 0.422, 0.931, 0.56])

The final part of the system consists of using a neural network that is sent to the Raspberry Pi which is connected to the RC controller. The Arduino then sends high or low signals to drive the car. This was quite a taking place, after an initial period of trial and error, it took an long period of time to get it right before it started running independently.

# Could you give us an overview of how the self-driving system works?

# How do you see the future of this project? Where is it going?

The core of the system consists of using the Raspberry Pi and Arduino to work seamlessly in sync. Each system consists of input for controlling the car and ultrasonic sensor to drive the main RC car.

What is the role of the Raspberry Pi in the scheme of your self-driving car

There are lot of areas that I would like to explore further to make the project even better. For example, I'd like to use more of the ultrasonic sensor and integrate more components. There are many challenges that I need to overcome, and they are far more than I expected when I first started.

First, live video and ultrasonic data are sent from the Raspberry Pi to the computer via a Wi-Fi connection. I was quick to recognize that it was possible to record the streaming, in order to achieve these goals, the video resolution is limited to (320x240). It proves that enough streaming was enough. The next step is for the colour

I connected a Pi module to an ultrasonic sensor

There are also clear programs running on the Raspberry Pi that help with the streaming of data and the other is for the data from the ultrasonic sensor. When I needed

all in there here. When I needed

help with measuring distance with the ultrasonic sensor,

there were some

Zheng Wang
software engineering background
working on his Raspberry Pi project

Like IT?
Zheng Wang started the entire process from scratch. For those who wanted to learn more about it, here is the object detection technique.

David Singleton
He took inspiration from David Singleton and I recommend you check out his blog on how to build a Raspberry Pi RC car. The process is a bit long but it is an interesting reading.

www.linuxuser.com | 69