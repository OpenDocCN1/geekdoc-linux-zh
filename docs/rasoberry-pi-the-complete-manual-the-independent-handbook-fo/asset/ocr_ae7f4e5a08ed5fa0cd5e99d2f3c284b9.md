# # Raspberry Pi plus Arduinos

Find out just how to get your Raspberry Pi to talk to and use your Arduino

The Raspberry Pi is a truly amazing single-board computer that gets used in lots of DIY projects. That has been the basis for this whole column and the previous several articles. While the Raspberry Pi has a GPIO and can communicate with sensors and actuators, you may have cases where you want to use your Raspberry Pi as the brains of your project and offload the interactions with the physical world to another system.

This is usually handled by one of the many microcontroller boards that are available. In this issue, we will specifically use the Arduino board and see how to connect it to a Raspberry Pi and how to handle the communications between the two. As always, we will be using Python as the language of choice to handle all of the actual coding in the examples here.

The Arduino is an open source prototyping platform defined as a specification. This means that you can get Arduino implementations from several different manufacturers, but they should all behave in a similar fashion. For this article, the assumption will be that whatever implementation you wish to use will behave properly. The first step is to connect the two boards together.

You will probably want to use a powered USB hub to connect them since the Raspberry Pi can't provide huge amounts of power through its USB port. While they are connected over USB, the Arduino will appear as a serial port to the Raspberry Pi.

This means that you can communicate with the Arduino directly over the serial connection. To be completely sure you have all of the relevant libraries installed, you can simply install the Arduino IDE with the command:

```
```
$ sudo apt-get install arduino
```
```

This will make sure that you are starting with all of the core software that you might need. When you plug in your Arduino, you need to know over which port communications will happen. The specific port name will vary based on the exact version of Raspberry Pi and Arduino that you are using. However, it should be something like `/dev/ttyUSB0` or `/dev/ttyACM0`. In the example code below, we will be assuming that the Arduino is visible on the port `/dev/ttyUSB0`.

Once you have the two devices connected, you can start writing code to have them talk to each other.

> “For this article, the assumption will be that whatever implementation you wish to use will behave properly”