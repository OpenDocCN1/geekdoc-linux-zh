
# Hack a toy with the Raspberry Pi : Part 1

> Learn how to master four simple hacks and embed them into a toy

![](img/628186dda7facdc011bf39c938de3975_67_0.png)

### About the Author

**Dan Aldred**

Dan is a Raspberry Pi Certified Educator and a lead school teacher for CAS. He is passionate about creating projects and uses projects like this to engage the students that he teaches. He led the winning team of the Astro Pi Secondary School Contest and his students' code is currently being run aboard the ISS. Recently he appeared in the QFC's 'inspiring teacher' TV advert.

Combining an old toy and a Raspberry Pi, you can embed a selection of components to create your own augmented toy that responds to user input. For example, take a R2-D2 sweet dispenser, light it up, play music and stream a live web feed to your mobile device.

Part one of this two-part tutorial covers setting up four basic features: an LED for the eye, a haptic motor to simulate an electric shock, a webcam stream from a hidden camera and the Star Wars theme tune broadcast to a radio. You may choose to combine these with your own hacks or use them as standalone features in other projects. Don't feel limited to just using a Star Wars toy either – we used the R2D2 figure because it was cheap, available and popular, but there's no limit to the toys that you can experiment with. Action figures (provided that they can be disassembled and/or have a stand or cavity that can be used to hold the electronics) and plushy or cuddly toys both lend themselves well to this kind of maker project, especially if they accompany a movie or TV show that has recognisable music or sound effects that you can make them broadcast. Part two next issue covers how to set up the toy and set up triggers to start features.

## 01 Set up an LED

LEDs are really easy to set up and control. They make a nice addition to your toy and can be used as eyes, flashing buttons or, in this example, R2-D2's radar eye. Take your LED and hold the longest leg; this is the positive arm and connects to the input. Wrap the resistor around the leg and attach to a female jumper jerky wire. Now take the negative arm and attach this to another jumper wire.

## 02 Attach the LED

Take the positive wire, the one with the resistor, to GPIO 17, which is physical pin number 11 (look at the far-left top pin and count down six pins). This pin will provide the current that powers the LED. Connect the other wire to any of the ground pins, (GND) 6, 9, 14, 20, 39; you may need to move this around later as you add more wires for the other components.

## 03 Light up the LED

To turn the LED on and off, use the gpiozero library, which was developed to simplify the interaction between code and a physical computer. Open the LX Terminal and type

```bash
sudo apt-get install python3-gpiozero
```

to install the library (Remove the '3' if you want to use it with Python 2). Once installation is completed, open a new Python window and import the LED module (line 2 of the following code). Assign the pin number of the LED (line 3) and finally turn it on and off (lines 6 and 8). Save your code and run it to make the LED flash. Change the timings to suit your own project.

```python
import time
from gpiozero import LED
led = LED(17)
led.off()
```

```python
while True:
    led.on()
    time.sleep(0.5)
    led.off()
    time.sleep(0.5)
```

### What you'll need

- An old/new toy
- Resistors
- Small disc motor
- LED
- A radio
- Small webcam
- Female-to-female jumper jerky wire

![](img/628186dda7facdc011bf39c938de3975_67_1.png)

## 04 Add a vibration

You may want the toy to vibrate or shake when it is touched. R2-D2 is known for giving out electric shocks and a safe way to emulate this is to add haptic feedback, similar to that when you press a key on the screen of your mobile. Pimoroni stocks a suitable disc motor (bit.ly/29hEla), which will deliver a short vibration. Take each of the wires and connect them each to a female-to-female jumper wire.

![](img/628186dda7facdc011bf39c938de3975_68_0.png)

## 05 Wire up the disc motor

Take the positive wire from the motor (usually coloured red) and attach it to GPIO pin 9; this is physical pin number 21. The black wire connects to a ground pin - the nearest is physical pin 25, from pin 21, drop down two pins on the left and this is number 25. Start a new program or add the code to your existing program. Import the RPi.GPIO library (line 1) and set the board to the BCM setting. This ensures that the GPIO numbering system is used.

```python
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
import time
```

## 06 Turn the motor on

To enable the motor, first set the output pin, number 9. This tells the program that GPIO pin 9 is an output. Next, set the GPIO pin to 'HIGH' (line 2), this is the same as turning it on. Current flows through and your motor will turn on. Add a short pause (line 3) before setting the output to LOW, which turns the motor off. Play around with the timings to find the perfect pause for your needs.

```python
GPIO.setup(9, GPIO.OUT)
GPIO.output(9, GPIO.HIGH)
time.sleep(5)
GPIO.output(9, GPIO.LOW)
```

## 07 Hack a web camera

A small web camera can be hidden within the toy as an eye or more discreetly within the body of the toy. This can be used to take photos or stream a live feed to a laptop or mobile device. Take your webcam and carefully strip away the plastic shell so you are left with the board and lens. Depending on the size of your toy, adjust the casing so that it fits and can be hidden.

![](img/628186dda7facdc011bf39c938de3975_68_1.png)

