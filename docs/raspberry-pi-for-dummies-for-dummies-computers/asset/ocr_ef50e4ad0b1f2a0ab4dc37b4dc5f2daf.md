**y**: Axis runs vertically and could be described as the height. You can fly at least as 500 blocks, but you can't see the ground from higher than 70 blocks, so there's not much point. Sea level is 0. You can break blocks to tunnel under the sea. We made it down to about ~70 before we fell out of the world and died. This is the only way we've seen that you can die in Minecraft on the Pi.

**x**: This is the other axis parallel to the ground. The world measures 255 blocks in this direction.

We put the axes in order deliberately because that's the order that Minecraft uses. If, like us, you use x and y to refer to positions in 2D (as you do in Scratch), take a short while to get your head around that y represents height. Most of the time in this chapter, you'll use the x and z coordinates to describe a wall's position (which differs on the wall), and the y coordinates to describe its height (which doesn't).

As you move in the game, you can see the player's coordinates in the top left of the Minecraft window change. If you try to move outside the world, you hit a wall of sky that you can't penetrate, in *The Truman Show* (except that he had a door).

# Repositioning the player

You can move your character to any position in the Minecraft world, using this command:

```
mc.player.setTilePos(x, y, z)
```

For example, to parachute in the world, use

```
mc.player.setTilePos(0, 100, 0)
```

![](bbox=[0.17, 0.679, 0.23, 0.756])

You don't have to put this command into a program and run it. If you've already run the program to set up the Minecraft module, you can type commands to move the player and add blocks in the Python shell.

Assuming that the game is not in Flying mode, you'll drop from the sky into the world. If it is in Flying mode, click Minecraft on the taskbar and double-tap the space to turn off and start your descent.

Note that this coordinate won't always be in the middle of the world, though worlds are the same size. In one of ours, the coordinates run from -85.7 to 169.7 in the x plane and from -98.7 to 156.7 in the z plane.