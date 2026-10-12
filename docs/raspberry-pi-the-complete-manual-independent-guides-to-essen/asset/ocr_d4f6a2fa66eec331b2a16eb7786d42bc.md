# Projects

# Program Minecraft-Pi

# Program
Minecraft-Pi

Learn to program while playing one of the
most popular games in the world today . . .

# What you’ll need. . .

+   *   Raspbian (latest release)
+       www.raspberrypi.org/downloads
+   *   Minecraft-Pi tarball
+       http://pi.minecraft.net/
+   *   Keyboard & mouse
+   *   Internet connection

# Did you know. . .

Minecraft-Pi is based on a very old build 6 of the Redstone Edition of Minecraft. We’ll hope there will be a new version soon!

![](bbox=[0.06, 0.67, 0.44, 0.93])

Below Unlike all other versions of Minecraft, the Pi version encourages you to hack it

Now you’ve got the hang of Minecraft for the Raspberry Pi it’s time to try your first project. Over the next four pages we’ll show you how you can use Python to program Minecraft-Pi to make fun games and projects. We’ll implement a version of Hide & Seek created by Martin O’Hanlon that challenges you to find a block of diamond hidden somewhere within 50 blocks of your current position. The game uses a simple algorithm to test to see how far you are away from the block and it will tell you if you’re getting warmer or colder! Don’t worry if you’re never programmed in Python before. You can copy our code and follow the instructions to take it for a test run. Once you’ve got the hang of it, you can try changing the settings to create your own version of the game.

# Configure the API

**01** To take control of Minecraft-Pi with the Python API you next need to have convenient access to the Python API folder from within the / mcpifolder. This contains all the secret sauce you need to hack your own little games and projects together. The easiest way to do this (and keep the original folder clean in case of problems) is to create a new copy of the folder and its contents into a new folder. To do this open the terminal and type the following:

```
```
cp -r ~/mcpi/api/~/mcpi/~/mcpiminecraft
```
```

Once this is complete we can create a “bootstrap” Python document that connects the API to the game. You can