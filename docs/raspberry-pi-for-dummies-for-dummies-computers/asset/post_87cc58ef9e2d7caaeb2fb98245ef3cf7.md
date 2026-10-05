
part of the maze can be visited. There is only one path between any two points in the maze.

An algorithm is a set of rules or a process for solving a particular problem. It is typically performed by a computer, but you could carry out the maze algorithm using paper and pencil, and an eraser to wipe out the walls as you go. Here's how it works:

- 1. You start with the "waffle" you've built, with every cell having four walls.
- 2. You pick a random cell in the maze to start at.
- 3. You look at your current cell's neighbors and make a list of all those that have four walls intact. These are the cells that have not been visited.
- 4. If you found some unvisited neighbors, you pick one at random, knock down the wall between it and your current cell, and move into that cell, making your current cell.
- 5. If your current cell has no unvisited neighbors, you go back one cell in the path you've taken, and make that your current cell.
- 6. Repeat Steps 3 to 5 until you've visited every cell.

## Setting up the variables and lists

To implement this algorithm, you'll use the following variables:

- >> numberOfCells: This is the total number of cells in the maze, which will be SIZE*SIZE.
- >> numberOfVisitedCells: This keeps track of how many cells you've visited. When this is the same as numberOfCells, every cell has been visited and had a wall demolished, and is therefore reachable.
- >> xposition: This remembers your x position as you move through the maze generating it. It's measured in cells, and it starts as a random number between 1 and maze SIZE.
- >> zposition: This remembers your z position as you move through the maze generating it, also measured in cells and also starting as a random number.
- >> cellsVisitedList[] this is a list that stores the path you've taken so that the program can retract its steps. When you set it, you put your starting position into it using the append() list method.
- >> playerx and playerz: These are used to remember the starting position, you can put the player there when the maze has been built.

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

## Creating the functions

There are a number of basic functions you will need for your program:

- * realx(x) and realz(z): Convert coordinates in the maze (measured in cells) into coordinates in the Minecraft world (measured in blocks and offset from the maze's starting point).
- * showMaker(x, y) and hideMaker(x, z): These functions use a gold block to show the program has reached as it builds the maze. It's fun to watch from above and is useful while building and debugging the program.
- * demolish(realx, realz): This knocks down a wall in the maze and takes real x and z coordinates in the Minecraft world as its parameters.
- * testWalls(cellx, cellz): This checks whether the four walls on a cell are intact. If all of them, it returns True. Otherwise it returns False. It uses the command .getBlock(x, y, z), which tells you the blockType at a particular location. You use two signs, as usual, to test whether a block in a position is the same as the MAZE_MATERIAL, which means that there's a wall there.

Add these function definitions at the start of your program, right where you set up the Minecraft module:

```python
def realx(x):
    return MAZE_X + (x*2) - 1

def realz(z):
    return MAZE_Z + (z*2) - 1

def showMaker(x, z):
    mc.setBlock(realx(x), GROUND+1, realz(z), 41) # 41=gold

def hideMaker(x, z):
    mc.setBlock(realx(x), GROUND+1, realz(z), 0)

def demolish(realx, realz):
    mc.setBlocks(realx, GROUND+1, realz, realx,
    HEIGHT+1, realz, 0)

def testAllCells(cellx, cellz):
    if mc.getBlock(realx(cellx)+1, GROUND+1,
    realz(cellz))==MAZE_MATERIAL and mc.getBlock(
    realx(cellx)-1, GROUND+1, realz(cellz))==MAZE_MATERIAL
    and mc.getBlock(realx(cellx), GROUND+1, realz(cellz)+1)==
    MAZE_MATERIAL and mc.getBlock(realx(cellx), GROUND+1,
    realz(cellz)-1)==
    MAZE_MATERIAL:
        return True
    else:
        return False
```

If you found some unvisited neighbors, you pick one at random, knock down the wall between it and your current cell, and move into that cell, making your current cell.

If your current cell has no unvisited neighbors, you go back one cell in the path you've taken, and make that your current cell.

Repeat Steps 3 to 5 until you've visited every cell.

## Creating the loop

Your maze runs until you've visited every cell, so it starts with:

```python
while visitedCells < numberOfCells:
```

You need to check whether your current cell's neighbors have all walls intact. To do that, check each direction in turn:

```python
if len(possibleDirections) != 0:
    directionChosen = random.choice(possibleDirections)
    if directionChosen == "left":
        demolish(realx(xposition)-1, realz(zposition))
        xposition -= 1
    elif directionChosen == "right":
        demolish(realx(xposition)+1, realz(zposition))
        xposition += 1
    elif directionChosen == "up":
        demolish(realx(xposition), realz(zposition)-1)
        zposition -= 1
    elif directionChosen == "down":
        demolish(realx(xposition), realz(zposition)+1)
        zposition += 1
```

If you find a new cell, you need to increase your tally of cells visited by one, and add the new cell to the list. This is also a good time to show the gold block in the cell:

```python
numberOfVisitedCells += 1
cellsVisitedList.append((xposition, zposition))
showMaker(xposition, zposition)
```

If your cell has no unvisited neighbors, you go back to the previous position in the path. This involves taking the last position out of the list:

```python
else:
    retrace = cellsVisitedList.pop()
xposition = retrace[0]
    zposition = retrace[1]
```
