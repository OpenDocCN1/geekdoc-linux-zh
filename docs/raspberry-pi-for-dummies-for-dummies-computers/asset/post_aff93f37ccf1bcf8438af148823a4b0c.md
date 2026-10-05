
## TABLE 13-1
## Materials in Minecraft: Pi Edition

| BlockTypeId | Block Type |
| :--- | :--- |
| 0 | Air |
| 1 | Stone |
| 2 | Grass |
| 3 | Dirt |
| 5 | Wooden plank |
| 8 | Water |
| 10 | Lava |
| 12 | Sand |
| 20 | Glass brick |
| 24 | Sandstone |
| 41 | Gold brick |
| 45 | Brick |
| 47 | Bookshelf |
| 53 | Wooden stairs |
| 57 | Diamond block |
| 64 | Wooden door |
| 81 | Cactus |

If your Minecraft window goes black when you try this, you've probably built the walls on top of the player. Reposition the player using code to get the view back.

> The # symbol represents a comment that's there only as a reminder for you. computer ignores anything on the same line after the #.

Although players can have coordinate positions with decimal portions (such as 1.7), when you place a block, its position is rounded down to the nearest whole number.

![](img/df9a01bf057d58c2401b5edabd6e8829_279_0.png)

## Stopping the player from changing the world

We know you wouldn't cheat, but there's no fun in a maze that you accidentally hit your way through, is there? To stop players from being able to destroy or place blocks in the world, using the following:

```
mc.setting("world.immutable", True)
```

The word *immutable* is often used in programming, and it means "unchangeable.".

## Setting the maze parameters

Now that you know how to place blocks in the world and use the air block to remove them again, you're ready to start making the maze program. In this program, you'll use a number of constants to keep track of important information about the maze. *Constants* are just variables that you decide not to change the values of as program is running, so their values are always the same. It's conventional to use uppercase letters for the names of constants to signal your intent to others reading the program, and to remind yourself that you're not supposed to be letting the program change these values. Replacing numbers in your program with constants makes it easier to customize your program, but also makes it easier to read your program and understand what different numbers represent.

![](img/df9a01bf057d58c2401b5edabd6e8829_280_0.png)

Variable names are case sensitive, so Python would think **SIZE** and **size** were two different variables. You'd be mad to use both in the same program, though!

The program starts by setting up these constants:

```
SIZE = 10
HEIGHT = 2
MAZE_X = 0
GROUND = 0
MAZE_Z = 0
MAZE_MATERIAL = 1 #stone
GROUND_MATERIAL = 2 #grass
CEILING = False
```

To build the maze, you start with a grid of walls with 1-block spaces (cells) between them, which looks a bit like a waffle. (See Figure 13–2) Each cell with four walls, and the program knocks down walls to create paths between them and build the maze. The maze is square, and its **SIZE** is measured in cells. A maze with a **SIZE** of 10 will have 10 cells in the x and z dimensions, but will occupy double space in the Minecraft world (that is, 20 blocks by 20) because there is a 1-block wall between each cell. This becomes clearer as you start to build the maze. We've tried mazes as big as 40, but they take some time to build and ages to explore. Ten is big enough for now.

CHAPTER 13 Programming Minecraft with Python 265

![](img/df9a01bf057d58c2401b5edabd6e8829_281_0.png)

The HEIGHT is how many blocks tall the maze walls are. We chose 2 because a value of 1 means that the player can just walk over the maze. (The player automatically steps onto blocks 1 unit height.) Higher values obscure any mountains in the distance that can otherwise give a nice visual hint to the player.

The constants MAZE_X, GROUND, and MAZE_Z are used for the starting coordinates of the maze. The MAZE_MATERIAL is stone (1), and the GROUND_MATERIAL is grass (2). We've added an option for a ceiling, to stop players from flying out of the top of the maze, but we've turned it off for now so that you can freely explore the maze as you are building it.

The program stops with an error if there isn't enough room for all of the maze in your world. In that case, you can try using a smaller maze, moving the MAZE_X and MAZE_Z coordinates, or use a different world.

