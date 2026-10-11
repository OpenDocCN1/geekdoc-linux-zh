# Tutorial

# Battleships

![](bbox=[0.04, 0.15, 0.13, 0.19])

# Pixel Inspiration

Johan Viet has some excellent and inspirational examples of 8x8 pixel art ([http://bit.ly/8xBipixe](http://bit.ly/8xBipixe)lart), which include some famous characters and will show you what you can create with 64 pixels of colour.

```
sense.show_message("BETTER LUCK NEXT\nTIME", text_colour=[0, 255, 255])
pygame.mixer.music.load("sounds/intro.mp3") # add a sea sound
nexttime.mp3" # add a sea sound
pygame.mixer.music.play()
```

![](bbox=[0.21, 0.24, 0.42, 0.26])

# 07 Starting the game

This completes all the game mechanics, which are stored in the function called main() – this code will only run when main() is called. However, before that, let’s create an introduction to the game. Begin by playing a suitable sound, line one. This example is the soothing sound of waves. Trigger the sound to play, line two. On line three, use the code import intro_ship to import the animation you created in Step 2. This is displayed as the sound is playing, creating a nice introduction to the game.

```
pygame.mixer.music.load("sounds/intro.mp3") # add a sea sound
pygame.mixer.music.play()
import intro_ship
```

# 08 Beginning the game

After the short animation finishes, we announce the start of the game to the player. This uses the familiar sense.show_message code to scroll a message across the LED matrix. This time, add a background colour using the code back_colour=[0, 0, 180], line one. Create a variable, line two, which sets the state of the game in play as True, meaning the game is in play. Next, check that the game is in play, line three, and create another variable called play_again, line four, to respond if a player wishes to play the game again.

# 09 Create the sea

Now to create the sea. This is a list containing 64 items which turn each matrix LED blue. Every time you select a position, the data from the Sea2 list (created in tutorial one), an enemy ship or ammo dump is added to the current position in the Sea list. Then the LED display is updated. Begin by setting the colour and assigning it to a variable called S. Then create the list and add 64 ‘S’ characters – note that a comma is not required after the last one. To write the list data to the LEDs, use the code sense.set_pixels(Sea). Add a small delay and then stop the intro music from Step 7 playing. Note that all these lines are indented in the code.

# 10 Get ready and countdown

After the introduction to the game, inform the player to ‘get ready’ as the game is about to begin. This is triggered by a simple sound file and uses the Pygame code which you’ve used before. Next, create a simple countdown from three to one. This uses a loop to iterate over a list in reverse order. Each time, it displays the number: sense.show_letter(str(num)). Note that the number is converted into a string before being displayed. As before, add a small delay between each number being shown.

![](bbox=[0.47, 0.16, 0.68, 0.22])

# 11 Go

After the countdown, the game is ready to play. Inform the player with a simple ‘go’ or similar auditory command, lines one and two. Then call the main() game function that you began in tutorial one and completed in Step 6. Since the main() function is at the beginning of the Python program, it is already loaded and ready to deploy. The game begins…

```
pygame.mixer.music.load("sounds/go.mp3")
pygame.mixer.music.play()
### Begin the main game ###
main()
```

# 12 Play again?

The game will now begin and you can select your chosen location in the sea. This position is checked to see if there is an enemy ship, ammo or just open space. Once the main() function has finished, it breaks out of the game loop and runs the code below. This gives you the option to play again. Begin by loading the ‘choice’ image. Then load and play a sound file asking the player if they want to play again.

![](bbox=[0.47, 0.66, 0.68, 0.78])

# 13 Checking for player response

To respond to the question the Sense HAT joystick can be used to select up or down. One line one, a while() loop which checks if the game choice is equal to a value of one or true. If it is then use Pygame to check for