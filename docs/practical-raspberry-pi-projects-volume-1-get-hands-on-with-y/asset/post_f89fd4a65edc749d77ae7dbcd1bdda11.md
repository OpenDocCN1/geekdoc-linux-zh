
# HARDWARE

## Mod your Minecraft

Here is some example code, and explanations for it, so that you can learn how to program in Python and mod Minecraft Pi.

We program *Minecraft* to react in Python using the API that comes with *Minecraft: Pi Edition* – it’s what we moved to the home folder earlier on. Now’s a good time to test it – we can do this remotely via SSH. Just `cd` into the Minecraft folder in the home directory we made, and use *nano* `test.py` to create our test file. Add the following:

```python
from mcpy.minecraft import Minecraft
from mcpy import block
from mcpy.vec3 import Vec3
mc = Minecraft.create()
mc.postToChat("Hello, Minecraft!")
```

Save it, and then run it with:

```bash
$ python test.py
```

"Hello, Minecraft!" should pop up on-screen. The code imports the *Minecraft* function from the files we moved earlier, which allows us to actually use Python to interact with *Minecraft*, along with the various other functions and modules imported. We then create the *mc* instance that will allow us to actually post to *Minecraft* using the *postToChat* function. There are many ways you can interact with *Minecraft* in this way – placing blocks that follow the player, creating entire structures and giving them random properties as they’re spawned as well. There are very few limits to what you can do with the Python code, and you can check out more projects here: **https://mcppy.wordpress.com**.

On the next page, we have a full listing for a hide and seek game that expands on the kind of code we’re using here, where the player must find a diamond hidden in the level, with the game telling you whether you’re hotter or colder. You can write it out from scratch or download it to your Pi using the following commands:

```bash
$ wget http://www.linuxuser.co.uk/tutorialfiles/Issue134/ProgramMinecraftPi.zip
$ unzip ProgramMinecraftPi.zip
$ cp Program_MinecraftPi/hide_and_Seek.py ~/minecraft
```

Check out the annotations to the right to see how it works.

## We program Minecraft to react in Python using the API that comes with Minecraft Pi – it’s what we moved to the home folder earlier

![](img/a1548a579bd09ff29b2b92de3f565e63_65_0.png)

# BUILD A RASPBERRY PI MINECRAFT CONSOLE

## Full code listing

- **Import**

    Here we're importing the necessary modules and APIs to program Minecraft. Most importantly are the files in the `mcpi` folder that we copied earlier.

    ```python
    from mcpi.minecraft import Minecraft
    from mcpi import block
    from mcpi.vec3 import Vec3
    from time import sleep, time
    import random, math
    ```

- **Locate**

    We connect to Minecraft with the first line, and then we find the player's position and round it up to an integer.

    ```python
    mc = Minecraft.create()
    playerPos = mc.player.getPos()

    def roundVec3(vec3):
        return Vec3(int(vec3.x), int(vec3.y), int(vec3.z))
    ```

- **Range finding**

    Calculate the distance between the player and diamond. This is done in intervals later on in the code, and just compares the co-ordinates of the positions together.

    ```python
    def distanceBetweenPoints(point1, point2):
        xd = point2.x - point1.x
        yd = point2.y - point1.y
        zd = point2.z - point1.z
        return math.sqrt((xd*xd) + (yd*yd) + (zd*zd))
    ```

- **Creation**

    Create a random position for the diamond within 50 blocks of the player position that was found earlier.

    ```python
    def randomBlock():
        randomBlockPos = roundVec3(playerPos)
        randomBlockPos.x = random.randrange(randomBlockPos.x - 50, randomBlockPos.x + 50)
        randomBlockPos.y = random.randrange(randomBlockPos.y - 5, randomBlockPos.y + 5)
        randomBlockPos.z = random.randrange(randomBlockPos.z - 50, randomBlockPos.z + 50)
        return randomBlockPos
    ```

- **Start**

    This is the main loop that actually starts the game. It asks to get the position of the player to start each loop.

    ```python
    def main():
        global lastPlayerPos, playerPos
        seeking = True
        lastPlayerPos = playerPos

        randomBlockPos = randomBlock()
        mc.setBlock(randomBlockPos, block.DIAMOND_BLOCK)
        mc.postToChat("A diamond has been hidden - go find!")
    ```

- **Checking**

    We start timing the player with `timeStarted`, and set the last distance between the player and the block. Now we begin the massive `while` loop that checks the distance between the changing player position and the fixed diamond. If the player is within two blocks of the diamond, it means they have found the block and it ends the loop.

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

- **Message writing**

    If you are two or more blocks away from the diamond, it will tell you whether you're nearer or farther away than your last position check. It does this by comparing the last and new position distance - it's the same, a quirk in Python means it says you're colder. Once it's done this, it saves your current position as the last position.

- **Success**

    It takes a two-second break before updating the next position using the `sleep` function. If the loop has been broken, it tallies up your time and lets you know how long it was before you found the diamond. Finally, the last bit then tells Python to start the script at the `main` function.

    ```python
    timeTaken = time() - timeStarted
    mc.postToChat("Well done - " + str(int(timeTaken)) + " seconds to find the diamond!")

    if __name__ == "__main__":
        main()
    ```

# **HARDWARE**

![](img/a1548a579bd09ff29b2b92de3f565e63_67_0.png)

**Camera**
48 Raspberry Pi Cameras make up Bullet Pi, with each one sitting in the lower half of each piece of the frame composing the ring.

**Ring**
Bullet Pi uses a ring setup so that you can rotate around a subject frozen in time once the photos are stitched together.

