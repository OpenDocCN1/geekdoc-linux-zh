# BUILD A RASPBERRY PI-POWERED BIGTRAK

The Raspberry Pi is a small, low-cost computer designed to promote an interest in computing and programming – but it doesn’t have to be straight-laced computing. In fact, in this article we’ll be showing you how you can use it to turn a Bigtrak into a robot. That’s educational, right?

The Bigtrak is a toy that takes in a list of straightforward commands (Go forwards, turn left, turn right) and then executes them. To make things more interesting we’re going to remove the existing circuitry and replace it with a Raspberry Pi, using a small motor driver to safely control the motors in the Bigtrak, which we’ll then set up to be controlled via a PlayStation 3 DualShock controller.

Everything required on the software side comes pre-installed on the latest Raspbian OS images, so all we need to translate changes from the controller to the motors is a small Python script that uses the Pygame and RPi.GPIO modules.

# 01 Opening up the Bigtrak – the easy bit

Before we can make any changes to the Bigtrak we need to get inside. First, flip the Bigtrak upside down and remove the nine screws from around the edge. These are mostly easy to get at, however the ones on the front may require a more slender screwdriver to reach them.

![](bbox=[0.46, 0.17, 0.9, 0.4])

# 02 Opening up the Bigtrak – the fiddly bit

The last two screws are located underneath the grey grille on the back. This grille is held in place by four plastic tabs that need to be pushed in while at the same time sliding the grille away from the Bigtrak. This can be quite tricky as there is limited space to get extra hands in to help out. It can help to wedge some thin plastic items (eg a guitar pick) into the sides to keep those two tabs unlocked, while using your fingers to push in the bottom two tabs and slide the grille upwards, allowing you to remove the screws.

![](bbox=[0.46, 0.41, 0.9, 0.65])

# 03 Removing the top

Put the Bigtrak back onto its wheels then carefully loosen the top and lift upwards. The lid is connected to the base with a ribbon cable and a switch, so only pull the top up far enough for you to tilt it to one side and expose the inside.

With the lid lifted up onto one edge, remove the screw holding the switch in place and detach it from the lid. Next, you need to unscrew the two screws on the PCB that hold the ribbon cable in place and let it slip free.

With the switch and ribbon cable disconnected, the lid should now come free and can finally be completely removed from the base of the Bigtrak.

# 04 Cut the wires

Cut the wires leading to the main PCB. The ones for the switch and power should be cut close to the PCB (so we can reuse them later) whereas the ones to the LED and speaker can be cut wherever you like.

# 05 Remove the engine

Turn the Bigtrak upside down and remove the four screws holding the engine in place (this will reduce the chance of soldering iron damage to the main body). Carefully turn the Bigtrak back over and lift it up until the engine slips free.

![](bbox=[0.45, 0.66, 0.9, 0.99])