A maze of bookshelves (MAZE_MATERIAL=47) looks great!

## Laying the foundations

One of the first things you need to do before you build the maze is make sure that you're building on solid land. Because Minecraft worlds are dynamically generated, you might find that, otherwise, you're building a maze inside a mountain or in the sea.

You'll need to clear, as well as the area the maze will occupy, an area of ten blocks all the way around it so that players can approach easily and walk around the outside of it. First you clear the area by filling it with air blocks, which will wipe out anything else in that space. Then you add the floor, a layer of blocks made of the ground material.

The maze occupies a ground space measured in blocks from MAZE_X to MAZE_X+(SIZE+2), and from MAZE_Z to MAZE_Z+(SIZE+2). (Remember: * is the symbol for multiplication.) The number of blocks is twice the number of cells (SIZE) because each cell has a wall on its right and below it. The middle of the maze in the Minecraft world is MAZE_X_SIZE, MAZE_Z_SIZE.

You need to clear 10 blocks in each direction. The following code clears everything as in 150 above the ground level of the maze, to stop the risk of any remaining blocks falling from the sky into the maze, and then lays the floor:

```
mcBlocks(MAZE_X-10, GROUND, MAZE_Z-10,
MAZE_X+(SIZE+2)+10, GROUND+150, MAZE_Z+(SIZE+2)+10, 0)
mcBlocks(MAZE_X-10, GROUND, MAZE_Z-10,
MAZE_X+(SIZE+2)+10, MAZE_Z+(SIZE+2)+10,
GROUND_MATERIAL)
```

We recommend adding a block to indicate the starting corner of the maze (where MAZE_X and MAZE_Z are). You will find it useful when writing and debugging the program, it will enable you to tell which way around the maze is as you fly around it. To do so, use the following:

```
mcBlock(MAZE_X, GROUND+HEIGHT+1, MAZE_Z,
MAZE_MATERIAL)
```

Put your player character above the middle of the maze, too, so you can watch it being built by looking down, as follows — if you're not flying, you'll fall onto the maze wall, but you can just fly up again:

```
mc.player.setTilePos(MAZE_X+SIZE, GROUND+25, MAZE_Z+SIZE)
```

## Placing the maze walls

To make the waffle-like grid, use the following code:

```
for line in range(0, (SIZE+1)*2, 2):
  mcBlocks(MAZE_X+line, GROUND+1, MAZE_Z,
  MAZE_X+line, GROUND+HEIGHT, MAZE_Z+(SIZE+2),
  MAZE_MATERIAL)
```

```
mc.setBlocks(MAZE_X, GROUND+1, MAZE_Zline, 
MAZE_X+(SIZE+2), GROUND+HEIGHT, MAZE_Zline, 
MAZE_MATERIAL)
```

The loop gives the variable line values of even numbers starting at 0 and finishing at SIZE+2, in turn. Note that you have to add 1 to SIZE doubling the loop, because the range function doesn't include the last number in the sequence. If you use range(1, 10), for example, you get the numbers 1 to 9. The 2 at the end of the range function is the step size, and it adds 2 each time it goes around the loop, and only gives you the even numbers. This means you leave a gap for two walls between each wall. Each time around the loop, it uses cuboids to draw two walls that stretch across the maze from edge to edge in the x and z dimensions. It doesn't matter that the same block is set twice where those lines intersect. You build the wall starting at GROUND+1, so the grass is underneath when you knock down the walls to make paths.

![](img/df9a01bf057d58c2401b5edabd6e8829_283_0.png)

You should have a grid that looks like Figure 13-3.

FIGURE 13-3:
Your grid in Minecraft.

![](img/df9a01bf057d58c2401b5edabd6e8829_283_1.png)

## Understanding the maze algorithm

Before you dig into the code that turns your waffle into a maze, let us tell you how it works. You're going to make what is known as a perfect maze (that's a technical term, not us bragging); That means there are no loops in it and every

268 PART 4 Programming the Raspberry Pi
