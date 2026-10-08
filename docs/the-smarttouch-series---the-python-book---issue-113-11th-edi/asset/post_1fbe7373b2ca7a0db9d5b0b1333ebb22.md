
## Use Python with Pi

Extract the files into:

```bash
start_motion_daemon=yes
mkdir PiFM
cd PiFM
```

Then download the required Python files:

```bash
sudo apt-get update
sudo apt-get upgrade
wget http://www.omattos.com/pifm.tar.gz
```

Finally, extract the files using the code:

```bash
sudo tar -xvzf pifm.tar.gz
```

### 15. Add a simple aerial and then broadcast

Setting up the hardware is really easy. In fact, there is no need to attach anything as the Pi can transmit directly from physical pin 7 without the need to alter anything. However, you will probably want to extend the range of the broadcast by adding a wire to GPIO 4 (pin number 7). Unbelievably, this can extend the range of the broadcast to up to 100 metres! Ensure that you are in the PiFM folder and then broadcast the WAV file with the code line:

```bash
sudo ./pifm name_of_wav_file.wav 100.0
```

In this example, the Star Wars theme will play, but you can create and add your own sound files. The ‘100.0’ refers to the FM frequency of the broadcast; this can be changed between a range of 88 and 108MHz. Turn on your radio and adjust to the appropriate frequency and you will hear your message being played.

### 16. Stop the broadcast

If you wish to end the broadcast before the song or voice has finished, then you will need to kill the transmission. In a new terminal window, type `top`. This will list all the running programs. Look for PiFM somewhere near the beginning of the list and note the ID number. Return to the LX Terminal and type `sudo kill 2345`, replacing the 2345 with the appropriate process ID number. This will ensure that each broadcast is new and the Pi is only trying to transmit one WAV file at a time.

![](img/e016e192a91ffc1a9e474690a590742f_170_0.png)

### 17. Next time...

You now have four mini hacks which you have prepared and can adapt and combine. You may want to try embedding some of your own hacks that you have created. Over the page we will cover how to wire up and deploy them!

![](img/e016e192a91ffc1a9e474690a590742f_170_1.png)

## BCM number

GPIO pins are a physical interface between the Pi and the outside world. At the simplest level, you can think of them as switches that you can turn on or off. You can also program your Raspberry Pi to turn them on or off (output). The GPIO.BCM option means that you are referring to the pins by the ‘Broadcom SoC channel’ number. The GPIO.BOARD option specifies that you are referring to the pins by their physical location on the header.

![](img/e016e192a91ffc1a9e474690a590742f_170_2.png)

## Hack a toy with the Raspberry Pi: Part 2

Embed your hacks into your toy and create the code to bring it to life

**Resources**
- An old/new toy
- Resistors
- Small disc motor
- LED
- A radio
- Small webcam
- Female-to-female jumper wire
- Tactile button

In part one of this ‘hack a toy’ tutorial you created four hacks that were originally used to augment a £3 R2D2 sweet dispenser making it light up, vibrate, play music and stream a live web feed to a mobile device. You may have been working on your own features to use and customise your toy. Part two of this tutorial begins by showing two different ways to set up and use a button to trigger your hacks. One method is to add and code your own button, the second method is to utilise the toy’s own built-in button. The next part walks you through how to wire up, code and test each of the individual features before combining them into a single program which will bring your toy to life.

### 01 Prepare a button

A button is a simple and effective way of triggering the hacks that you created in part one of this tutorial. Take a 4 x 6mm tactile button or similar and solder / attach a wire to each of its sides. Take each wire and connect it to one end of a female-to-female jumper wire. You can solder these into place or remove the plastic coating and wrap them around each metal contact.

![](img/e016e192a91ffc1a9e474690a590742f_171_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_171_1.png)

### 02 Set up the button

Next set up and test the button to ensure that it is working correctly. Take one of the wires and slot it onto GPIO pin 17, this is physical pin number 11 on the board. The second wire connects to a ground pin, indicated by a minus sign or the letters GND. The pin directly above GPIO pin 17 is a ground pin, physical pin number nine. This will complete the circuit and make the button functional.

