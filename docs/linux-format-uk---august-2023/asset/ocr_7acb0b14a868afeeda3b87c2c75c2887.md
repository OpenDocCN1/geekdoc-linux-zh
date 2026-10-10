keycodes that translate into what a keyboard would send to the computer. Finally we import consumer codes that are used by multimedia keyboards for extra functions (volume and so on).

```
from adafruit_hid.keyboard import Keyboard
from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS
from adafruit_hid.keycode import Keycode
from adafruit_hid.consumer_control import ConsumerControl
from adafruit_hid.consumer_control_code import ConsumerControlCode
import ConsumerControl
```

Create an object, i2c, to store the I2C pin setup. The Drum HAT is connected to GPIO16 (SDA) and GPIO17 (SCL).

```
i2c = busio.I2C(board.GP17, board.GP16)
```

Create an object, cap, and then call the CAP1188 module, passing the i2c object and the i2c address, 0x2c. We found the address using this resource: [https://pinout.xyz/pinout/drum_hat](https://pinout.xyz/pinout/drum_hat).

```
cap = CAP1188(I2C(i2c, 0x2c)
```

Next, create three objects. The first creates a USB keyboard that we can control. Then we set the keyboard layout to US. Finally, we enable an easier method to access ConsumerControl codes.

```
keyboard = Keyboard(usb_hid.devices)
layout = KeyboardLayoutUS(keyboard)
consumer = ConsumerControl(usb_hid.devices)
```

Create a while True loop to run the main code body.

```
while True:
```

Using a series of conditional tests, we will check for a button press. If pad 1 is pressed, the value will report True and trigger a sequence of code to run. First it will send the keycode for the B key, then print a message to the Python shell. All keypresses will be released and a short 0.3-second sleep will reduce the chance of multiple keypresses. Tweak this timing to suit.

```
if cap[1].value:
    keyboard.send([Keycode.B])
    print("B pressed")
    keyboard.release_all()
    time.sleep(0.3)
```

We won’t cover every pad on Drum HAT, as there are eight. We will pick out those that show different ways to send keypad commands. That said, every DrumsHAT pad is represented by cap[x], where x is a number between 1 and 8, so it is easy to remember which pad does what. All the code is in the download.

For the second pad, we will send a keyboard command to move the cursor to the right using the right arrow key. As before, send the code, print a message, release the keys and then pause.

```
if cap[2].value:
    keyboard.send([Keycode.RIGHT_ARROW])
    print("Right arrow pressed")
    keyboard.release_all()
    time.sleep(0.3)
```

The third pad will send a consumer code to mute the system audio. Consumer codes offer features that are not part of the standard keyboard specification: in this case, audio control. The process is the same. Send command, print a message, release keys, then pause.

```
if cap[3].value:
    consumer.send(ConsumerControlCode.MUTE)
    print("MUTED")
    keyboard.release_all()
    time.sleep(0.3)
```

Skipping to the fifth pad, we send a raw keycode value that maps to a Super/Windows/Command key. Pressing this pad will trigger a Start menu to appear.

```
if cap[5].value:
    consumer.send(227)
    print("Super / Windows key pressed")
    keyboard.release_all()
    time.sleep(0.3)
```

Save code to [CIRCUITPY](CIRCUITPY) as [code.py](code.py). CircuitPython loads code.py each time it is power cycled. In [Thonny](Thonny) click on Stop, then Run to restart the code. The Python shell prints each message as a key is pressed. The project can be used with Linux, Windows or Mac OS machines and appears as a basic USB keyboard.

![](bbox=[0.35, 0.09, 0.93, 0.32])

The circuit for this build uses only five wires, two resistors and some header pins. Take your time, though, as it can be tricky.

# USING THONNY WITH CIRCUITPYTHON

Thonny is an excellent Python editor. It works with Python on our computer and it can work with MicroPython and CircuitPython on a microcontroller, such as the Raspberry Pi Pico. [Thonny](Thonny) can be downloaded from [https://thonny.org](https://thonny.org) – once installed, go to Tools > Options, then click on the Interpreter tab and select CircuitPython (Generic). If we were using MicroPython on the Pico, we would select the Raspberry Pi Pico option; RP2040 is for other RP2040-based boards. Under Port, leave the option as Try To Detect Port. Automatically: Click OK to save. Plug in your Raspberry Pi Pico running CircuitPython, and Thonny detects and connects to the device. If it fails, click Stop to retry. If it still fails, go back to the Interpreter menu and manually select the port. The Python shell (also called a REPL. Read, Evaluate, Print, Loop) starts and in there we can interactively run code on the Pico. The Python shell is also used to show the output of a project’s code. We use it to print the current keypress as a debug method.