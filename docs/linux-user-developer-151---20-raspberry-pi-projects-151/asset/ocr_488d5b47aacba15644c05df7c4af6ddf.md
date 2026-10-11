![](bbox=[0.05, 0.05, 0.95, 0.58])

# What you'll need

+   Breadboard & wires
+   - 16x16 LED Matrix
+   - 2x 74HC238
+   - 2x 74HC244
+   - 16x 220 Ohm Resistor
+   - Source code **FileSilos.co.uk**

# Build a complex LED matrix

LED Matrix display systems find use everywhere from gaudy kebab shops to impressive steampunk-styled systems

![](bbox=[0.05, 0.73, 0.15, 0.85])

**Tam Hanna**
has worked in IT since the Palm IIc days. A journalist, tutor, speaker and author, Tam has seen every aspect of the mobile market more than once

Driving LEDs in an efficient fashion is a science of its own.
The common availability of single-board computers has put the necessary technology within reach of everyone.
When dealing with LED displays, two different systems must be considered. We will focus on traditional matrix-based systems made up of one or more LEDs. Their affordable nature makes them ideally suited to classic display applications: they communicate currency prices, provide stock-brokers with updates from the trading floor and have even been used as basic displays for primitive oscilloscopes.
Finally, we will also provide you with an overview of electronic basics. This tutorial is a bit more advanced than the ones we usually run in this section of the magazine, and it's also worth noting that we're going to be programming with C rather than Python. Follow along using the code listing annos.

# 01 Think about LEDs

Standalone LEDs are primitive – they light up once current flows through them. Driving a few LEDs is as easy as connecting them to GPIO pins along with a resistor. Sadly, this method becomes wasteful once more than a few of them get involved – driving 16 diodes ties up 16 pins.

# 02 Arrange your diodes

Methods were devised to reduce the number of pins needed. Matrix-based systems are resilient to individual diode failures, and provide a pin-to-LED ratio of n=(n/2)². The following steps assume a 16x16 LED matrix which is made up according to Figure A. Since LEDs permit current in only one direction, you can enable a single LED by bringing the corresponding pins high and low.