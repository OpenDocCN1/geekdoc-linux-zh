
# Learn to code BASIC with FUZE

Discover the language that started it all

**TUTORIAL**

## 01 Hook up FUZE BASIC

![](img/c7d3278283754436651c50a2e9c72912_46_0.png)

Some of the FUZE models already have a Raspberry Pi built in, so all you need to do is hook it up to a monitor and power source to get it going. Make sure the SD card is placed into the slot before you plug it in using the supplied power adaptor.

## 02 BASIC interpreter

The FUZE will boot into a desktop of a modified Raspbian. Here you can do your normal Raspberry Pi-related activities, but what we’re interested in is the FUZE BASIC option on the desktop that takes us to the BASIC interpreter.

## 03 Say hello

Our first foray into a programming language needs to be done right with a proper “Hello World” statement. It’s very simple to do in BASIC and just requires you to write:

> PRINT “Hello World”

## 04 Look around you

While this version of BASIC has been updated since the BBC Micro days, you can still perform some of its more simple tasks and the infamous GOTO 10 command. You can do this by executing commands like this:

> 10 PRINT “Hello World”
> 20 GOTO 10

> **Note:** FUZE will boot into a desktop of a modified Raspbian. Here you can do all your normal Pi activities.

## 05 The modern way

Press Esc to end the loop. BASIC has seen some improvements in this version, so we can create this endless loop of Hello World by using a better loop statement in the code editor. To access the editor, press F2.

## 06 Modern loop code

The code for this is quite simple: we create a CYCLE, place the command within it and then tell the code to return to the beginning of the cycle with REPEAT at the end. In our case:

```basic
CYCLE
PRINT “Hello World”
REPEAT
```

## 07 Save and run the code

Once you’ve typed it in, you can press F3 to bring up the option to save the code. For now, just call it helloworld and press Return. Once that’s done the code will run, looping Hello World over and over. Press Esc twice to end the loop.

## 08 Make variables

Creating a variable in BASIC is easy and is like most other languages:

```basic
A = 5
```

Use PRINT 'A' to confirm it's worked. You can modify the value by adding a number or other predefined variables like so:

```basic
A = A + 5
A = A + B
```

## 09 Something more complicated

Automatically increasing the value of a variable is easy. Let's create a fixed loop that prints out A as it increases from 1 to 5:

```basic
CLS
A = 0
FOR p = 1 to 5 CYCLE
  A = A + 1
  PRINT A
REPEAT
END
```

## 10 Wire up a project

The I/O board offers a lot of extra functionality that's perfect for learning physical programming. While you can connect directly to the Pi's GPIO ports via the header, you can also use the custom ports. The tray at the top of the FUZE is perfect to slot the breadboard into, so do that now.

## 11 Wire up a light

Choose one of the LEDs from the pack of electronics – any colour is fine – and then insert the short end into one of the two pins along the top and insert the long end into the middle section. Grab a 100Ω resistor (brown black brown gold) and insert one end into one of the pins that are on the same vertical row as the long end of the LED.

![](img/c7d3278283754436651c50a2e9c72912_47_1.png)

## 12 Connect the light

Place the other end of the resistor on a pin in a different vertical column and then use a jumper wire to connect GPIO 0 to this end of the resistor on the vertical. Finally, attach a wire to GND on supply and put it on the same row as the short end of the LED.

## 13 Easy operation

To activate the light, exit the editor using Esc and type the following line to let it know to set GPIO 0 as an output:

```basic
>PinMode (0,1)
```

To activate it and then deactivate it, use:

```basic
>DigitalWrite (0,1)
>DigitalWrite (0,0)
```

## 14 Light coding

Now that we've got our light working, let's create a little code that will turn it on and off repeatedly:

```basic
CLS
PinMode (0,1)
CYCLE
DigitalWrite (0,1)
Wait (1)
DigitalWrite (0,0)
Wait (1)
REPEAT
END
```

