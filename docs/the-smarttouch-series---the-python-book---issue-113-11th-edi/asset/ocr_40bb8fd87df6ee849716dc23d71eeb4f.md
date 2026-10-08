# Create with Python

```
```
• git clone git@github.com:tomwainer/breakout.git
cd breakout
ppgzrun breakout7.py
```
```

![](bbox=[0.28, 0.23, 0.9, 0.37])

> Right Tom Viner’s array of blocks negates the need for bordered rectangles

# 14. Sounds

Also upon bat collision, `sounds.blip.play()` looks in the sounds subdirectory for a sound file called blip. You can download the sounds (and finished code) from [FileSilo.co.uk](http://filesilo.co.uk).

Actually, now we think about it, I ignore the previous comment about homework – your real homework is to turn what we’ve written so far into a proper game of *Pong!* But first let’s finish turning it into *Breakout!*

# 15. Blockhead!

If you’re not very familiar with the ancient computer game *Breakout*, then:

```
```
! apt-get install libbreakout2
```
```

... and have a play. Now, we haven’t set our sights on building something quite so ambitious in just these six pages, but we do need blocks.

# 16. Building blocks

There are many ways of defining blocks and distributing them onto the screen. In Tom Viner’s team’s version, from the London Python Dojo – which was the code that originally inspired this author to give this a go – the blocks are sized in relation to number across the screen, thus:

```
```python
N_BLOCKS = 8
BLOCK_W = W // N_BLOCKS
BLOCK_H = BLOCK_W // 4
BLOCK_COLOURS = RED, GREEN, BLUE
```
```

Using multicoloured blocks which are then built into an array means that blocks can join without needing a border. However, the array of colour breaks in a single row is not enough for a full game screen, so we’re going to build our array from hard-coded values...

# 17. Going for gold

Create a Block class:

```
```python
class Block(Rect):
    def __init__(self, colour, rect):
        Rect.__init__(self, rect)
        self.colour = colour
```
```

... and pick a nice colour for your blocks:

```
```python
GOLD = 205,145,0
```
```

# 18. Line up the blocks

This builds an array of 24 blocks, three rows of eight:

```
```python
blocks = []
for n_block in range(24):
    block = Block(GOLD, (((n_block % 8) * 100) + 2, 
                        (n_block // 8) * 25) + 2), (96, 23)))
    blocks.append(block)
```
```

# 19. Drawing blocks

Draw_blocks() is added to `def draw()` after defining:

```
```python
def draw_blocks():
    for block in blocks:
        screen.draw.filled_rect(block, block.colour)
```
```

# 20. Block bashing

All that remains with the blocks is to expand `def move(ball)` to destroy a block when the ball hits it.

```
```python
to_kill = ball.collide(blocks)
if to_kill >= 0:
    sounds.block.play()
    ball.dir_x = direction(ball.dir_x, abs(ball.dir_x))
    blocks.pop(to_kill)
```
```

# Pg0+1

There’s a new version of Pg0 in development – it may even be out as you read this. Pg0 creator Daniel Pope tells us “A one-generation API is in the works,” and at the Pg0 PyConUK sprint, “we finished Actor rotation.”

Contributions are welcome – not only to the Pg0 code, but more examples are needed not just to show what can be done, but to give teachers tools to enthuse children about the creative act of programming.

Pg0 has also inspired GPIO Zero, to make GPIO programming easier on the Raspberry Pi, with rapid development occurring on this new library as we go to press.