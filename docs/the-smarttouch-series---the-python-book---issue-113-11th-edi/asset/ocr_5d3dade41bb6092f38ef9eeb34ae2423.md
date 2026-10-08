# Create with Python

# Quick tip

Could we take things to the next level and create a four-player version of Pong, with a paddle on every side? It would be utter madness, but it sounds fun!

```
import pygame
BLACK = (0,0,0)
class Paddle(pygame.sprite.Sprite):
    def __init__(self, color, width, height):
        super().__init__()
        self.image = pygame.Surface([width, height])
        self.image.fill(BLACK)
        self.image.set_colorkey(BLACK)
        pygame.draw.rect(self.image, color, [0, 0, width, height])
        self.rect = self.image.get_rect()
```

In our first class we’re setting the basic parameters of height, width and colour, as well as the shape. There’s not much to it, because we’re inheriting pygame.sprite class and building upon that. We don’t, therefore, have to specify what a rectangle is or how to draw one.

To control the movement of our paddles, we’ll need a couple of methods: one for the x-axis and another for the y-axis. Keeping in mind a pixel check to ensure they never go off the screen:

```
def moveUp(self, pixels):
    self.rect.y -= pixels
    if self.rect.y < 0:
        self.rect.y = 0
```

# Taking Pong to the next level

With Pong having been around for over 40 years, we’ve seen many iterations of what is essentially a basic game. Once our PyGame version of the game is fully functional, perhaps we could consider what steps we might take to improve our game? On the easier end of the spectrum we could change the colour scheme from black and white to something more contemporary. When Pong was first released, black and white were the only options available. By the time the Atari came out there were 128 colours in the PAL format. Eight-bit consoles introduced 256 colours, and we’re now literally in the billions. Our game is designed with a VGA resolution, so if we were sticking to those retro/vintage aesthetics we’d only have 75 colours available to us. Try changing your Pong game to blue and yellow, for example. What effect would changing the frame rate have on the game? Does increasing or decreasing it affect gameplay? Could we implement a momentary speedup when the ball hits a wall surface, and a temporary slowdown when the ball bounces off a paddle? That might provide a dramatic special effect. Likewise, we could change the speed of the ball itself.

To make the game difficult, if we were to introduce ‘levels’ we might want to set the paddles to a smaller size. There’s to make things go completely wrong so we could change the angles that balls bounce off walls, or even introduce more balls by spawning more objects from the ball class.

![](bbox=[0.24, 0.74, 0.55, 0.91])

![](bbox=[0.58, 0.11, 0.89, 0.33])

Above Pong with working paddles and bouncing ball.

```
def moveDown(self, pixels):
    self.rect.y += pixels
    if self.rect.y > 400:
        self.rect.y = 400
```

To implement our new class into our game, switch back to pong.py and import it as we would any other module, by adding from paddle import Paddle to the top of the code.

Creating instances of the paddle class is as simple as creating objects. By inserting the code shown below somewhere after defining our window, we’re able to create two paddles: one for player A and the other for player B.

```
paddleA = Paddle(WHITE, 10, 100)
paddleA.rect.x = 20
paddleA.rect.y = 200

paddleB = Paddle(WHITE, 10, 100)
paddleB.rect.x = 670
paddleB.rect.y = 200
```

Immediately after that we’ll want to create a list of all the sprites we’re using, including these two paddles:

```
all_sprites_list = pygame.sprite.Group()
all_sprites_list.add(paddleA)
all_sprites_list.add(paddleB)
```

When we introduce additional sprites later we’ll add them to this list. To ensure our sprites are drawn, we’ll then call this list right before we flip (draw) our screen, with all_sprites_list.draw(screen) .

# A good paddling

The final step of implementing our paddles class is setting up an event handler, to monitor for key presses. If player A is using S and W, and player B is using Up and Down on the keyboard, we’ll need to add the following to our main program loop. carryon:

```
keys = pygame.key.get_pressed()
    if keys[pygame.K_w]:
        paddleA.moveUp(5)
    if keys[pygame.K_s]:
        paddleA.moveDown(5)
    if keys[pygame.K_UP]:
        paddleB.moveUp(5)
    if keys[pygame.K_DOWN]:
        paddleB.moveDown(5)
```