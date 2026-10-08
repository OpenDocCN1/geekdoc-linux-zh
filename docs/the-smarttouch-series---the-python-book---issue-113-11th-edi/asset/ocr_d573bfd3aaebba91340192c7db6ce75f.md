# Use Python with Pi

```
#!/usr/bin/env python

#import the USB abd time libraries
import usb.core, usb.util, time

#allocate the name 'RoboArm' to the USB device
RoboArm=usb.core.find(idVendor=0x1267, idProduct=0x0000)

#Check to see if arm is detected
if RoboArm is None:
    raise ValueError("Arm not found")

#Create a variable for duration
Duration=1

#Define a procedure to execute each movement
def MoveArm(Duration, ArmCmd):
    #start the movement
    RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)
    #stop the movement after specified duration
    time.sleep(Duration)
    ArmCmd=(0,0,0)
    RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)
```

+   **12 Create a function, part 3**
The last part of the function is to send the stop command to the arm, line 1. This connects to the arm and then transfers to the ArmCmd=(0,0,0) code that you set up in the previous step. Note that it is stored in a variable called ArmCmd which means that you can change the command that is transferred to the arm. This line is also indented.

`RoboArm.ctrl_transfer(0x40, 6, 0x100, 0, ArmCmd, 1000)`

+   **15 Run the program**
Now you have a complete program that will connect to the USB port, search for the robotic arm, prepare a function and then transfer an instruction that controls the arm, turning the light on. Save the program into your home folder. An easy way to do this is to press F5 on the keyboard, name and save the file, press Enter and then it will run. Look at the light on the arm, it will be on!

+   **13 Movement and action code**
Once you have completed the function, you can now use it to control the arm. Each movement or action has a unique set of digits that identify how long the movement last for, which motors need to be turned on or off and in which direction they need to turn. Each command begins MoveArm, then the first number is the duration the movement lasts for. For example, "1" is basically, do this instruction or movement for one second. This is then followed by the required motor information to turn it:

`MoveArm(1, [0,1,0]) #rotate base anti-clockwise`

+   **16 Turn the light off**
The light will now stay on unless you code it to turn off. If you add this line straight after the 'turn on' command, then the light will switch on and off so fast that you will not see it. On the next line down, add a short delay of two seconds, line one, and then turn the light off, line 2. Save and run your program using the F5 button. Check out the full code listing to see the code for all the available movements. You can use these code lines to build up movements and experiment with the arm's functions.

+   **14 Turn a light on**
On the next line down, underneath the function, add the code to turn the light on. Type the command `MoveArm(1, [0,0,1]) #light on.` The #light on is a comment and is not required to control the arm. It is used to identify to the user what the code does: it turns the light on. This is useful when you have several commands in the program.

> > **Use these code lines to build up movements and experiment with the arm's functions**