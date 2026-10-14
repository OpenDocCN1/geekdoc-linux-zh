# The electronics

Connect switches and lights together using the magic of soldering.

![](bbox=[0.07, 0.25, 0.65, 0.42])

# 1 Prototype your layout

Rather than diving in and making your control panel, we'd recommend deciding how big you want your panel to be by make a mockup version in cardboard. Use a pen, pieces of Lego or actual switches to try different layouts until you find one that works for you (as we've done for our panel, pictured left). We'd also suggest that you don't replace every key in the game with a button – think about whether a dial or an illuminated switch would make for more useful and immersive interface.

# 2 Proof of concept

To get started with the Arduino, try building a simple device. Take an ordinary switch and connect one leg to one of the Arduino's GND pins and the other to digital pin 2. Now use a prototyping breadboard to connect the long leg of an LED to one end of a 1,000-Ohm resistor. Connect the free end of the resistor to digital pin 3 on the Arduino and the short leg of the LED to the other GND pin. See if you can program the Arduino to detect when the switch is closed and light the LED. The example programs at http://arduino.cc/en/Tutorial will show you how.

![](bbox=[0.45, 0.45, 0.95, 0.62])

![](bbox=[0.06, 0.62, 0.42, 0.83])

# 3 How to solder

Soldering is mainly about keeping a steady hand. Clamp or blu-tack the wires so that the ends overlap, then apply the soldering iron for a few seconds and touch the solder to the wire so that it melts and flows across the surface. Make sure you allow the soldered wires to cool before moving them.

![](bbox=[0.45, 0.72, 0.95, 0.88])

# Crimping

Plugging bare wires into the Arduino doesn't work very well because the ends aren't stiff enough to push into the headers. You need metal spikes called crimp connectors on the ends of the wire. You can buy these and attach them yourself, but

It's simpler and more reliable to buy pre-crimped wire. Get 30cm wires with male crimp connectors at each end. You can cut these in half so you have a bare wire to solder to your switch at one end, and the crimp connector at the other.

# 4 Add connection leads

Every switch and light on your control panel needs its own connection leads. Ribbon cable makes for tidier wiring, but it's harder to solder and you can't move switches around if you change your mind about the positioning. Use 2.4mm heatshrink tubing to insulate the ends.