# ASSEMBLE A MINECRAFT POWER MOVE GLOVE

# 03 Test that the button works

Use this test code to ensure the button is functioning correctly. Once it is, the same setup method can be used throughout this project. To ensure the buttons are responsive, use the pull-up resistor with the code GPIO.PUD_UP – this will ensure that multiple touches aren’t registered on each button. Using Python 2.8, type in the code below, then save and run. If working correctly, it will return the message ‘Button works’.

```
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)

GPIO.cleanup()
GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)

while True:
    if GPIO.input(17) == 0:
        print "Button works"
```

![](bbox=[0.11, 0.37, 0.43, 0.54])

# 04 Create a power move

Now to create your first power move. The glove and code are structured in such a way that once the basic code template is set up, you can create your own power moves and assign them to each button, keeping both your ideas and your gameplay fresh. The first power move you will program enables you to place a wall of TNT between you and the player trying to catch you. They have a choice to go around the wall or slow it up, but it will slow them down. In a new Python window, type the code below and save the program into the home folder:

```
import time
def FireWall():
    mc.postToChat("Firewall Placed")
    TNT = 46,1
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-6, y, z+2, x+6, y+10, z+3, TNT)
    time.sleep(10)

while True:
    FireWall()
```

# 05 Open Minecraft

The updated version of the Raspbian OS comes with Minecraft pre-installed, it can be found under Menu>Games – so load it up. If you have used the Minecraft: Pi Edition before you will be aware that it runs better in a smaller-sized window, so don’t make it full screen. You may prefer to adjust and arrange each window side-by-side to enable you to view both the Python code and the Minecraft game at the same time.

# PiGlovePowerMoves.py

```
import time
from mcpi import minecraft

mc = minecraft.Minecraft.create("192.168.1.21")
#Replace with the other player's IP address

import RPi.GPIO as GPIO

#Set up the GPIO Pins
GPIO.setmode(GPIO.BCM)

#Sets the pin to high
GPIO.cleanup()
GPIO.setup(17, GPIO.IN, GPIO.PUD_UP)
#11 on the BOARD GREEN Firewall
GPIO.setup(18, GPIO.IN, GPIO.PUD_UP)
#12 on the BOARD BROWN Lava
GPIO.setup(3, GPIO.IN, GPIO.PUD_UP)
#21 on the BOARD BLUE Mega Jump
GPIO.setup(4, GPIO.IN, GPIO.PUD_UP)
#10 on the BOARD ORANGE Puddle
GPIO.setwarnings(False)    #switch off other ports

#Builds a wall of TNT which if the player hits will explode
def FireWall():
    mc.postToChat("Firewall Placed")
    TNT = 46,1
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-6, y, z+2, x+6, y+10, z+3, TNT)
    time.sleep(1)

#Lays Lava to slow down the other player
def LavaLava():
    Lava = 10
    check = 1
    mc.postToChat("Lava Deployed")
    while check == 1:
        time.sleep(0.2)
        x, y, z = mc.player.getPos()
        mc.setBlock(x-1, y, z, Lava)
        check = 1

#Performs a Mega Jump to lose players
def Mega_Jump():
    time.sleep(0.1)
    mc.postToChat("Mega-Jump")
    x, y, z = mc.player.getPos()
    mc.player.setPosition(x, y+15, z)
    time.sleep(1)

#Creates a Puddle to slow down the player
def Mega_Water_Puddle():
    mc.postToChat("Mega Water Puddle")
    time.sleep(0.2)
    WATER = 9
    x, y, z = mc.player.getPos()
    mc.setBlocks(x-5, y, z-4, x-1, y, z+4, WATER)
    time.sleep(1)
```

# GPIO pins

GPIO pins are a physical interface between the Pi and the outside world. At the simplest level, you can think of them as switches that you can turn on or off (input) or that the Pi can turn on or off (output). The GPIO_BCM option means that you are referring to the pins by the "Broadcom SOC channel" number, GPIO_BOARD specifies that you are referring to the pins by the number of the pin and the plug – the numbers printed on the board.