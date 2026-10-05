There are also blocks that let you use virtual drums and pitched instruments to create music using Scratch. Notes are numbered: C is 60, D is 62, and so on. There's a block called Play Note 60 for ø.5 Beats that plays a note with a particular number for a certain duration. When you click this block in the menus to specify which note to play, a piano opens that you can use to select the note.

If you're new to music, you can generally get a good result by starting with C, sticking to the white notes, and making sure no two consecutive notes are too far apart on the piano.

![](bbox=[0.166, 0.188, 0.226, 0.253])

You can use a block Set Instrument to 1 to change the instrument, but if you want to use this, you need to install the different instruments first if you're using the original Scratch. To do so, click Terminal on the task bar at the top of the desktop and issue these commands in the Terminal window (explained in greater depth in Chapter 5):

```
sudo apt-get update
/usr/share/scratch/timidityinstall.sh
```

Finally, in order to finish the instruments, you need to reboot the Raspberry Pi. Save your work in any applications first, and then open the Applications menu, click Shutdown, and choose Reboot.

![](bbox=[0.166, 0.497, 0.226, 0.562])

The notes used in Scratch are the same as those used in Sonic Pi.(See Table 14-1, in Chapter 14).

# Creating scripts

Clicking blocks in the Blocks Palette is one way to issue commands to Scratch, but if that's all you're doing, you're not really programming. The fact is, if you have to click each block every time you want to run it, you're doing all the hard work of remembering the instructions, and the computer work only as fast as you can click the blocks.

A program is a reusable set of instructions that can be carried out (or run) whenever you want. To start to create a program, you drag blocks from the Blocks Palette and drop them in the Scripts Area of the screen. Most blocks mentioned so far in this chapter have a notch on the top and a lug on the bottom, so they fit together like jigsaw pieces. You don't have to align them perfectly; Scratch snaps them together for you if they close enough when you release the mouse button.