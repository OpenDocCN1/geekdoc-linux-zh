# # Using the Minecraft Module

For your first Python program for Minecraft, we will show you how to send a message to the Chat feature in the game.

We'll use the editor in Thny (the top part of the window). Enter the File menu to save it in your pi folder, and press F5 or Click the button to run it (note that you must have a Minecraft game session running for this work):

```
import sys, random
from mcpi import minecraft
mc = minecraft.Minecraft.create()
mc.postToChat("Welcome to Minecraft Maze!")
```

Your first line of code imports the sys and random modules. The random module, you'll need later to build a random maze as you develop this program.

To issue Python commands to Minecraft, use the minecraft.Minecraft.create() function and then add the command at the end. For example, to put a greeting in the Chat window, you might use the following:

```
minecraft.Minecraft.create().postToChat("Welcome to Minecraft Maze!")
```

That soon gets hard to read, so in the program you're working with, use so mc that you can use it as an abbreviation for minecraft.Minecraft.create().As a result, use the shorter line that you see in the program to post a message.

If your code isn't working, pay particular attention to the case. Python is case-sensitive, so you have to use upper- and lowercase as shown here. Look out for the mixed output— and lowercase in postToChat, and the capital M in minecraft.Minecraft.create().

![](bbox=[0.171, 0.63, 0.238, 0.699])

When you run the program, switch back to Minecraft to see your message on screen. It disappears after about 10 seconds.

# ## Understanding coordinates in Minecraft

As you might expect, everything in the Minecraft world has a map coordinate. Three axes are required in order to describe a position in the game world:

+   - x: This axis runs parallel to the ground. The world measures 255 blocks in this direction.