### 03 Test the button

Open your Python editor and start a new file. Use the test program below to check that the button is functioning correctly. To ensure the buttons are responsive, use a pull-up resistor code `GPIO.PUD_UP` on line 4. This removes multiple touches and means that only one ‘press’ is registered each time the button is pressed. Save and run the program. If it is working correctly it will return the message “Button works”.

```python
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.cleanup()
GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)
while True:
    if GPIO.input(17) == 0:
        print("Button works")
```

### 04 Use the button on the toy

Instead of adding your own button you can utilise an existing button on the toy to trigger the events. On the R2D2 example this is the button at the front which releases the sweets and plays the classic R2D2 beep sound. Using a screwdriver or suitable tool, open the casing of your toy and then locate the electronics of the button. Locate the negative wire and cut this in two. Now attach a jumper wire to each of the ends. You can test that the connection is still working by joining the two jumper wires together and pressing the button.

### 05 Wire up your button

If your toy has a button to trigger a sound or movement then it will use batteries. These will sit in a case; we can bypass the battery circuit you added in Step 4 creates a secondary circuit. When you press the button you join the two contacts and in turn complete the circuit, this sends a small current around the circuit which can be detected by the GPIO pin on the Raspberry Pi. Take one of the wires and attach it to GPIO pin 1, the 3.3 volts which will provide the current.

Attach the other wire to GPIO pin 15, physical pin number 10. Pin 15 checks for a change in current.

When the button is in its normal state, i.e. it has not been pressed, no current flows from the 3.3v pin as the circuit is broken. When you press the button it joins the contacts, the circuit completes and the current flows. Pin 15 registers a change in state which is used to trigger an event.

### 06 Test the button

Open a new Python file and enter the test code below. On line four a Pull Down is used to check for the change in state. The toy’s button completes the circuit and GPIO pin 15 receives a little current. Its state becomes True or 1, line six, and then it triggers the display of a confirmation message. The final line prints out a confirmation message each time the button is pressed.

![](img/e016e192a91ffc1a9e474690a590742f_172_0.png)

```python
import time
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(15, GPIO.IN, GPIO.PUD_DOWN) #checks for a change on pin 7
while True:
    if GPIO.input(15) == 1:
        print ("You touched R2D2!")
```

### 07 Wire up the LED

Now to connect the individual hacks to your toy. These examples are based on Part One of the tutorial but can be replaced with your own. Shut your Pi down and unplug the power. Assuming that the LED is connected to the jumper wires, take the positive wire of the LED, the one with the resistor, and attach it to GPIO pin 21. This is physical pin number 40, the one at the very bottom-right of the pins. The black wire connects to a ground pin. The nearest one is physical pin 39 just to the left of pin 40; attach it there.

### 08 Wire up the motor

Next take the positive wire from the motor, usually coloured red, and attach it to GPIO 09, which is physical pin number 21. You will then need to connect the other wire to any of the ground pins, (GND) 6, 9, 14, 20, 39. You may find that you need to relocate this wire later on as you add more wires for the other components.

### 09 Add the PiFM aerial

The Raspberry Pi can broadcast to your radio directly from physical pin 7 without the need to alter anything. However, you will probably want to extend the range of the broadcast by adding a wire to GPIO 04, physical pin number 7. Unbelievably this can extend the range of the broadcast up to 100 metres. You must use physical pin number 7 to broadcast so move around any other wires that may be attached from your own hacks.

![](img/e016e192a91ffc1a9e474690a590742f_172_1.png)

![](img/e016e192a91ffc1a9e474690a590742f_172_2.png)

### 10 Add the web camera

The web camera is the simplest component to connect as it uses one of the USB ports. Once you have plugged it in use

## gpiozero

This is a smart Python library that makes interaction with the GPIO pins really simple, for example you can control an LED with the code `led.on()`. It covers a massive range of components, hardware and add on boards. You can find out more here: https://gpiozero.readthedocs.io/en/v1.2.0/#
