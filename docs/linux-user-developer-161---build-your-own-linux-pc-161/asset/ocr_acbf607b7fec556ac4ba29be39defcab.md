# Tutorial

Right Our modular,
PROC-based code
means you can
easily add new
modules – another
power-up, for
example – to mix up
t core gameplay

| Score | 148 |
| Level | 2 |

![](bbox=[0.185, 0.125, 0.915, 0.385])

+   07 Update the power-up lines 099 - 137
The updatePowerUp procedure checks to see if we
already have a power-up on-screen, and if there's not 1-in-
200 chance that one be created. The first power-up
alys you particles, and then gives you an
extra life to be awarded. If we have collected the
power-up, we just check if the outer edge is and if it is
slower than the player. If playerAngle-(gap)/(gap/2) AND IF/powerUp < playerAngle+(gap).

+   12 Update the player lines 197 - 214
Next, the player is drawn (in yellow) using a simple
PolyPlot function inside the player procedure. When
there are few steps to define the movement, so when
one from one to another it glides and (doesn't)
jump to segment. The LERP function is used to
determine the movement step

+   08 Activate the warp lines 135 - 141
The warp procedure checks to see if a warp has
activated and, so, modifies the inner and outer radius so
zoom off the screen. The inner radius is reduced by a smaller
amount than the outer so you get a warp effect.

+   13 Calculate the lerp lines 225 - 265
The draw lerp (DEF LERP) takes three arguments,
if the first two are start and end of something, it
could be between two points regardless of
score, or before, the third number is
to work an equal step between the first. The function
nis used to ensure that there is enough and smooth
ment

+   09 Check the lasers lines 142 - 189
One of the shorter sections of our final code listing,
DEF PROC lasts is a quick (simple) IF
to see if we are running lasers or not. The fire speed
is adjusted accordingly, using hard-coded values than
more

```
DEF lerp(a, b, c)
result = a + c * (b - a)
```

+   10 Stage the staggers lines 190 - 224
HEP PROC enters. Here we use a counter
variable,delay, to determine how long the de
each enemy in the game loop is lasting so
you'll see one more than once or maybe again.

+   14 Playing field and perspective lines 267 - 305
Next up, we draw the field. Each segment is drawn
with the drawPlayer procedure. The size and position persist
until completed. The GAP variables determine the size of
segment. Moving from one to the next procedure, it's
relativePerspective is a little radius. This simply
changes the size of the field as the player moves and
ifts the origin a bit so that everything is drawn
from that point center.

+   11 Update the stars lines 230 - 266
To create an illusion of flying through space, we have
a field that displays objects like enemies and the
background stars move towards the center. The stars
handed with DEF PROCUpdates:The FOR CYCLE
loop counts from one to max. If the star goes off
it is repositioned in the center of the screen with a smallandom offset, so they don't start in the dead center.

+   15 Draw the power-up lines 306 - 329
The drawPowerUp procedure checks to see if the
power is within the outer radius, and, so, modifies its
brightness depending on how to keep it edge. LERP
is used again to draw from one step to the core
next and smooth the transition from the centre outwards.

* With