### R2-D2 in action

Check out the video of the completed R2-D2 toy hack and see the features in action. This may give you some ideas for your own toy hack. youtube.br/VroUsAjSsy

![](img/628186dda7facdc011bf39c938de3975_68_2.png)

![](img/628186dda7facdc011bf39c938de3975_68_3.png)

## 08 Set up a static IP address

Each time you connect to the internet, your Pi will be given a new IP address; this is called a dynamic IP address. This can cause issues, as when it changes, other devices will no longer be able to locate your Pi. To create one that stays the same (a static IP address), load the LX Terminal, type `ifconfig` and make a note of the `inet addr`, the `Broadcast` and the `Mask` numbers. Then type `route -n` and note down the `Gateway` address. Now type `sudo nano /etc/network/interfaces`, find the line `iface wlan0 inet dhcp` and change it to:

```bash
iface wlan0 inet static
address 192.168.1.5
netmask 255.255.255.0
gateway 192.168.1.1
network 192.168.1.0
broadcast 192.168.1.255
```

Replace the numbers with yours (which you noted down). Press CTRL+X together to save and exit the nano text editor. When you reboot your Pi, it will now have a static IP address which will not change when you reboot or reconnect.

## 09 Install the web server

To set up the web server, open the LX Terminal and update your Raspberry Pi by typing `sudo apt-get update`, `sudo apt-get upgrade`. Next, install the Motion software that will control the webcam: type `sudo apt-get install motion`. Once it is finished, attach your USB webcam and type `lsusb` and you will see that your webcam is recognised.

![](img/628186dda7facdc011bf39c938de3975_68_4.png)

![](img/628186dda7facdc011bf39c938de3975_69_0.png)

## 10 Configure the software – part 1

There are now seven configurations to change in order to get the most suitable output from the camera. You can experiment with these to see which produces the best results. In the LX Terminal, type:

```bash
sudo nano /etc/motion/motion.conf
```

...to load the configuration file. Locate the *daemon* line (you can find the lines by pressing CTRL+W, which loads a keyword search) and ensure that it is set to ON; this will start Motion as a service when you boot your Pi. Next, find the *webcam_localhost* and set this to OFF so that you can access motion from other computers and devices.

![](img/628186dda7facdc011bf39c938de3975_69_1.png)

## 11 Configure the software – part 2

Next, find the *stream_port*, which is set to 8080. This is the port for the video and you can change it if you are having issues viewing the feed; 8081 provides a stable feed. Then, find the *control_localhost* line and set it to OFF. The port that you will access the web config interface is on the *control_port* line and the default is 8080; again, you can change it if you have any streaming issues. The frame rate is the number of frames per second that are captured by the webcam. The higher the frame rate, the better the quality, but setting it higher than 6fps will slow the Pi’s performance and produce lag. Finally, set the *photo_capture* and specify the number of frames to be captured after motion has been detected.

## 12 Running Motion as a daemon

A daemon is a program that runs in the background providing a service; in this project you want to run Motion. You do not want to manually have to start it every time you load the Pi; it’s better that it automatically starts at bootup. In the LX Terminal, type `sudo nano /etc/default/motion` to edit the file. To set Motion to run as a service from bootup, you need to change the *start_motion_daemon* to Yes:

```bash
start_motion_daemon=yes
```

Save and exit the file using CTRL+X and restart your Pi.

![](img/628186dda7facdc011bf39c938de3975_69_2.png)

## 13 Starting the web feed

Before viewing the feed, type a note of your IP address. In the LX Terminal, type `sudo ifconfig`, although you will have set this in step 8. Then start Motion by typing `sudo service motion start`. Wait for few seconds for it to initiate, then open a browser window on your device. Enter the IP address of your Pi, including the port number that you set in step 11. If you are using VLC player, go to *File/Open Network* and enter the IP address of your Pi followed by the *stream_port* – for example, 192.168.1.50:8080. The port number in this example is 8080, but you set this in step 11 to 8081 or another value of your choice.

## 14 Install the PiRadio software

PiFM is a neat little library which enables your Raspberry Pi to broadcast to a radio. Note that this is only for experimentation and should you want to make a public broadcast you must obtain a suitable licence. Getting set up is simple: load the LX Terminal and make a new directory to extract the files into:

```bash
mkdir PiFM
cd PiFM
```

Then download the required Python files:

```bash
sudo apt-get update
sudo apt-get upgrade
wget http://www.omatots.com/pifm.tar.gz
```

Finally, extract the files using the code:

```bash
sudo tar xvfz pifm.tar.gz
```

## 15 Add a simple aerial and then broadcast

Setting up the hardware is really easy. In fact, there is no need to attach anything as the Pi can transmit directly from physical pin 7 without the need to alter anything. However, you will probably want to extend the range of the broadcast by adding a wire to GPIO 4 (pin number 7). Unbelievably, this can extend the range of the broadcast to up to 100 metres! Ensure that you are in the PiFM folder and then broadcast the WAV file with the code line:
