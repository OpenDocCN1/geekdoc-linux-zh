
When you create a variable, new blocks appear in the Blocks Palette that you can use to change the variable's value and show or hide it on the Stage. If you want the score to go up by 50 each time the alien is hit (be generous — it's not an easy game!), you drag the Change score by 1 into your script and edit the number in it to 50. This block needs to go inside the If bracket that detects whether the alien touches the fireball, as you can see in Figure 10-10.

![](img/df9a01bf057d58c2401b5edabd6e8829_213_0.png)

Figure 10-10: Setting up the alien and detecting when it hits.

Scratch developed by the Lifelong Kindergarten Group at the MIT Media Lab. See https://scratch.mit.edu.

In Chapter 9, you will see how to display a sprite's position and direction on the Stage. By default, the values of variables are shown on the Stage, too. They appear in the top left, you can drag them wherever you want. This can be useful for tracing and fixing problems, but it can also get in the way of game. We recommend that you deselect the check box beside your score variable in the Blocks Palette to remove it from the Stage again.

In the finished game, the alien comes down the screen toward the ship, and the game ends when the alien catches the player's flying saucer. At this point, you will want to show the score variable on the Stage and use a special Control block that stops all scripts so that the program comes to an end. Figure 10-10 also includes the blocks that do this, which use a similar pattern to the blocks used for detecting when the alien is hit.

# Making Sprites Move Automatically

If you're wondering why we left the alien's movement to the end, it's because it makes it easier to test the game. You now have a spaceship that the player can move, a working firing mechanism, and an alien that dies and regenerates when shot. You can test all that at your leisure and fix any problems without having to keep up with the alien.

The alien moves from left to right and then from right to left, and then again. Each time it changes direction, you can move down the screen. This is quite sophisticated behavior, but you can create most of it using the blocks you've already used in this chapter. The art of programming is about working how you use the different blocks or commands at your disposal to achieve what you want to.

To start, you need to make a new variable and call it leapsize. When you create the leapsize variable, you're asked whether this variable should apply to all sprites or this sprite only. Make sure you click the button to make it apply only to this sprite. Scratch goes around the Forever loop, it moves the sprite and checks to see whether it's touching a fireball. The leapsize variable is used to store how much the alien's X position should change by time. If the alien is going right, the leapsize variable is 20, and if it's going left, it's -20.

If you don't set the leapsize variable for sprite only, you'll have problems when you duplicate the sprite later because the alien will use the same leapsize variable. The leapsize variable is for each sprite, and its value depends on where the sprite is on the screen. If you have sprites stuck at the edge of the screen, they are probably interfering with each other.

![](img/df9a01bf057d58c2401b5edabd6e8829_214_0.png)

When the alien reaches the edge of the screen, the leapsize variable is changed so that the alien goes back in the other direction and is moved down the screen by 20 units. Figure 10-11 shows movement script you need to insert into your alien's Forever loop as its first blocks. You'll find it easiest to assemble this set of blocks to the side of your main script and drag it into the Forever loop in your main script.

![](img/df9a01bf057d58c2401b5edabd6e8829_215_0.png)

Figure 10-11: The alien's movement script.

Scratch is developed by the Lifelong Kindergarten Group at the MIT Media Lab. See http://scratch.mit.edu.

The Operator blocks enable you to build more sophisticated instructions. They include the capability to do sums, check how one value compares to another, and combine different conditions in an If block. This can be hard to understand because you often put other blocks inside them.

The If blocks in your alien's movement script use Operator blocks to compare the X position with a number so that they can detect when the alien reaches the edge of the screen. We have found that -200 and 200 represent the minimum and maximum positions if you want to avoid the alien slipping off the Stage. The comparison blocks are diamond-shaped, so they slot into the If block. You can use one to check whether the X position is more than (>)200 and another to check whether it is less than (<)-200. You shouldn't check for an exact match with 200 or -200 because the alien starts at a random position and its steps increase by 20 units. If it started at X 170, it would go to 190 and 210 but never 200.

You also need to insert a block to set the starting value of leapsize to 20; otherwise, it will be zero and your alien won't move. In the Blocks Palette, the block for setting a variable's value to the start of your script, and edit it to set leapsize to 20. This block must go inside your alien's green flag script but outside your Forever loop. You can insert it as the first block under the Green Flag block.

# Fixing the Final Bug

In commercial software development projects, most of the time and money is spent testing programs to make sure they work as expected, and then fixing them when they don't. Errors in programs are often called bugs, and even in the simple game in this chapter, we have a bug that would enable the player to cheat.

If the fireball is moving up the screen and the player presses the Fire key, the firing sequence starts over. That means the fireball was traveling through the air, and a new one is sent up from the ship. That doesn't make logical sense, and then players suffer no consequences if they misfire: they can just fire again and it's as if the misfired shot never happened.

You can use a variable to keep track of when the fireball is moving up the screen so that you can stop the ship from allowing a fireball to fire again at that time. Variables like this, which are used only to keep track of whether something is happening, are called flags. The firing flag needs to be able to say whether the fireball is in play or not, so it has two values. While the fireball is onscreen, the firing flag value is 1. When it isn't, give the firing flag value of 0.

Set up your firing flag on the fireball sprite. Start by clicking that in the Sprite List. Click the Variables button at the top of the Blocks Palette, and click the option to make a variable. Give it the name firingflag and make sure the button is selected so that it's for all sprites. Check the box beside it in the Blocks Palette to hide it on the Stage.

After you've created the variable, you can drag it in the Variables section of the Blocks Palette to the start of the fireball's firing sequence, and to the end again. You should also update the fireball's green script so that it resets the firing flag to 0 at the start of a game, in case game ended while the fireball was onscreen. Figure 10-12 shows the final scripts for the fireball.

You also need to modify the script for the ship so that it only fires if the firingflag variable is 0 at the time the spacebar is pressed. This is a little bit complicated you will need to look tougher different of blocks to express this idea.
