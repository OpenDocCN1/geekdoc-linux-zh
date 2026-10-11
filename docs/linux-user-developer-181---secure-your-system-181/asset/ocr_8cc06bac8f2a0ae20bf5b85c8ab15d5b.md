Battleships

# Part 2: Command the seas with Sense HAT Battleships

The final part of our series on creating the classic game of Battleships using a Sense HAT on a Raspberry Pi

Dan Aldred
is a Raspberry Pi enthusiast, teacher
and coder who
enjoys creating
new projects
and hacks to
inspire others to
start learning.

+   * Raspberry Pi
+   www.raspberrypi.
+   org/products
+   * Sense HAT
+   http://bit.ly/
+   Battleship
+   SenseHAT

![](bbox=[0.21, 0.31, 0.92, 0.6])

In the first part of this tutorial [LJUD#180, Tutorials, p74]
you started to build the classic game of Battleships,
coding the features such as deploying ships, firing
torpedoes and keeping a running total of your score.
In part two, you will begin by installing a small program
which enables you to easily create animations to play
across the Sense HAT's LED matrix. These can be used
to introduce the game, display a game over message or
update the player wherever your game requires it.
The tutorial then completes the main mechanics of
the gameplay before setting up the code for deploying
the game. Begin by introducing the game with a range
of sounds and verbal announcements before scrolling a
boat animation across the display. Then create a simple
countdown from three to zero before the game begins.
The game utilises the main function we created in part 1
one. Once the game is over, we'll add the option to play it
again or not. If you move the joystick down, the program
plays a farewell sound, an animation is displayed and
then your game ends and the program closes. Move the
joystick up and you can select to play another round and
a new random layout is created. Check out the full game
in action here: https://youtu.be/So1WAJHCac.

+   1. **Create your own 8x8 animation**
+   There's a simple way to create an animation to
+   run on the LED matrix; a superb onscreen program that
+   enables you to manipulate the LEDs in real time. You can
+   change the colours, rotate and export the animation as
+   code. Begin by installing the Python PNG library, open the
+   Terminal and type sudo pip3 install png; then:
+   
+   git clone https://github.com/jrobinson-uk/
+   RP1_8x8GridDraw