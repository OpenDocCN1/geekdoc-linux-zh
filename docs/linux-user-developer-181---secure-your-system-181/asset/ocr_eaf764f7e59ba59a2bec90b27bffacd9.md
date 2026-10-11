eight blocks high, and we want to make sure it appears upward from ground level.

```
```python
pos = mc.player.getTilePos()
x = pos.x
y = pos.y + 7
z = pos.z
```
```

Our blocks are built in rows:

```
```python
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBlackType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockGreenType)
```
```

```
```python
woolBlockOrangeType = 1
#Blue wool is type 11
woolBlockBlueType = 11
#Brown wool is type 12
woolBlockBrownType = 12
#White wool is type 0
woolBlockWhiteType = 0
#Pink wool is type 6, but double jungle wood slabs look good (125:3)
woolBlockPink = 125
woolBlockPinkType = 3
```
```

# ## 06 Creating a Steve head – extending your for loops

We’ll also need to add these new variables to our **for** loop below, so that they’re added to each row. We can do this as many times as we like.

```
```python
for row in range(len(pixelArt)):
    for pixel in range(len(pixelArt[row])):
        if pixelArt[row][pixel] == 0:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockOrangeType)
        elif pixelArt[row][pixel] == 1:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBlueType)
        elif pixelArt[row][pixel] == 2:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockBrownType)
        elif pixelArt[row][pixel] == 3:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockWhiteType)
        elif pixelArt[row][pixel] == 4:
            mc.setBlock(x, y - row, z +
                        pixel, woolBlock, woolBlockPinkType)
```
```

# ### 04 Drawing a 2D creeper

Now, to create your first piece of pixel art you’ll need to create a list of 1s and 0s in the **pixelArt** list:

```
```python
pixelArt = [
    [1, 1, 1, 1, 1, 1, 1, 1],
    [1, 0, 0, 1, 1, 0, 0, 1],
    [1, 0, 0, 1, 1, 0, 0, 1],
    [1, 1, 1, 0, 0, 1, 1, 1],
    [1, 1, 0, 0, 0, 0, 1, 1],
    [1, 1, 0, 0, 0, 0, 1, 1],
    [1, 1, 0, 1, 1, 0, 1, 1],
    [1, 1, 1, 1, 1, 1, 1, 1]
]
```
```

If you squint, you can make out a Creeper head in the 1s and 0s.

# ### 05 Creating a Steve head – adding more block type variables

Obviously a Creeper is just black and green, but if you’re looking to create something more advanced, you’ll need to add more colour blocks by adding more variables with block IDs and types. Here are the colours we’d need to create a Steve head:

```
```python
#wool is blockID 35
#Orange wool is type 1
woolBlock = 35
```
```

# ## 07 Running your code

Save your **pixelart.py** file in ~/home/minecraft. open Minecraft with the Forge 1.8 profile, create/load a world and type **/python pixelart** to spawn your creation. You can do this as many times as you like to build a new copy of your prefabricated pixel art.■

> **Finding new pixel art**
> If you’re stuck for ideas for your pixel art creation, or you need a little assistance, try Googling for pixel art templates. There are plenty of free templates available, with grid-lines and countable boxes. You can mirror these by counting the rows/columns and adjusting your Python list to match. Our Creeper and Steve heads were 8x8, but you could easily adapt this to 12x12 by adding four more lines of code and appending four more numbers to each row.
> 
> We’d love to see your 2D/3D Minecraft pixel art creations. Pop us a tweet with your best screenshot @linuxusermag and let us know which distro you’re running Minecraft on.