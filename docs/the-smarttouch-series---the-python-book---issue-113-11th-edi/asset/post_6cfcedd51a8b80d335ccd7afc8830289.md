
## Win, lose or draw?

We'll probably need to consider adding a win and lose state to our game, so that our player experiences some closure by either winning or losing the game.

We already implemented collision detection in our Move() function, so the game freezes when Pac-Man collides with a ghost. However, nothing is currently communicated to the player. Look for the following code and insert a message. You'll see in this example we've printed “Game over”:

```python
for point, course in ghosts:
    if abs(pacman - point) < 20:
        print("Game Over!")
        return
```

```python
if state["score"] == 160:
    print("You Win!")
```

We'll also need a way for players to win the game. For that, we'll need to implement a win state. Perhaps code the writer turtle to print You Won! when Pac-Man has collected all the dots, using a conditional statement, checking for the score to hit 160, which is the maximum number of dots in this level. One way would be to add the following code toward the bottom of the Move() function:

![](img/e016e192a91ffc1a9e474690a590742f_106_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_106_1.png)

Above *Type* in the final few lines of code, before launching the game.

In this function we're drawing the scores first, then we're checking if a movement is valid before allowing it. The second **if** statement is what controls the eating of dots. If we wanted to take things a step further and introduce an animation, sound effect or other things we would introduce it after **square(x,y)**. Try adding **print("much")** as an example.

```python
def change(x, y):
    if valid(pacman + vector(x, y)):
        aim.x = x
        aim.y = y
```

Movement is all well and good, but we'll need to be able to change the direction our Pac-Man is aiming in. We'll start to seeing if that direction is valid, thanks to our previous function, then we'll go ahead and switch the x and y accordingly:

Our last aim is for the floor calculation, which takes into consideration the offset we made earlier:

```python
def floor(value, size, offset=200):
    return float(((value + offset) // size) * size - offset)
```

With this we can work out the floor value given its size and offset. To explain the floor function we can use a number line diagram:

```
-220      0    100   200
<-===|=====|===|=y--|-z-->
```

The number line shown has offset 200 denoted by the left-hand tick mark at -200 and size 100 denoted by the tick marks at -100, 0, 100, and 200. The floor of a value is the left-hand tick mark of the range where it lies. So for the points show above: floor(x) is -200, floor(y) is 0 and floor(z) is 100. Some examples would be **floor(10, 100) = 0.0** , **floor(120, 100) = 100.0** , **floor(-10, 100) = -100.0** , **floor(-150, 100) = -200.0** , **floor(50, 167) = -33.0** .

And finally, we can get our game going, we'll need to set a resolution, hide the Turtles, write the score, listen for keyboard presses (we're using lambdas for this) and monitor the up, down, left, and right keys for our aim changes. We'll then draw the world, start the move function and we're done!

```python
setup(420, 420, 370, 0)
hideturtle()
tracer(False)
writer.goto(160, 160)
writer.color('white')
writer.write(state['score'])
listen()
onkey(lambda: change(5, 0), "Right")
onkey(lambda: change(-5, 0), "Left")
onkey(lambda: change(0, 5), "Up")
onkey(lambda: change(0, -5), "Down")
world()
move()
done()
```

Our version of Pac-Man is pretty basic, utilising 2D vector graphics and Python's turtle graphics to draw shapes and dots on our screen. This art style is very much in-line with the look and feel of the original incarnation of the game in the 1980. This simplistic artistic direction also meant we were able to code an entire game in a magazine article.

However, programming techniques and computers have moved on incredibly since the time of the first Pac-Man release and if we wanted to take things a step further we could introduce graphical sprites into our game. For instance, we might want a more accurate representation of our ghost antagonists in full colour, with features such as eyes.

Repil user Anurag Gouda has developed a relatively simple solution to take our Python game to the next level, by introducing real sprites. A sample of his code can be found at https://repl.it/tak/share/Pacman/12194 which is fully forkable. Replit is an online IDE (Integrated Development Environment) that enables you to code Python on even the most basic of machines, using cloud resources instead of your local hardware. All you need is an Internet connection. Using a fork of Anurag's code on Replit, you can code a visual Pac-Man in the cloud – fancy!

> **Quick tip**
> Credit to Grant Jenks of Free Python Games for the code reference. We wouldn't have been able to create a vector graphics based Pac-Man game, or indeed describe 'flooring' without his instruction.

## Revisit the arcade classic

### Pong in Python

Calvin Robinson takes us through creating a contemporary homage to Pong – considered by many to be the very first arcade game.

This series of building retro games in Python has so far seen us coding a lunar landing space module (LXF262), a side-scrolling platformer (LXF263), the famous pellet-munching, ghost-chasing Pac-Man (page 104), and in this tutorial we’re going to develop our own version of Pong! To many, Pong is the original arcade game. It’s certainly the first video game to become a commercial success. Released for arcades in 1972 and for the home in 1975, Pong has gained popularity worldwide and is now permanently memorialised in the Smithsonian Institute in Washington, DC. Developed and self-published by Atari, Pong is a 2D table tennis simulation with arguably the most simplistic game design imaginable, while managing to achieve an incredibly addictive gaming experience.

### What gameplay?

Gameplay mechanics in Pong are quite simple. It’s essentially ping-pong seen from a basic bird’s-eye view. The game makes use of vector graphics to display a rectangular shape for the players’ pads and a square (or rough circle, depending on the processing power) for the ball.

In single-player mode, the player moves one paddle and the computer acts as a non-player character, controlling the second. The idea is to get the ball to pass the opponent’s paddle on their side of the screen. You earn a point for each time the opponent misses a rally. Atari’s Home Pong console was set up for two-player mode, with a paddle for each player. That’s the version we’re going to create today. Since we don’t have hardware and we’re programming this entirely in Python, we’ll give each player two keys on either side of the keyboard: one for up, one for down.

![](img/e016e192a91ffc1a9e474690a590742f_107_0.png)

Python offers us an accessible programming language with straightforward syntax. It’s the perfect language for playing around with vector-based video games. Let’s go!

### Ping-pong Python

Without getting into any debates between version 2 versus version 3, we’ll be using Python 3 for this tutorial. If you’re running a Debian based Linux distro you can install Python in Terminal with the command `sudo apt-get install python3` after a quick update with `sudo apt-get update`, of course. We’ll also be taking advantage of a vector graphics module `linuxformat.py` from last issue. This can be found on the disc, or via the source code link on our Archives page at `www.linuxformat.com/archives`. Once downloaded or copied, ensure `linuxformat.py` is saved in the same directory as the rest of the files we create in this tutorial.

Now that Python 3 is installed we can create a new Python file. Using your favourite text editor create an empty file and save it in the same folder as your `linuxformat.py`, which we’ll be using as a reference module for vector graphics. To create the file you can use `touch pong.py` followed by `nano pong.py`, or open it directly through the Python IDE.

We’re going to take advantage of the PyGame toolset for this project. PyGame is a useful module designed to assist with, as the name would suggest, the development of games in Python. PyGame includes a sprite class with shapes such as the rectangle, which we’ll certainly make use of. To install PyGame use `pip` in command line: `pip3 install pygame` should cover it. Remember to use `pip3` to install modules for Python 3, rather than just `pip`, which can get messy with multiple installations of Python on a single machine.

When it comes to programming, there’s no point re-inventing the wheel every time. Start off by importing the pygame module and initialising the game engine:

```python
import pygame
pygame.init()
```

Let’s declare those constant ‘variables’ and define the
