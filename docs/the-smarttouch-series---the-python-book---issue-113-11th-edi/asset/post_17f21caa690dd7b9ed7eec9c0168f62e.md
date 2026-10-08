
## Gesture control

![](img/e016e192a91ffc1a9e474690a590742f_163_0.png)

## 17 Skywriter movements

The Pimoroni Skywriter HAT is an electrical near-field 3D gesture-sensing board that uses a 4-layer PCB for the best sensing performance, up to 5cm away! It has the capability to collect full 3D position data and gesture information (swipes, taps, double taps, flicks and swirls) and then respond to them with an action that you set. It also comes fully assembled.

## 18 Install the software

Pimoroni has made it extremely easy to install the software for your Skywriter HAT. Load the LX Terminal and type:

```bash
sudo curl -sS get-pimoroni.com/skywriter | bash
```

Follow the instructions that are displayed on the screen; these involve giving permission to install the software and agreeing to the changes that the library requires. This will now download the required libraries and a selection of Skywriter examples and programs for you to try out. When installation has completed, reboot your Raspberry Pi, and then you can get started with the next part of the process.

## 19 Your first Skywriter program

Open a new Python file, (remember to use the LX terminal method as used in Step 6, as administrative privileges are required) and add the code below. First import the libraries to talk to the Skywriter, lines 1 and 2. Next create a function called move that will sense the position of your finger on the Skywriter, line 3. Next read the x, y and z co-ordinates, line 4, and finally print these to the Python window. Save the program and run it. Move your finger over the Skywriter. Note that because it has touch-capacitive capabilities you do not need to actually touch the board, just hover above it.

```python
import signal
import skywriter

@skywriter.move()
def move(x, y, z):
    print(x, y, z)
```

![](img/e016e192a91ffc1a9e474690a590742f_163_1.png)

### Use Python with Pi

```text
login as: pi
pi@192.168.1.219's password:

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sun Sep 18 07:27:00 2016 from dan-pc.default
pi@raspberrypi:~$ sudo curl -sS get-pimoroni.com/skywriter | bash

This script will install everything needed to use
the Pimoroni Skywriter

=== Warning ===

Always be careful when running scripts and commands
copied from the internet. Ensure they are from a
trusted source.

If you want to see what this script does before
running it, you should run:
curl -sS https://get-pimoroni.com/skywriter

Note: Skywriter requires I2C communication

Do you wish to continue? [y/N]
```

### New Skywriter board

Pimoroni has developed a larger Skywriter gesture board which works in three dimensions. It can sense your gestures from up to 15cm away, which means that you can embed it underneath non-conductive materials. This makes it suitable for wearables and projects where you want to conceal the board. All the common gestures are recognised such as taps, flicks and double taps, but these can be made from further away. You can even use it as a mouse or keyboard. Find out more details here: http://bit.ly/2dJF0sw

### 20 Double tap

In this program you can double tap a part of the Skywriter board and it will tell you the location of the tap. This makes use of a variable called position, line 3, which stores your tap location as either north, east, south, west or centre, depending on where you tap it. Line 4 prints out the position that you double tapped at. For example, if you double tap at the top of the board it will print: Double tap! North. All signals are cleared after the tap to ensure that each tap is clearly identified, line 5. Save and run the program; tap, tap.

```python
import skywriter

@skywriter.tap()
def tap2(position):
    print('Tap!', position)
    if position == 'north':
        print('North')
    elif position == 'south':
        print("South")
```

### 21 A single tap

When making any of the gestures such as tap, double-tap, touch, flick and so on, you can identify the location of the gesture on the Skywriter board and respond with a particular action. For example, you can touch the board at the top; this is the North tap. The right is East, South is the bottom and West is on the left. A conditional can be used to check the physical position where you touched the Skywriter and then return one of five responses.

```python
import signal
import skywriter

def doubletap(position):
    print('Double tap!', position)

signal.pause()
```

### 23 Slow down the responsiveness

The double tap is when you press the Skywriter twice in quick succession, a tap is a single press, but, if you press it once and then again, it will be interpreted as a double tap. You may wonder how, a tap is distinguished from a double tap. To resolve this issue, add a separate rate to the tap code. This means that the action, the tap, is only repeated once. Increase the repeat rate value if you still find the two gestures are not distinct enough.

```python
@skywriter.tap(repeat_rate=1)
```

### 24 Sense a flick