## 15 Bigger project

![](img/c7d3278283754436651c50a2e9c72912_48_0.png)

*Below our traffic crossing setup will activate the LEDs in sequence*

Let’s ramp up the lighting setup on the breadboard and make it into a traffic crossing setup. Add two extra lights in the same way we added the original LED and attach them to GPIO pins 2 and 3. Wire up a button by attaching one end to pin 7 and the other end to a new 3.3V rail taken from the second set of power pins. The button will make the lights go 'red' in sequence, then after a pause go back to 'green' – see **Fig. 01** for the full code.

## 16 CLS

The CLS command clears the current display. This is helpful to make sure any errors or printouts from your code will show up without possibly blending in with outputs from previous programs or runs.

## 17 Use PinMode

The numbers on the PinMode variable handles the GPIO port (X) as well as whether it’s an output (1) or input (0). It is therefore constructed like so for GPIO X as an output:

```basic
PinMode (X,1)
```

DigitalWrite is constructed similarly for output pins, with 1 being on and 0 being off.

## 18 IFTHE

Unlike other coding languages, when you create an IF statement you need to make sure THEN is appended to let BASIC know that the following code is for a True situation.

## 19 digitalRead

As pin 7 in this code is set as an input, we want to read when it’s activated (ie when the button is pressed). Our button completes the circuit when pressed so the read needs to be 1.

## 20 ENDIF

Let the code know when the IF statement ends by adding ENDIF to the end of it. This can make it slightly easier and clearer for figuring out where an IF begins and ends compared to other languages.

**Fig 01**

```basic
CLS
PinMode (0,1)
PinMode (1,1)
PinMode (2,1)
PinMode (7,0)
CYCLE
  DigitalWrite (2,1)
  IF digitalRead (7) = 1 THEN
    Wait (1)
    DigitalWrite (2,0)
    DigitalWrite (1,1)
    Wait (1)
    DigitalWrite (1,0)
    DigitalWrite (0,1)
    Wait (5)
    DigitalWrite (0,0)
    DigitalWrite (1,0)
    DigitalWrite (2,1)
  ENDIF
REPEAT
END
```

***

# THE ESSENTIAL GUIDE FOR CODERS & MAKERS

# PRACTICAL Raspberry Pi

## Contents

- 58 Discover a new musical instrument
- 60 Upgrade your Pi-powered Bigtrac
- 64 Transform your Pi into an oscilloscope
- 70 What is the new browser?

## BUILD A SUPER RASPBERRY PI

Pool the resources of multiple Pis to create your own scalable Pi supercomputer

The Raspberry Pi is actually quite powerful for its price. On its own, though, you won’t be doing any extraordinary calculations – or compiling anything strenuous at all, for that matter. However, as it’s readily available and fairly cheap, you can get twenty of them for the price of a new computer. Each of them on their own will be no different, but link them together over a network and you can have them share their power and vastly increase the amount they can process.

This kind of setup is generally known as a Beowulf cluster, so named for the eponymous hero of the epic poem in which Beowulf is described as having “thirty men’s heft of grasp in the gripe of his hand”; it’s not ridiculously hard to achieve, either – all you need is a lot of Raspberry Pis, a bit of Python know-how and a reason to use it. This makes it a good project for things like classrooms, after-school Pi clubs and the like – really, anywhere there’s a collection of Pis available for general use.

The more Raspberry Pi nodes you add into the setup, the more powerful it will become, which means you can start with just two or three at home and then gradually add more and more to your cluster, if you want to. And because of the way it all works, you can hook in and control your SuperPi cluster from your main computer as well, making this as accessible as it is scalable.

Over the next two pages we’re going to show you how to get your Raspberry Pi set up ready for use, including all the tools you’ll need, how to get them all connected and then finally what you can do with all that processing power. We’d love to see your SuperPi once it’s finished – drop us a tweet!

www.linuxuser.co.uk
