The code starts off by defining the number of LEDs you have, the brightness you want to run them at, and the pins used for the data and clock lines. These lines are determined by the we Blink! is made, but these could be any two GPIO pins, if you want to experiment with more LED strips connected to the Pi. The leads variable is set to the class reference — use this reference by a dot and the method's name to call any method. The program simply sets each LED in turn to the three primary colors and back again. Note how in the setLED method the colors are given as three values in a tuple. It is the show method that actually displays the contents of the data buffer on the LEDs. If you don't call method, the LEDs do not change.

Though this is all very interesting, the results of running this program are not very spectacular — so let's make a game with this small LED strip.

# # Raspberry Invaders

To get this off the ground, the first thing you have to do is to build the hardware. Unfortunately, adding buttons is a bit trickier than it could be. This is because the LED strip takes all the GPIO pins — even the ones it doesn't use. There are two ways to round this problem: You could solder wires on the back of the Blink! and bring these out to your push buttons, or you could use an extender board, like the Black Hat Hack 3r or the Mini Black Hat 3r. Figure 17–7 shows where to solder the wires to the base of the Blink!, and Figure 17–8 shows the Black Hat Hack 3r extender board.

Your base in the righthand LED, but with the Black Hat board, you can position this LED so that your base is at the bottom of a vertical line.

We wrote the software using the pygame framework comes preloaded for the Pi's operating system, it's a great framework for handling sound effects. You should your sound samples in a directory and create them them in the same directory as this game file. You can steal these sounds

370 PART 5 Exploring Electronics with the Raspberry Pi