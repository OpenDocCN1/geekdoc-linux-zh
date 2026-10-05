When an algorithm like this is implemented (it's called a depth-first maze generation algorithm), it often requires a list or similar data structure to store the locations of walls. You don't need that, because you have actual walls in Minecraft you can look at. The game world stores your maze, if you

The following code sets up your variables:

```
numberOfCells = SIZE * SIZE
numberOfVisitedCells = 1 # for the one you start in
cellsVisitedList = []

xposition = random.randint(1, SIZE)
zposition = random.randint(1, SIZE)
playerx = xposition
playery = zposition
showMaker(xposition, zposition)
# see the next section, "Creating the functions"
cellsVisitedList.append(xposition, zposition)
```

# Creating the functions

There are a number of basic functions you will need for your program:

+   * realx(x) and realz(z): Convert coordinates in the maze (measured in cells) into coordinates in the Minecraft world (measured in blocks and offset from the maze's starting point).

+   * showMaker(x, y) and hideMaker(x, z): These functions use a gold block to show the program has reached as it builds the maze. It's fun to watch from above and is useful while building and debugging the program.

+   * demolish(realx, realz): This knocks down a wall in the maze and takes real x and z coordinates in the Minecraft world as its parameters.

+   * testWalls(cellx, cellz): This checks whether the four walls on a cell are intact. If all of them, it returns True. Otherwise it returns False. It uses the command .getBlock(x, y, z), which tells you the blockType at a particular location. You use two signs, as usual, to test whether a block in a position is the same as the MAZE_MATERIAL, which means that there's a wall there.

Add these function definitions at the start of your program, right where you set up the Minecraft module:

270 PART 4 Programming the Raspberry Pi