
## Create a Minecraft Minesweeper game

Use your Raspberry Pi and Python knowledge to code a simple mini-game in Minecraft

### Resources

- **Jessie or Raspbian:**  
  raspberrypi.org/downloads
- **Python:**  
  www.python.org/

You may remember or have even played the classic Minesweeper PC game that originally dates back to the 60s. Over the years it has been bundled with most operating systems, appeared on mobile phones, and even featured as a mini-game variation on Super Mario Bros.

This project will walk you through how to create a simple version in Minecraft: it's Minecraft Minesweeper! You will code a program that sets out an arena of blocks and turns one of these blocks into a mine. To play the game, guide your player around the board. Each time you stand on a block you turn it to gold and collect points, but watch out for the mine as it will end the game and cover you in lava!

### 01 Update and install

To update your Raspberry Pi, open the terminal and type:

```bash
sudo apt-get upgrade
sudo apt-get update
```

The new Raspberry Pi OS image already has Minecraft and Python installed. The Minecraft API which enables you to interact with Minecraft using Python is also pre-installed. If you are using an old OS version, we would highly recommend you downloading and then updating your version to either the most recent Jessie or Raspbian image.

![](img/e016e192a91ffc1a9e474690a590742f_119_0.png)

### 02 Importing the modules

Load up your preferred Python editor and start a new window. You need to import the following modules: import random to calculate and create the random location of the mine, and import time to add pauses and delays to the program. Next, add a further two lines of code: from mcpi import minecraft and mc = minecraft.Minecraft.create(). These create the program link between Minecraft and Python. The mc variable enables you to write “mc” instead of “minecraft.Minecraft.create()".

```python
import random
import time
from mcpi import minecraft
mc = minecraft.Minecraft.create()
```

### 03 Grow some flowers

Using Python to manipulate Minecraft is easy: create the program below to test it is working. Each block has its own ID number, and flowers are 38. The x, y, z = mc.player.getPos() line gets the player’s current position in the world and returns it as a set of coordinates: x, y, z. Now you know where you are standing in the world, blocks can be placed using mc.setBlock(x, y, z, flower). Save your program, open MC and create a new world.

```python
flower = 38
while True:
    x, y, z = mc.player.getPos()
    mc.setBlock(x, y, z, flower)
    time.sleep(1)
```

### 04 Running the code

Reducing the size of the MC window will make it easier for you to see both the code and the program running; switching between too can be frustrating. The Tab key will release the keyboard and mouse from the MC window. Run the Python program and wait for it to load — as you walk around, you’ll drop flowers! Change the ID number in line 1 to change the block type, so instead of flowers, try planting gold, water or even melons.

### 05 Posting a message to the Minecraft world

It is also possible to post messages to the Minecraft world. This is used later in the game to keep the player informed that the game has started and also of their current score. In your previous program add the following line of code under the flower = 38 line, making this line 2: mc.postToChat("I grew some flowers with code"). Now save and run the program by pressing F5 – you will see the message pop up. You can try changing your message, or move to the next step to start the game.

### 06 Create the board

The game takes place on a board created where the player is currently standing, so it is advisable to fly into the air or find a space with flat terrain before running your final program. To create the board you need to find the player’s current location in the world using the code x, y, z = mc.player.getPos(). Then use the mc.setBlocks code in order to place the blocks which make up the board:

```python
mc.setBlocks(x, y-1, z, x+20, y-1, z+20, 58)
```

The number 58 is the ID of the block that is a crafting table. You can increase or decrease the size of the board by changing the +20. In the code example above, the board size is 20 x 20 blocks, which gives you a 400-block arena to play within.

![](img/e016e192a91ffc1a9e474690a590742f_120_0.png)

### Switching to the shell

Switching between the Python Shell and Minecraft window can be frustrating, especially as MC overflies the Python window. The best solution is to half the windows across the screen. (Don’t run MC full-screen as the mouse coordinates are off). Use the Tab key to release the keyboard and mouse from the MC window.

![](img/e016e192a91ffc1a9e474690a590742f_121_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_121_1.png)

Right. Nothing says “game over” quite like a huge eruption of lava

### 07 Creating the mine

In the previous step you found the player’s location on the board. This x, y, z data can be reused to place the mine on the board. The code mine = random.randrange(0, 11, 1) generates a random number between 1 and 10. Combine this with the player’s current x axis position and add the random number to the position – this creates a random mine block on the board.

```python
mine_x = int(x+mine)
mine_y = int(y-1)
mine_z = int(z+mine)
```

Use setBlock to place the mine: mc.setBlock(mine_x, mine_y, mine_z, 58). Using y-1 ensures that the block is placed on the same level as the board and is therefore hidden. The number 58 is the block ID, which you can change if you wish to see where the mine is; this is useful for testing that the rest of the code is working correctly. Remember to change it back before you play!

### 08 Create a score variable

Each second that you remain alive within the game, a point is added to your score. Create a variable to store the current score, setting it to a value of zero at the beginning of the game. Use the postToChat code to announce the score at the beginning of the game. Note that MC cannot print a value to chat, so the score is first converted into a string before it is displayed.

```python
score = 0
mc.postToChat("Score is "+str(score))
time.sleep(10)
```

### 09 Check the player’s position on the board

Next, you need to check the player’s position on the board and see if they are standing on the mine. This uses a while loop to continually check that your player’s position is safe, no mine, else game over. Since the player’s coordinate position is used to build the original board and place the mine, you have to find the player’s position again and store it as a new variable – x1, y1 and z1

```python
while True:
    x1, y1, z1 = mc.player.getTilePos()
```

### 10 One point, please

Now that the player has moved one square they are awarded a point. This is a simple action of adding the value one to the existing score value. This is achieved using score = score + 1. Since it sits inside a loop, it will add one point each time the player moves.

```python
time.sleep(.1)
score = score + 1
```

### 11 The tension increases...

Once you have been awarded a point, the next stage of the game is to check whether the block you are standing on is a safe block or if it is the mine. This uses a conditional to compare the coordinates of the block beneath you – x1, y1-1, z1 – with the mine_x, mine_y, mine_z position of the mine. If they are equal then you are standing on the mine. In the next step you will code the explosion:

```python
if (x1, y1-1, z1) == (mine_x, mine_y, mine_z):
```

### 12 Setting the mine off

In the previous step a conditional checks whether you are standing on the mine or a safe block. If it is the mine then it will explode. To create this, use lava blocks, which will flow and engulf the player. You can use the mc.setBlocks code to set blocks between two points. Lava blocks are affected by gravity, so setting them higher than the player means that the lava flows down over the player.

```python
mc.setBlocks(x-5, y+1, z-5, x+5, y+2, z+5, 10)
```

### Other Minecraft hacks

If you enjoy programming and manipulating Minecraft then there are more great Raspberry Pi-based projects for you to check out. Our expert has a bunch of them at teacead.co.uk/minecraft.htm. The folks behind Adventures in Minecraft have some great guides over at stuttacodoc.com/pyminecraft.html, as well.
