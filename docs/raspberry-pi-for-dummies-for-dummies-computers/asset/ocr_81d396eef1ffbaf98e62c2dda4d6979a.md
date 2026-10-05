```
mc.setting("world.immutable", True)
```

The word *immutable* is often used in programming, and it means "unchangeable.".

# Setting the maze parameters

Now that you know how to place blocks in the world and use the air block to remove them again, you're ready to start making the maze program. In this program, you'll use a number of constants to keep track of important information about the maze. *Constants* are just variables that you decide not to change the values of as program is running, so their values are always the same. It's conventional to use uppercase letters for the names of constants to signal your intent to others reading the program, and to remind yourself that you're not supposed to be letting the program change these values. Replacing numbers in your program with constants makes it easier to customize your program, but also makes it easier to read your program and understand what different numbers represent.

![](bbox=[0.176, 0.433, 0.237, 0.493])

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