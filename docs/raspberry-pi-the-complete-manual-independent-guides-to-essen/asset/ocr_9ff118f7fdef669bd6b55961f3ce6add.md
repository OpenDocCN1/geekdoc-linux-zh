# Paint the Egg sprite

**17** Click the New Sprite: Paintbrush icon to paint a new sprite. In the Paint Editor, draw a small yellow ellipse. Name the sprite Egg. The Egg will appear randomly on the stage and cause the snake to grow and increase its score.

![](bbox=[0.09, 0.21, 0.33, 0.38])

# Add Egg sound

**18** Go to the Sounds tab for the Egg sprite and import the Recreation-Symbol Crash sound. Or you can choose a different sound if you like. This sound will play when the snake eats an egg.

![](bbox=[0.09, 0.52, 0.33, 0.7])

# Add Egg scripts

**19** Copy the Egg script so that the Egg appears randomly at the start of the game. When the Egg senses that it has been eaten, it must hide, play the Cyber sound, for whatever you chose in step 18, update the score, broadcast the Egg Eaten event and then randomly appear again. When the Game Over event is received, it must stop.

# Make Bad Egg

**20** Create the black Bad Egg in the same way as the Egg but using a different graphic and the Instruments-StringPluck sound. Drag the Egg's green flag scripts onto the Bad Egg to copy them – just change the sound that is played and reduce the score instead of increasing it.

![](bbox=[0.38, 0.23, 0.62, 0.41])

# Create Bonus sprite

**22** Create the Bonus sprite in a similar way. You can choose the shape and sound for the Bonus. Its scripts are similar to the Egg ones so you could drag one of those to the Bonus sprite and work from that. Make sure you change the sound and increase the score by a random bonus.

![](bbox=[0.38, 0.55, 0.62, 0.95])

# Grow Bad Egg

**21** Add another 'when green flag clicked' script to the Bad Egg so it sets its size to the default 100% when a new game is started and then increases its size by 10 every 10 seconds. The Bad Egg will get bigger and bigger and harder to avoid.

![](bbox=[0.67, 0.23, 0.91, 0.38])