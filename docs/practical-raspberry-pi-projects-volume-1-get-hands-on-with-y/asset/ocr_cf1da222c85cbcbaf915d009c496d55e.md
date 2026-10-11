# BUILD A RASPBERRY PI MINECRAFT CONSOLE

# Full code listing

+   * Import
+   
+   Here we're importing the necessary modules and APIs to program Minecraft. Most importantly are the files in the mcpi folder that we copied earlier

```
```python
from mcpi.minecraft import Minecraft
from mcpi import block
from mcpi.vec3 import Vec3
from time import sleep, time
import random, math
```
```

+   * Locate
+   
+   We connect to Minecraft with the first line, and then we find the player's position and round it up to an integer

```
```python
mc = Minecraft.create()
playerPos = mc.player.getPos()

def roundVec3(vec3):
    return Vec3(int(vec3.x), int(vec3.y), int(vec3.z))
```
```

+   * Range finding
+   
+   Calculate the distance between the player and diamond. This is done in intervals later on in the code, and just compares the co-ordinates of the positions together

```
```python
def distanceBetweenPoints(point1, point2):
    xd = point2.x - point1.x
    yd = point2.y - point1.y
    zd = point2.z - point1.z
    return math.sqrt((xd*xd) + (yd*yd) + (zd*zd))
```
```

+   * Creation
+   
+   Create a random position for the diamond within 50 blocks of the player position that was found earlier

```
```python
def randomBlock():
    randomBlockPos = roundVec3(playerPos)
    randomBlockPos.x = random.randrange(randomBlockPos.x - 50, randomBlockPos.x + 50)
    randomBlockPos.y = random.randrange(randomBlockPos.y - 5, randomBlockPos.y + 5)
    randomBlockPos.z = random.randrange(randomBlockPos.z - 50, randomBlockPos.z + 50)
    return randomBlockPos
```
```

+   * Start
+   
+   This is the main loop that actually starts the game. It asks to get the position of the player to start each loop

```
```python
def main():
    global lastPlayerPos, playerPos
    seeking = True
    lastPlayerPos = playerPos

    randomBlock = random_block()
    mc.setBlock(randomBlockPos, block.DIAMOND_BLOCK)
    mc.postToChat("A diamond has been hidden - go find!")
```
```

+   * Checking
+   
+   We start timing the player with timeStarted, and set the last distance between the player and the block. Now we begin the massive while loop that checks the distance between the changing player position and the fixed diamond. If the player is within two blocks of the diamond, it means they have found the block and it ends the loop

```
```python
    lastDistanceFromBlock = distanceBetweenPoints(randomBlockPos, lastPlayerPos)
    timeStarted = time()
    while seeking:
        playerPos = mc.player.getPos()
        if lastPlayerPos != playerPos:
            distanceFromBlock = distanceBetweenPoints(randomBlockPos, playerPos)
            if distanceFromBlock < 2:
                seeking = False
        else:
            if distanceFromBlock < lastDistanceFromBlock:
                mc.postToChat("Warmer  " + str(int(distanceFromBlock)) + " blocks away")
            if distanceFromBlock > lastDistanceFromBlock:
                mc.postToChat("Colder  " + str(int(distanceFromBlock)) + " blocks away")
            
        lastDistanceFromBlock = distanceFromBlock
        sleep(2)
```
```

+   * Message writing
+   
+   If you are two or more blocks away from the diamond, it will tell you whether you're nearer or farther away than your last position check. It does this by comparing the last and new position distance - it's the same, a quirk in Python means it says you're colder. Once it's done this, it saves your current position as the last position

+   * Success
+   
+   It takes a two-second break before updating the next position using the sleep function. If the loop has been broken, it tallies up your time and lets you know how long it was before you found the diamond. Finally, the last bit then tells Python to start the script at the main function

```
```python
    timeTaken = time() - timeStarted
    mc.postToChat("Well done - " + str(int(timeTaken)) + " seconds to find the diamond!")

if __name__ == "__main__":
    main()
```
```