**Cables**
About half a kilometer of network cable was used to build Bullet Pi - the PiFace modules were a godsend during debugging.

**Frame**
While the shots for each set of Bullet Pi images can be adjusted, they're levelled with a custom laser-cut frame.

**PiFace**
The Control and Display modules have an LED screen for two 16-character lines, five control buttons, a navigation switch and IR receiver.

## Components list

- 48 Raspberry Pi Model Bs
- 48 Raspberry Pi Cameras
- 48 PiFace Control and Display modules
- 48 NOOBS SD cards
- 48 5V PSUs
- 500m of network cable
- 2 x 24 port switches
- Wireless router

![](img/a1548a579bd09ff29b2b92de3f565e63_67_1.png)

*Above Many people wondered if Andrew and the team were building a Large Hadron Collider when the first few photos were teased online*

*Left Liz Tu-ton, head of communications at the Raspberry Pi Foundation, tests out Bullet Pi at the Manchester Raspberry Jam in 2013*

# **How I made:**

## Bullet Pi

![](img/a1548a579bd09ff29b2b92de3f565e63_68_0.png)

**Freeze time by chaining 48 Raspberry Pis**

**What inspired you to create Bullet Pi?**

So I'd seen *The Matrix* and also a BBC programme called *Supernatural*. The Unseen Powers jumping out of the water, freeze time, and then spun around so you saw the water drops, and I thought that was a really amazing effect. And re-doing how it was done, it was with a whole array of cameras and it seemed quite simple. So I had the Raspberry Pi and a couple of cameras sat on my desk, and it was sort of like, ‘Well, if it seems that simple, then surely if I just got a whole load of Raspberry Pi and cameras – and they're not that expensive – why shouldn't we just be able to build it?’

It was one of those moments where you think it should work but you don't actually know. So what I did was buy four cameras and I tried it, and that looked like it would work – it gave us a timeslapse glimpse that we could do it.

**So it was a good concept test?**

Yeah, but even so it wasn't conclusive – it just told us it's possibly likely but we still didn't actually know. So then it was just a case of buying a few more cameras. You get to the stage where all you can think is, ‘Right, let's go for it. Let's have a full set of 48 cameras and just build it.' It was only really when we got the first set of images out, and then stitched that together, that you could see having a whole load of cameras and firing them at once is pretty much all we needed. It was one of those things where 'Wouldn't it be cool if...' became 'You know, we might be able to...’ and then ‘Oh, we've done this!'

**That's where the best Pi projects come from! So how do you set it up?**

It's gone through a few iterations and, as we've tried it, we've made a few refinements. In the latest setup, we've got all the Pis booted into Raspbian and, on boot, they run a little Python script we've got. We've fitted them to so many Pi's got a PiFace Control and Display module with using buttons – it just drives a menu. So that lets us know that all the Pis have booted up, because if you've got 48 Pis and a network cable comes out, it's tricky to find out which one when they all look the same. So that was really just a luxury in terms of helping to debug, and it also means we can reconfigure the array if we wanted to do a lateral version.

**What are you using to stitch the images?**

That's FFmpeg. We've had to do some things with the alignment just to get a smooth video out, because some of the cameras are at slightly different angles and if you don't then the picture tends to go up and down. Basically we take a set of images with each calibration and work out whether there's a positive or a negative offset to each frame, then when we stitch them together we chop off the top and the bottom and just use the middle of the frame.

**Is that handled by a script or do you do it manually once you've taken the shots?**

We actually trigger it as two points, but there's nothing to stop the two scripts being put together in the command line and all being run at once. The only reason we run it twice is that the script to stitch the images together takes about a minute and sometimes, if you take an image and then the person you're taking the image of says 'I don't like that, let's do it again', it saves cancelling something that's already started. So for logical reasons we run it as two separate operations but effectively they're just two commands: one command to take the images and one command to stitch the images, and there's nothing to stop it all being automated. You could put a pressure pad in there so that when people stood in the middle of the bullet rig it would automatically trigger.

**Is the PiFace a crucial component or was it just something you wanted to use?**

It was a luxury for us that we had it kicking around. It turned out to save us time when we were debugging. It's not essential – you can build it without – but it made life much easier. We've also tried it in other configurations, and when you put it in other configurations, just being able to go through a menu on each Pi and then see where it is in the sequence is a lot easier if you can actually relate to the Pi that we're to look at what number, rather than having to look at what number it is; SSI into it and set a file.

**What configurations have you tried?**

We tried semicircles and we've tried straight lines, and that way you get the effect of the camera panning along as opposed to spinning around a point. We've got future plans, which involve taking it into more wild and wacky situations. So far we've learned from the examples we've done inside, and then as we've got the setup faster, and more automated and got all the little tweaks and experiences from it, we're becoming more ambitious with it. There are definite plans to mount it on impressive things outside and get some sports photography going with it. There's one person who actually booked us for their wedding after they'd seen it – they wanted photographs of their guests and it would be different, something unusual to capture the guests in a 360-degree spin. That's the other nice thing about it – community. You put something online and suddenly it goes off in a different direction.

![](img/a1548a579bd09ff29b2b92de3f565e63_68_1.png)

**Andrew Robinson** is an honorary research fellow of the University of Manchester, and the creator of PiFace Control and Display (learn more at piface.org.uk)

**Like it?**

If you're thinking of using PiFace Control and Display in one of your own projects, check out the excellent tutorials provided by the team over at: piface.org.uk/guides

**Further reading**

To see Bullet Pi in action, check out this video from its first outing at the Manchester Raspberry Jam in 2018: bit.ly/twoPi

> **We've got future plans, which involve taking it into more wild and wacky situations**
