
middle in the original Scratch and on the right on Scratch 2. In the original Scratch, you can use two buttons in the top right (refer to Figure 9-1) to toggle the Stage between full size and small. In Scratch 2, click the Edit menu to find the option for Small Stage Layout. When the Stage is small, the Scripts Area is bigger, so you might find that useful when you're writing scripts in this chapter.

Maximize window

Enlarge sprite
Full Stage
Small Stage

![](img/df9a01bf057d58c2401b5edabd6e8829_181_0.png)

> Figure 9-1:
> The screen layout in the original Scratch.

| Blocks Palette | Scripts Area | Sprite List | Stage |
| :--- | :--- | :--- | :--- |

Scratch is developed by the Lifelong Kindergarten Group at the MIT Media Lab. See http://scratch.mit.edu.

## Positioning and resizing your sprite

You can drag and drop your sprite (the cat) around the Stage to position it where you would like it to be at the start of your program.

You can also resize the sprite. Two buttons above the Stage (refer to Figures 9-1 and 9-2) are used to enlarge or shrink a sprite. Click one of them, and the mouse pointer changes to arrows pointing outward (for enlarging) or inward (for shrinking). Click your sprite on the Stage repeatedly to change its size.

### Enlarge Sprite

### Shrink Sprite

### Stage

![](img/df9a01bf057d58c2401b5edabd6e8829_182_0.png)

FIGURE 9-2:
The screen layout in Scratch 2.

### Sprite List

### Blocks Palette

### Scripts Area

> Scratch is developed by the Lifelong Kindergarten Group at the MIT Media Lab. See http://scratch.mit.edu.

When you've finished resizing, clicking that that isn't a sprite to return the mouse pointer to normal and stop resizing.

## Making your sprite move

Experimenting with Scratch is easy. To try out different blocks, just click them in the Blocks Palette. For example, clicking the Move 10 Steps block, and you should see the cat to the right. You can also turn the sprite 15 degrees in either direction by clicking the appropriate blocks.

If your cat goes somewhere that you don't want it to (don't always?), you can click it on the Stage and drag it back to where you want. You can reset rotation in the original Scratch, too, by clicking the tiny cat at the top of the Scripts Area, holding down the mouse button, and rolling the mouse in a circle pattern on the desk until the sprite is at the angle you want. In Scratch 2, you can correct a

![](img/df9a01bf057d58c2401b5edabd6e8829_182_1.png)

TIP

CHAPTER 9 introducing Programming with Scratch 167

sprite's rotation by clicking the sprite's i button in the Sprite List, and then clicking and dragging the blue line on the direction indicator. When you've finished, click the back arrow to show the Sprite List again.

Not all of the blocks will work at the moment because some of them need to be combined with other blocks. There's no harm in experimenting, however. If you click something that doesn't work, you might get an error message, but you won't cause any harm to Scratch or your Raspberry Pi.

Next, you can use the different Motion blocks you can use.

## Using directions to move your sprite

You can use two different methods to position and move sprites. The first is to make your sprite "walk," and to change its direction when you want to walk the other way. The other is using grid coordinates, which we cover in the next section.

Here are the blocks you use to move your sprite in this (see Figure 9-3):

- **Move 10 Steps**: This makes your sprite walk in the direction it is facing. If your sprite has been rotated, the steps taken could move it in a diagonal line across the Stage. You can click the number in this block and then another number to increase or decrease the number of steps taken, but bigger numbers spoil the illusion of animation. It looks like the sprite is walking across the screen when the number of steps taken is too big.

![](img/df9a01bf057d58c2401b5edabd6e8829_183_0.png)

> Scratch is developed by the Lifelong Kindergarten Group at the MIT Media Lab. https://scratch.mit.edu.

- **Turn Right or Left 15 Degrees**: This block rotates your sprite. As the number of steps, you can edit the number to change the degree by which your sprite is rotated. It walks in the direction it is facing when you use Move 10 Steps block.

- **Point in Direction 90**: Whatever direction your sprite is facing, this block points it in the direction you want it to face. Use this block as is to reset your sprite to face right. You can change the number in this block to change the direction you want your sprite to, and the numbers are measured in degrees from the position of facing up.(See Figure 9-4). It helps to think of it like the hands of a clock: when the hand is pointing right, it's 90 degrees from the 12 o'clock position; when it's pointing down, it's 180 degrees from the top. To point left, you use -90. When you click the arrow in the right of the number box, it gives you a menu from which you can select the four main directions — but you can enter any number.

0

![](img/df9a01bf057d58c2401b5edabd6e8829_184_0.png)

FIGURE 9-4:
The number of degrees used to face in different directions.

> You might be wondering whether you can enter 270 to point left, and the answer is that it works, but it can cause errors in your programs. If you turn your cat to direction 270 and ask Scratch which way the cat is facing, it tells you -90. Avoid any inconsistencies like this, keep direction numbers in the range from -179 to 180.

- **Point Towards**: You can also tell the sprite to point towards the mouse pointer or another sprite. Use the menu in this block to choose what you would like your sprite to point towards.

If you're changing the number value in a block, you still need to click the block to run.

## Using grid coordinates to move your sprite

The second way you can move and position your sprite is to use grid coordinates. This treats the Stage as having a horizontal (X) and a vertical (Y) axis. Each point on the Stage can be identified by a pair of coordinates. The X-axis ranges from -240 on the left to 240 on the right. The Y-axis ranges from -180 at the bottom to 180 at the top. The center of the Stage is (0,0).

Here are the blocks you use to move your sprite using coordinates (see Figure 9-5):

- **Go to x y**: This block moves your sprite to a specific location on the Stage. By default, it returns to the center (0,0). Edit the numbers for X and Y to position your sprite somewhere else.
- **Glide secs to x y**: When you use the Go block, your sprite jumps to its new position. The Glide block makes your sprite float. You can change the number of seconds the glide takes, including decimals for part of a second (for example, 0.5 for half a second).
- **Change X by 10**: This moves your sprite to the right. You can change the number of units and use a negative number if you want to move left. This doesn't affect your sprite's vertical position.
- **Change Y by 10**: This moves your sprite to the top. You can change the number of units and use a negative number to move the sprite down the screen. This doesn't affect your horizontal position.
- **Set X to 0**: This changes the horizontal position of your sprite on the Stage, without affecting its vertical position. The value 0 returns it to the center of the screen horizontally, and you can edit the number to position it left or right of that.
- **Set Y to 0**: This changes the vertical position of your sprite on the Stage, without affecting its horizontal position. The value 0 returns it to the center of the screen vertically, and you can edit the number to position it above or below that. 

![](img/df9a01bf057d58c2401b5edabd6e8829_185_0.png)

FIGURE 9-5:
The coordinate system of the Stage.
