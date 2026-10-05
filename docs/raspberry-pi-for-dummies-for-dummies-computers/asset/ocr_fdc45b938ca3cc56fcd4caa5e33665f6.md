```
if len(possibleDirections) != 0:
    directionChosen=random.choice(possibleDirections)

#knock down wall between cell in direction chosen
if directionChosen == "left":
    demolish(realx(position) - 1, realz(position))
    xposition -= 1

if directionChosen == "right":
    demolish(realx(position) + 1, realz(position))
    xposition += 1

if directionChosen == "up":
    demolish(realx(position), realz(position) - 1)
    zposition -= 1

if directionChosen == "down":
    demolish(realx(position), realz(position) + 1)
    zposition += 1
```

LISTING 13-1: (continued)

numberOfVisitedCells += 1
# after the move, increase number of visited cells
cellsVisitedList.append(xposition, zposition)
showMaker(xposition, zposition)

else: # do this when there are no unvisited neighbors
retrace = cellsVisitedList.pop()
xposition = retrace[0]
zposition = retrace[1]
showMaker(xposition, zposition)

if CEILING == True:
mc.setBlocks(MAZE_X, GROUND+HEIGHT+1, MAZE_2,
MAZE_X+(SIZE*2), GROUND+HEIGHT+1, MAZE_Z+(SIZE*2), 0)

mc.postToChat("Your maze is ready!")
mc.postToChat("Happy exploring!")
mc.player.setTilePos(realx(player), GROUND+1,
realz(player))