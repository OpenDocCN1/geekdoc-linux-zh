
Change the speed of the moving clouds, by changing their duration in the animate() functions. Remember that there's one animate() function at the start, and one when they reappear at the bottom of the screen.

Increase the amount of time on the clock.

# The final game listing

To help you find your way around creating this program, and provide you with it all in one place, here's the final listing (12-4):

LISTING 12-4: The final Cloudbusting game

+   # Cloudbusting game
# From Raspberry Pi For Dummies 3rd Edn
# By Sean McManus - www.sean.co.uk
# Run with: pgzrun cloudbusting.py

```python
import random

WIDTH = 500
HEIGHT = 500
score = 0
timer = 10
clouds = list()

for i in range(6):
    filename = 'target' + str(i)
    clouds.append(filename)
    this_cloud = clouds[i]
    this_cloud.x = random.randint(int(this_cloud.width / 2), WIDTH - this_cloud.width / 2)
    this_cloud.y = HEIGHT + this_cloud.height
    animate(this_cloud, tween='linear', 
            duration=random.uniform(1, 3), 
            pos=(this_cloud.x + random.randint(10, 100), -200))
```

```python
def draw():
    screen.clear()
    for i in range(6):
        this_cloud = clouds[i]
        this_cloud.draw()
```

```python
screen.draw.text("Score: " + str(score), (2, 2), color="orange")
screen.draw.text("Timer: " + str(timer), (WIDTH - 70, 20), color="orange")
if timer == 0:
    screen.draw.text(str(score), (130, 120), color="white", fontsize=300)
```

```python
def update():
    for i in range(6):
        this_cloud = clouds[i]
        if this_cloud.y < 0 - this_cloud.height:
            this_cloud.y = HEIGHT + this_cloud.height
        if timer > 0:
            this_cloud.x = random.randint(int(this_cloud.width / 2), WIDTH - this_cloud.width / 2)
            this_cloud.image = 'target' + str(i)
        animate(this_cloud, random, tweens='linear', 
                duration=random.uniform(1, 3), 
                pos=(this_cloud.x + random.randint(-10, 100)))
```

```python
def on_mouse_down(pos):
    for i in range(6):
        this_cloud = clouds[i]
        if this_cloud.collidepoint(pos) and timer > 0 
            and this_cloud.image != 'pop':
                this_cloud.image = 'pop'
                sounds.blop.play()
                score += 1
```

```python
def countdown():
    global timer
    timer -= 1
    if timer == 0:
        clock.unschedule(countdown)
        sounds.whoops.play()
```

```python
clock.schedule_interval(countdown, 1)
```

# Exploring Pygame Zero Further

We hope this project has given you a taste for what Pygame Zero can do. As well as supporting mouse clicks, you can use it to detect keypresses, making it possible to make more conventional games with characters moving under keyboard control. As such, it's a good foundation for most types of game.

To find out more, we recommend that you check out the following resources:

- Daniel Pope's blog post announcing Pygame Zero: http://mauveweb.co.uk/posts/2015/05/pygame-zero.html

- The Pygame Zero documentation, including simple examples: http://pygame-zero.readthedocs.io/en/latest

- The Pygame Zero built-in objects list, with information about actors, images, sounds and the clock: http://pygame-zero.readthedocs.io/en/latest/buildins.html

You can also read Sean's book *Mission Python* to see how Pygame Zero can be used as the foundation for a 3D adventure game.

# IN THIS CHAPTER

- » Exploring the Minecraft world
- » Manipulating the Minecraft world in Python
- » Generating a random Minecraft maze in Python

# Chapter 13

# Programming Minecraft with Python

Minecraft appeals to the Lego fan in everyone. It enables you to build immersive 3D worlds from blocks of materials, and it has fired up imaginations to the extent that over 100 million copies have been sold across various platforms, including the PC and Xbox.

A version of Minecraft is available for the Raspberry Pi. It features the Creative mode, where you can build items peacefully without the threat of monster attacks or starvation. The best feature is that you can program it using multiple languages, including Python. This means that you can build a grand palace without having to manually place every block, and you can write programs that invent original new structures for you to room and around, and as you see in this chapter.

The project in this chapter will show you how to use Python to interact with Minecraft.

# Exploring the Minecraft world

Minecraft appeals to the Lego fan in everyone. It enables you to build immersive 3D worlds from blocks of materials, and it has fired up imaginations to the extent that over 100 million copies have been sold across various platforms, including the PC and Xbox.

A version of Minecraft is available for the Raspberry Pi. It features the Creative mode, where you can build items peacefully without the threat of monster attacks or starvation. The best feature is that you can program it using multiple languages, including Python. This means that you can build a grand palace without having to manually place every block, and you can write programs that invent original new structures for you to room and around, and as you see in this chapter.

The project in this chapter will show you how to use Python to interact with Minecraft.

# Moving around

Minecraft is easy to use with two hands — one on the mouse and one on the keyboard. Use the mouse to look around and change direction, sliding left and right to turn, and forward and backward to move. To, use the keys W and S for forward and backward, and A and D to take a sidestep left and right. These keys form a cluster on the keyboard, which makes it easy to switch between.

Your character automatically jumps onto low blocks if you walk into them, but you can deliberately jump by pressing the spacebar.

For the best view of your world, take to the skies by double-tapping the spacebar. When you're flying, hold the spacebar to go higher, and the left Shift to go lower. Double-tap the spacebar to stop flying and drop to the ground. There's no health or damage in this edition of Minecraft, so you can freefall as far as you like.

# Making and breaking things

To break blocks in your world, use the mouse to aim the crosshair at the block you want to destroy, and click and hold the left mouse button. Some blocks are easier to break than others. There's a limit on how far away you can be, so move closer if you can't see chips off the blocks as you attempt to smash them.

The panel at the bottom of the window shows the blocks you can place in the world. (Refer to Figure 13-L) You choose them using the scroll wheel on the mouse or by pressing a number between 1 and 8 to pick one (from left to right). Press E to open your full inventory, and then you can use movement keys (W, A, S, D) to navigate around it or Enter to choose a block — or you can simply click your chosen block with the mouse.

To position a block, right-click where you would like to place it. You can put a block on top of another one only if you can see the top of it, so you might need to fly to make tall structures.
