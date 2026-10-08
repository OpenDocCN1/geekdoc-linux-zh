# Control an LED using GPIO Use Python with Pi

Breadboard, or prototype board,
The Breadboard, provides an easy-to-use and solderless environment for creating and changing your development circuits

# Breadboard wire

A must for any budding electrical engineer,
these male-to-male and male-to-female wires make for fast and easy circuit building

# GPIO header

This provides a mechanism for both gathering input and providing output to electrical circuits, enabling reactive program

# Coloured LED

Different coloured LEDs are a great way to physically pair which part of the software is running and help you understand the program flow

![](bbox=[0.109, 0.116, 0.895, 0.555])

# The Pi's pins

# Pin numbers

# GPIO pins

+   01 Before we dive into writing code, let's take a look at the layout of the pins on the Pi. If you have a Pi in case, take it out and in front of it with the USB ports on the right. The next few steps we'll look at some of the issues you'll encounter when using the GPIO port.

+   03 If you take a look at the small white label, 'P1'. This is pin 1 and above it is pin 2. The right of pin 1 is pin 3, and above 3 to 4. This pattern continues until you get to pin 26 at the end. As you'll see in the next step, some pins have important uses.

+   05 The other pins on the board are GPIO (General Purpose Input/Output). These are used for other tasks that you need to do as your projects become more complex and challenging. Be aware that the USB power supply doesn't offer much scope for powering large items.

# Pi revision 1 or 2?

+   02 Depending on when you purchased your Pi, you may have a 'revision 1' or 'revision 2' model. The GPIO layout is slightly different for each, though they have the same functionality. Here we have a revision 1; revision 2 became available towards the end of 2012.

# Basic LED Lighting

+   04 Pin 1 is 5V3, or 3.3 volts. This is the main pin we will use in this guide to provide power to our GPIO. Pins 2 and 4 are 5V Pi is pin we will use here, which is ground. Ground pins are 9, 14, 20 and 25. You should always ensure your project is properly grounded.

+   06 Okay, let's get down to business and start making something. Firstly, get your breadboard, two wires, a 220 resistor and an LED. Note the slightly bent on one side of the LED; this is important for later. Make sure your Pi is unplugged from the mains supply.