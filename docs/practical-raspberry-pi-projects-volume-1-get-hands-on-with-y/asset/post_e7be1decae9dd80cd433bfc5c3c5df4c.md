
# ASSEMBLE A MINECRAFT POWER MOVE GLOVE

Raspberry Pi, then enter this IP address into this line of code: `mc = minecraft.Minecraft.create()`. For example, `mc = minecraft.Minecraft.create("192.168.2.234")`, filling the empty brackets with the IP address of the other Raspberry Pi within your game. Remember that this is the IP address of the other player's Raspberry Pi and not your IP address.

## 14 Find your IP addresses

To find the IP address of a Raspberry Pi, load the LX terminal, type `ifconfig` and press `Enter` — the address will be displayed on the line that begins `inet_addr`. This is the number that you enter into the `mc = minecraft.Minecraft.create("192.168.2.234")`. Remember on the Glove Raspberry Pi to enter the IP address of the other player's Raspberry Pi, not yours.

## 15 Run both programs

No game would be complete without some healthy competition and strategy. A second program is deployed to the other player on the network which tracks and registers if they catch or hit you. The program checks the block that they have hit and compares it to the player's location.

![](img/a1548a579bd09ff29b2b92de3f565e63_128_0.png)

## 16 Test for hits

To check if the other player has hit you, run the second program on the Raspberry Pi of the player who is doing the chasing. The program basically finds the other 'glove' player's current position and stores it in a variable. It then compares the position that you hit with your sword, recording and storing this too. The program then compares the values. If they match then you have hit the other player and have won the game. If not, get ready for a trade of power moves. Note that in order to monitor where the other player is, you must set the code line `mc1 = minecraft.Minecraft.create()` to the IP address of the Glove Raspberry Pi; for example, `mc1 = minecraft.Minecraft.create("192.168.1.251")`.

## 17 Game on

Now you are ready to play, check again that the IP addresses are set for the other Raspberry Pi and not your own. Build a new Minecraft world and start a new game on the Raspberry Pi with the player who is chasing. When loaded, the glove player joins the multiplayer game – this will be called Steve (see Step 11). When loaded, you should see both players in the world. Then run the 'Pi Glove power moves' program, and on the other Pi run the 'You hit me program'. Don't forget to set the IP addresses to each other Raspberry Pi.

Once set up, you can modify the power moves, use different blocks and add new moves. You could create a timer and a scoring system to track which player can survive the longest. If you are feeling adventurous, you may want to make another Power Glove, one for each player.

> The program compares the values, if they match then you have hit the other player and have won the game. If not, then get ready for a trade of power moves.

### PiGlovePowerMoves.py (Cont.)

```python
#Main code to run
try:
    lava_check = 0
    mc.postToChat("Minecraft Power Glove Enabled")
    while True:
        if GPIO.input(L7) == 0:
            Firewall()
        if GPIO.input(L8) == 0:  #Needs to stop
            Lay_Lava()

        #GPIO.output(L10, GPIO.LOW)

        if GPIO.input(L3) == 0:
            Mega_Jump()

        if GPIO.input(L1) == 0:
            Mega_Water_Puddle()

except:
    print("Error")
```

### YouWereHit.py

```python
import time
from mcpi import minecraft

mc1 = minecraft.Minecraft.create("192.168.1.245")
#The other players IP address goes here

mc = minecraft.Minecraft.create()
mc.postToChat("####Here I come")
Hit = 1

while Hit == 1:

    #Find the block stood on
    stood_x, stood_y, stood_z = mc1.player.getPosition()
    time.sleep(0.1)

    blockHits = mc.events.pollBlockHits()
    if blockHits:
        for blockHit in blockHits:
            if stood_z == blockHit.pos.z and stood_y == blockHit.pos.y+1:
                mc.postToChat("I got you")
                time.sleep(1)
                mc.postToChat("###GAME OVER###")
                time.sleep(1)
                Hit = 0
                mc.postToChat("####Restart Hit Code")
```

![](img/a1548a579bd09ff29b2b92de3f565e63_129_0.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_129_1.png)

# What you'll need

- Breadboard & wires
- 16x16 LED Matrix
- 2x 74HC238
- 2x 74HC244
- 16x 220 Ohm Resistor

# Build a complex LED matrix

