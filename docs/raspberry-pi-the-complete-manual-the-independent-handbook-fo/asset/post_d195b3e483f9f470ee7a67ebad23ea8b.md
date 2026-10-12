
## Projects

### Control an LED using GPIO

An introduction into using an external output, such as an LED, on the Pi.

#### What you'll need...

- **Breadboard:** www.pctotools.co.uk/half-size-breadboard
- **3mm LED light:** www.ultraleds.co.uk/led-product catalogue/basic-leds-3-5-4-10mm.html
- **Wires:** www.pccompare.com/product/breadboard-wires
- **270-ohm resistor:** http://goo.gl/wxFwP[dg]P091

![](img/f11b7dbb71886af07ef87126037ebe98_57_0.png)

*图 1: 你需要连接的所有东西——注意：连线应有公头和母头。*

![](img/f11b7dbb71886af07ef87126037ebe98_57_1.png)

*图 2: 将母头接到树莓派上，在 0 号引脚上连接一个 1000 欧姆电阻。蓝色线接地。*

![](img/f11b7dbb71886af07ef87126037ebe98_57_2.png)

*图 3: 一切连接完成后，将 USB 电源线插入树莓派*

![](img/f11b7dbb71886af07ef87126037ebe98_57_3.png)

*图 4: 打开电源。LED 灯会亮起。如果光线微弱，请使用一个更低电阻的电阻。*

After you have fired up your Pi, maybe installed XBMC and had a play around with streaming, you might be ready for your next challenge. One route to go down is to find interesting uses for one of the many desktop OSs available for the little computer, perhaps using it as a web server, an NAS or retro arcade console. This is all great fun, but an often-overlooked feature of the Pi is its hardware pins. If you've never done any electronics before, then the Pi is a great place to start. Or maybe you have used a programmable microcontroller such as Arduino in the past; the Pi, with its increased CPU and RAM over the Arduino, opens up many more possibilities for fun projects.

The Raspberry Pi features a single PWM (pulse width modulation) output pin, along with a series of GPIO (General Purpose Input/ Output) pins. These enable electronic hardware such as buzzers, lights and switches to be controlled via the Pi. For people who are used to either just 'using' a computer, or only programming software that only acts on the machine itself, controlling a real physical item such as a light can be a revelation.

This tutorial will assume no prior knowledge of electronics or programming, and will take you through the steps needed to control an LED using the Raspberry Pi, from setting it up to coding a simple application.

![](img/f11b7dbb71886af07ef87126037ebe98_57_4.png)

> We'll take you through the steps needed to control an LED using the Pi, from setting it up to coding

#### Component Overview

- **Breadboard**
  The breadboard, or prototyping board, provides an easy-to-use and reconfigurable environment for creating and changing your development circuits.

- **Breadboard wire**
  A must for any building electrical engineer, these male-to-male-and male-to-female wires make for fast and easy circuit building.

- **GPIO header**
  This provides a mechanism for both gathering input and providing output to electrical circuits, enabling reactive program design.

![](img/f11b7dbb71886af07ef87126037ebe98_58_0.png)

- **Coloured LED**
  Different coloured LEDs are a great way to physically see which part of the software is running and help you understand the program flow.

### The Pi's pins

01 Before we dive into writing code, let's take a look at the layout of the pins on the Pi. If you have your Pi in a case, take it out and place it in front of you with the USB ports on the right. Over the next few steps we'll look at some of the uses you'll encounter when using the GPIO port.

**Pi revision 1 or 2?**

02 Depending on when you purchased your Pi, you may have a revision 1 or revision 2 model. The GPIO layout is slightly different for each, although they do have the same functionality. Here we have a revision 1; revision 2s became available towards the end of 2012.

### Pin numbers

03 If you take a look at the top left of the board you will see a small white label, P1. This is pin 1 and above it is pin 2. To the right of pin 1 is pin 3, and above 3 is 4. This pattern continues until you get to pin 26 at the end. As you'll see in the next step, some pins have important uses.

**Pin uses**

04 Pin 1 is 3V3, or 3.3 volts. This is the main pin you will be using in this guide to provide power to our LED. Pins 2 and 4 are 5V. Pin 6 is the other pin we will use here, which is ground. Other ground pins are 9, 14, 20 and 25. You should always ensure your project is properly grounded.

### GPIO pins

05 The other pins on the board are GPIO (General Purpose Input/Output). These are used for other tasks that you need to do as your projects become more complex and challenging. Be aware that the USB power supply doesn't offer much scope for powering larger items.

**Basic LED lighting**

06 Okay, so let's get down to business and start making something. Firstly, get your breadboard, two wires, a 220Ω resistor and an LED. Note the slightly bent leg on one side of the LED, this is important for later on. Make sure your Pi is unplugged from the mains supply.

### Wiring the board

07 Plug one wire into the number 1, pin, and the other end into the breadboard. Note that it doesn't matter where on the breadboard you plug it in, but make sure there are enough empty slots around it to add the LED and resistor to. Now get another wire ready.

### Add another wire

08 Place the female end of the wire into pin number 6 (ground) and the other end into the breadboard, making sure to leave room for the resistor, depending on how large it is. Next, get your resistor ready. You can use a little higher or lower than 220 ohms, but not using a resistor at all will likely blow the LED.

### Add the resistor

09 Next we need to add our resistor. Place one end next to the ground wire on the breadboard, and the other one slot below the 3V3 wire connection. This will sit next to the LED when we add it in a second. Note that there is no correct or incorrect way to add a resistor.

### Add the LED

10 Grab your LED and place the 'bent' leg end next to the 3V3 wire in the breadboard. Place the other leg next to the resistor leg opposite the ground wire. This now completes the circuit and we are ready to test out our little task.

### Power it up

11 Now get your micro-USB cable and either plug the mains end into the wall, or plug it into a computer or laptop port (and powered on). You should see the LED light up. If not, then check your connections on the breadboard or try a different LED.

### Set up programming environment

12 Now, we need to be able to do a little bit more than just turn a light on – we want to be able to control it via code. Set up a new Raspbian installation (a guide to this is found on page 28). You don’t need a GUI for this – it can all be done via the terminal if you so wish. Before starting, it’s best to check everything is up to date with:

```bash
sudo apt-get dist-upgrade
```

### Open up terminal

13 Assuming we want to use the GUI, rather than SSH into the Pi, open up a new terminal window, by double-clicking on the LXTerminal icon. We need root access to control the LEDs, so either enter `su` now, or remember to prefix any commands with `sudo`.

```bash
su
# 或者在前缀中添加 sudo，然后输入密码
sudo
```

### Download GPIO library

14 There is a handy GPIO Python library that makes manipulating the GPIO pins a breeze. From within your terminal window, use `wget` to download the tarball file, then extract it using `tar`. This will give us all the files in a new directory.

```bash
wget https://pypi.python.org/packages/source/R/RPi.GPIO/RPi.GPIO-0.5.2.tar.gz
tar zxf RPi.GPIO-0.5.2.tar.gz
cd RPi.GPIO-0.5.2
```

### Install the library

15 Now we need to install the library. This is simply a case of using Python’s install method, so we need the dev version of Python. Make sure you are in the directory of the library before running this command.

```bash
sudo apt-get install python-dev
sudo python setup.py install
```

### Import the library in a script

16 Create a new Python script. Next import the main GPIO library and we’ll put it in a try-except block. Save the file using Ctrl+X and choosing 'yes'.

```python
cd /
cd Desktop
sudo nano gpio.py
try:
    import RPi.GPIO as GPIO
except RuntimeError:
    print('Error importing GPIO lib')
```