Another useful gesture that you can detect is a flick. Simply set up the Skywriter to wait for flicks, line 1. Then create a function that recognises the flick and records the direction of the flick, for example, south to north or east to west, line 2. Then print out confirmation that a flick was registered including the start and finish positions of the flick direction, line 3.

```python
@skywriter.flick()
def flick(start, finish):
    print('Got a flick!', start, finish)
```

### 22 Sensing position

Create a new function that senses when the user taps the board, line 3, then wait for the tap and record the location on the board where the user touched it. This is stored in a variable called position, line 4. Add an if statement, line 6, to check and compare the position. If it is tapped at the top of the board, the north position, then print 'north'. Use an elif statement, line 8, to check for a tap at the bottom of the board, the south position. Save the program and run it.

```python
import signal
```

## 25 Edit your robot code

Now that you have tried some of the Skywriter commands you can use and adapt these to control the robotic arm. Open the previous robot arm file from Step 16 and import the additional required libraries at the top of the program window.

```python
import skywriter
import signal
```

![](img/e016e192a91ffc1a9e474690a590742f_165_0.png)

## 26 Add Skywriter movements to raise the elbow

Next add the code that controls the robot based on the Skywriter gesture that it senses. Under the function, set up the `touch` command to register a touch, line 1, and create a variable to hold the position where you pressed the board, north, south, east, etc., line 2. Now check the position and use an `if` statement to check if you touched the north position, line 3. If it is touched then use the robot arm code to move the arm, line 4. Finally print a quick message to inform the user that the elbow has now been raised.

```python
@skywriter.touch(repeat_rate=1)  # Raise / lower the wrist
def touch(position2):
    if position2 == 'north':
        MoveArm1([16,0,0])  # elbow up
        print("Elbow Up")
```

![](img/e016e192a91ffc1a9e474690a590742f_165_1.png)

## 27 Add more touch movements

Now add some more movements to the program. On the next line down and indented inline with the `if` statement position, add an `elif` statement to check for the south position being touched, line 1. If you touch the board at the bottom, in the south position, then it will register the response and move the elbow down, line 2. Save your program by pressing F5, then run and test it.

```python
elif position2 == 'south':
    MoveArm1([32,0,0])  # elbow down
```

## 28 Add control for the grip

Continue to build up and assign the arm movements to the various gestures you make. Below the previous line of code add another `elif` statement to check for the west position, line 1, then use the arm command code to open the grip, line 2. Close the grip by touching east on the Skywriter, line three, and then add the code to close the grip, line 4.

```python
elif position2 == 'west':
    MoveArm1([1,0,0])  # grip close
elif position2 == 'east':
    MoveArm1([2,0,0])  # grip open
```

## 29 Using Taps

Any of the Skywriter gestures can be used to control the arm. On a new line, create a new function to identify taps, line 1. Note that the repeat rate is set to a value of 1 to remove the possibility of a double tap. Next create a new variable called position1, line 2. This is to stop the gesture overwriting the previous variable (For example, if the light is turned on, you might wish to move the arm but keep the light turned on). On line 4, check the position of the tap, then print the movement that the arm will make, line 5 (This is optional). As with the previous steps, assign the movement code for the arm; for example move the shoulder up, line 6.

```python
@skywriter.tap(repeat_rate=1)
def tap_tap(position1):
    print("Tap", position1)
    if position1 == 'north':
        print("Shoulder Up!")
        MoveArm1([64,0,0])  # shoulder up
```

## 30 Shoulder down

To move the shoulder down, use a similar format to that in Step 27. On the next line down, in line with the indentation level of the `if` statement, add an `elif` statement to check for a tap on the south position, line 1. Add an optional print statement to display that a tap has been registered, line 2, and then add the command to move the shoulder downwards, line 3. Save and run your program.

```python
elif position1 == 'south':
    print("Shoulder Down!")
    MoveArm1([128,0,0])  # shoulder down
```

## 31 Put it all together

Continue to create your program in a similar fashion as demonstrated in Steps 26 to 30. First choose the type of gesture/input that you want to use, then set up a function to identify the gesture and the position on the Skywriter where the gesture took place, for example, north, south, west etc. Next use conditional, `if` and `elif` statements, to check the position and then respond with a robot arm movement using the codes found in the full listing. Use the example program in the tutorial resources as a basic set up for your ideas and then expand and customise to add your own gestures and movements.