LED matrix display systems find use everywhere from gaudy kebab shops to impressive steampunk-styled systems.

Driving LEDs in an efficient fashion is a science of its own. The common availability of single-board computers has put the necessary technology within reach of everyone.

## 01 Think about LEDs

When dealing with LED displays, two different systems must be considered. We will focus on traditional matrix-based systems made up of one or more LEDs. Their affordable nature makes them ideally suited to classic display applications: they communicate currency prices, provide stock-brokers with updates from the trading floor and have even been used as basic displays for primitive oscilloscopes.

Standardise. LEDs are primitive – they light up once current flows through them. Driving a few LEDs is as easy as connecting them to GPIO pins along with a resistor. Sadly, this method becomes wasteful once more than a few of them get involved – driving 16 diodes ties up 16 pins.

## 02 Arrange your diodes

Finally, we will also provide you with an overview of electronic basics. This tutorial is a bit more advanced than the ones we've featured up until now, and it's also worth noting that we're going to be programming with C rather than Python. Follow along using the code listing above.

Methods were devised to reduce the number of pins needed. Matrix-based systems are resilient to individual diode failures, and provide a pin-to-LED ratio of n=(n/2)^2. The following steps assume a 16x16 LED matrix which is made up according to Figure A. Since LEDs permit current in only one direction, you can enable a single LED by bringing the corresponding pins high and low.

![](img/a1548a579bd09ff29b2b92de3f565e63_130_0.png)

Above The extended version of this schematic is inside File5ilo.co.uk — just sign in and head to the Issue #191 page

## 03 Harness the MUX

Our LED module has a total of 32 inputs, which overwhelms older versions of the Raspberry Pi. The first way to restrict their number comes in the shape of the 74HC238, a component described as a 3-to-8 line decoder/demultiplexer. Its function is described in the Figure B image on the next page.

## 04 Separate concerns

Chip two goes by the name of 74HC244, which is described as an octal buffer with tri-state capability. Tri-State outputs can physically disconnect themselves from the bus line. This permits you to tie their outputs together without fear of short circuits. As long as all but one chip are in tri-state mode, no current can flow between high and low output pins.

## 05 Round them up

Four GPIO pins control the currently-enabled 'line' of the display. Three pins configure the address which is to be emitted, while the signal emitted from the fourth pin is connected to the activity inputs. This ensures that but one IC is active. The 74HC244 ensures that but one of the two groups is active at any given time.

## 06 Configure the pins

We used a library from Hussam Al-Hertani's Herzwillie blog (herzwillie.com/2014/07/07/rpimmappgpio). The first step involves setting output functions. As the GPIOs are set to outputs, the tri-state feature might connect the internal state to the output pins of the IC. This could lead to internal shorting if the output is not turned off.

### Full code listing

```c
#include "GnammpGpio.h"
#include <unistd.h>
#include <stdio.h>

#define PINA0   2 // 3
#define PINA1   3 // 5
#define PINA2   4 // 7
#define PINA3   14 // 8
#define PINC0   17 // 11
#define PINC1   18 // 12

#define PIND0   23 // 16
#define PIND1   24 // 18
#define PIND2   10 // 19
#define PIND3   9 // 21
#define PIND4   25 // 22
#define PIND5   11 // 23
#define PIND6   8 // 24
#define PIND7   7 // 26
```

```c
void setAddress(unsigned char _which, mmapGpio* _where)
{
    if(_which&1)
    {
        _where->writePinHigh(PINA0);
    }
    else
    {
        _where->writePinLow(PINA0);
    }
    if(_which&2)
    {
        _where->writePinHigh(PINA1);
    }
    else
    {
        _where->writePinLow(PINA1);
    }
    if(_which&4)
    {
        _where->writePinHigh(PINA2);
    }
    else
    {
        _where->writePinLow(PINA2);
    }
    if(_which&8)
    {
        _where->writePinHigh(PINA3);
    }
    else
    {
        _where->writePinLow(PINA3);
    }
}
```

```c
void safelySetRow(unsigned char _which, mmapGpio* _where)
{
    _where->writePinHigh(PINC0);
    _where->writePinHigh(PINC1);
    if(_which==0)
    {
        _where->writePinLow(PINC0);
    }
    else
    {
    }
}
```
