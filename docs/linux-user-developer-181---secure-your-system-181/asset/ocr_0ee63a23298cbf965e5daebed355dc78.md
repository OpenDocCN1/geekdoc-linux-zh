# Minecraft

# Use Python code to create pixel art in Minecraft

Continuing our series on coding in Minecraft, this issue we'll show you how to create automated pixel art

![](bbox=[0.06, 0.15, 0.18, 0.24])

# Calvin Robinson

is head of computing and network manager at an all-through state school. Calvin also consults with schools all over London, helping provide high-quality teaching and learning in computing.

![](bbox=[0.2, 0.33, 0.55, 0.46])

```
```
woolBlockGreenType = 5
#Black wool is blockID 15
woolBlockBlackType = 15

pixelArt = []

pos = mc.player.getPosition()
x = pos.x
y = pos.y + 7
#8 blocks above ground
z = pos.z
```
```

Creating pixel art in Minecraft can be quite therapeutic, but placing the blocks down one-by-one can also be incredibly time-consuming. However, by using Python and a handy little 'for' loop or two, we can create scripts to automatically build prefabricated pixel art directly into our Minecraft worlds.

If you're using Minecraft Pi edition on a Raspberry Pi, no additional software is necessary. We've also put together a number of tools to ensure this hack works on Linux, with a retail version of Minecraft. Therefore as a prerequisite, we assume you've installed McPiFoMo from our previous three issues. McPiFoMo includes MCPiPy by 'jlep' and 'bluepillRabbit' of MCPiPy.com, and Raspberry Jam developed by Alexander Pruss.

In this tutorial we're going to use Python to create an array that'll build blocks in rows and columns, to produce some pixel art. You'll need to keep your block ID list to hand, so you can select a range of blocks matching the colours you desire. We're going to be using wool for the choice here, but you're welcome to use any blocks that meet your purpose.

All Python scripts should be saved in the directory `~/home/minecraft/mcppy/`, regardless of whether you're running Minecraft Pi edition or retail Linux Minecraft.

# 01 Setting up the code

Here's the main code listing...

```
```python
from mcpy import minecraft
mc = minecraft.Minecraft.create()

#Wool is blockID 35
#Green wool is blockID 35:5 (type 5)
woolBlock = 35
```
```

Be sure to run Minecraft with the Forge 1.8 profile that's included in our McPiFoMo package.

```
```
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z + pixel, woolBlock, woolBlockBlackType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z + pixel, woolBlock, woolBlockGreenType)
```
```

# 02 Dissecting the code – Block types

There are several points of interest in the above code. Firstly, you'll notice we're using two variables per block. To set our block ID to 35:5, which is green wool, we use `woolBlock 35` and `woolBlockGreenType 5`. We'll do this for all the blocks that we add to our pixel art. If there's no block 'type', simply use `0`.

In our for loop, we call `woolBlock.woolBlockGreenType.` If you're regularly using blocks with no type (such as Diamond: 57), you can drop the type variable altogether.

# 03 Dissecting the code – Positioning

You'll also notice the position of our blocks is +7 on the y-axis. That's because we'll be creating pixel art of

![](bbox=[0.55, 0.92, 0.95, 1.0])

# Resources

+   - **Minecraft**
+     www.mojang.com/
+     games/
+   - **Wireshark**
+     www.wireshark.org
+   - **Python**
+     www.python.org
+   - **McPiFoMo**
+     http://rpiethat.co.uk/McPiFoMo.rar
+   - **Block IDs**
+     http://minecraft-ids.grahamedgecombe.com