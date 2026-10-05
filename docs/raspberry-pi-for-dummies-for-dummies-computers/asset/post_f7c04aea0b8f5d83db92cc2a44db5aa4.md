
In this case, you just want to draw the cloud actor at its current position, so you use

```
cloud.draw()
```

Can you work out how to add another cloud to the program and position it to the left of the first one? Call cloud2, and remember to change its x position and draw it when you've finished. Listing 12-2 shows one answer. You can use a different number for the x position of cloud2. Again, you run this from the command line using pgzrun and the filename of your program:

# LISTING 12-2: Adding a Second Cloud

```
WIDTH = 500
HEIGHT = 500
cloud = Actor('target5')
cloud.x = 250
cloud.y = 250
cloud2 = Actor('target5')
cloud2.x = 80
cloud2.y = 250
ndef draw():
    screen.clear()
    cloud.draw()
    cloud2.draw()
```

# Detecting mouse clicks

Pygame Zero makes it easy to respond to mouse clicks. Add the following function to the end of your existing program. It doesn't matter whether you're using one-cloud or two-cloud program from Listing 12-2:

```
def on_mouse_down(pos):
    if cloud.collidepoint(pos):
        cloud.image = 'pop'
        sounds.blop.play()
```

This function runs when the mouse button is clicked, and stores the position of the mouse pointer in pos, which is called a tuple.

You don't need to know this to Pygame Zero, but if you're curious, a tuple is a sequence a bit like a list. The main differences are that you can't change the items in it, and it's defined using parentheses () instead of using square brackets []. The tuple used in this function contains the x and y values for the mouse pointer.

Using the mouse position stored in pos, we can work out whether the player clicked on the actor. Collision detection is all about working out whether sprite is touching or touching the mouse pointer. It can be tricky to code, but Pygame Zero includes some features built in to do it for you. You can check whether the mouse pointer (pos) is touching the actor using the command together with the collidepoint() function, as shown earlier. If so, you can change the image of the actor to the 'pop' image

```
cloud.image = 'pop'
```

Again, you don't need the file extension of the image.

For detecting mouse clicks also shows how to play a sound: blop is the name of our sound file, minus the extension (.ogg), which Pygame Zero works for itself. The rest of the line that plays the sound would be the same for any sound. You might find that a simple program like this is one template when you're building your programs.

Run the program. Save it to your pi folder cloud3.py and use pgzrun cloud3.py from the command line to run.

When you click the background, nothing happens. When you click the cloud in the center of the screen, you see it change to a "Pop!" image. One thing you might notice is that you can click near, but not, the image and it will register as a hit. That's because an actor is rectangular. The cloud has rounded corners, but the empty spaces in those corners are still part of the rectangular image, as far as collision detection is concerned.

When you're making your own images, try to stretch the image out to a rectangle as much as possible, and trim any unused space from the edges. That helps your collision detection look accurate. With fast-moving images, nobody will notice if the collision detection is slightly off. If your game includes circles, though, the unused corners of the image will also register a hit, which might feel unfair or unrealistic when playing the game.

# Animating your actors

Pygame Zero includes a simple function for animating your actors so that they can move across the screen automatically. This is another way it makes Pygame more accessible for people who have previously used Scratch: Usually, movement is achieved by having a loop that repeatedly changes the x or y position of the image. Pygame Zero handles all complexity for you.

Here's an example of the animate() function:

```
animate(cloud, tween='linear', duration=5, pos= (cloud.x, -200))
```

It breaks down like this:

- Give it the name of the actor you want to animate first
- Tell the type of actor you want to use. This describes whether the actor speeds up or slows down over the course of the animation. You can consult the documentation for a list of options (see the 'Exploring Pygame Zero Further' at the end of this chapter), but we are using 'linear' so that the animation is an even speed.
- The duration is how long the animation will take, measured in seconds.
- The pos is the finishing position. You give it the x and y position in brackets, like this: (x, y). With this motion, you've used the existing position (cloud.x), and set the y position to -200, which is off the top of the screen. As a result, the cloud will drift up the screen until it is no longer visible.

Try this animation by adding the preceding line of code into the section where you set up your cloud actor, in the following snippet. The instruction is in bold. Note that what you see in this example isn't the full program: You need to change the WIDTH and HEIGHT instructions, and the draw() and on_mouse_down(pos) functions from your previous program:

```
cloud = Actor('target5')
cloud.x = 250
cloud.y = 250
animate(cloud, tween='linear', duration=5, pos=(cloud.x, -200))
```

![](img/df9a01bf057d58c2401b5edabd6e8829_261_0.png)

> REMEMBER the second bracket at the end of the new line. One pair of brackets encloses the position, and another goes around everything given to the actor function.

When the program runs, the cloud actor will be set as before, but this time its animation will be started. Each time the draw() function runs, it draws the cloud in its latest position, making it appear to move over the screen.

You can still click the cloud to make it pop, so you have the engine for a basic game here. Next, let's add an element of chance.

# Using random numbers

Chapter 11 shows how you can use the random.randint() function to pick a random integer (whole number). To pick a random floating-point number, you can use random.uniform(a, b). This will return a random number between a and b.

To use these functions, you must first import the random module at the top of your program:

```
import random
```

Now you can use them in your code. For example, to pick a random integer between 1 and 10:

```python
number = random.randint(1, 10)
```

Or to pick a random floating-point number between 0 and 1:

```python
number = random.uniform(0, 1)
```

You can also use these functions within your animation to make it less predictable. For example:

```
animate(cloud, tween='linear', duration=random.uniform(2, 5), pos=(cloud.x + random.randint(-50, 50), -200))
```

This will make the cloud move at a random speed and drift a different horizontal distance each time.

# Adding more clouds

Chapter 11 shows how to create a list to store strings, but you can also use a list to store actors, which means you can have several in your game and manage them using loops. In this game, you'll use six clouds in total. When one goes off the top of the screen, you'll put it back at the bottom again, if there is still time left on the timer.

We'll be building on the ideas and code presented earlier, but you might find it easier to start a new file to make this program, to avoid the risk of overlooking some of the changes we've made.

Listing 12-3 shows the first part of the program.

**LISTING 12-3:** Adding Yet More Clouds

```
import random

WIDTH = 500
HEIGHT = 500
score = 0
timer = 10
clouds = list()

for i in range(6):
    filename = 'target' + str(i)
    clouds.append(Actor(filename))
    this_cloud = clouds[i]
```
