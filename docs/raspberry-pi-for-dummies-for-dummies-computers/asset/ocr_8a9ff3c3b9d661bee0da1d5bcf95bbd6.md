```
when clicked
broadcast gpioserver
broadcast config4out
broadcast config24in
forever
if
  gpio24 sensor value = 1
    wait 0,3 secs
else
  wait 1 secs
broadcast gpio4high
if
  gpio24 sensor value = 1
    wait 0,3 secs
else
  wait 1 secs
broadcast gpio4low
```

FIGURE 16-8: Scratch program to control the LED blink rate with a push button.

![](bbox=[0.178, 0.513, 0.228, 0.573])

Using GPIO pins is controlled by different blocks in Scratch 2.0. The main incompatibility, however, is that it sets the GPIO pin's internal registers to pull low by default. This means in place of connecting a push button switch between GPIO pin and ground, it should be placed between GPIO pin and 3V3. Care be taken not to connect it to 5V, or the Pi could be damaged.

# Using Python

The Python language was introduced in Chapter 11, and unlike Scratch's graphical-based programs, it uses entirely text-based instructions. Its great power is that the basic Python language can be extended to do more things by the use of libraries. These are functions that can be written in Python or any other language to extend what Python can do.

When using Python to access the GPIO pins, you have a number of different libraries you could choose that give you access to them. They provide not only normal input/output access but access to some of the special functions or capabilities of certain pins. We have deliberately written the next two examples in a style to match, as closely as possible, the two Scratch examples we have just presented, so that you can see how they are.