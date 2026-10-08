
# Create with Python

# A visual novel game

## How it relates

```python
import pygame
screen = pygame.display.set_mode(size)
screen.fill(gray)
text = pygame.font.render('US SCHOOL', True, (255, 255, 255))
start_button = pygame.draw.rect(black, pygame.Rect(415, 310, 180, 55))
screen.blit(text, start_button.getleft() + 10, 0)
pygame.display.flip()
```

**07** In our game, the code pulls in elements from the script as it goes. It works lately, but this also allows us to implement decisions to change which direction the game might take you in.

```python
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        pygame.quit()
    if event.type == pygame.MOUSEBUTTONDOWN:
        pos = pygame.mouse.get_pos()
        if start_button.collidepoint(pos):
            start_game()
```

## See the mouse

## First screen

## Starting the game

**11** As we created a rectangle and now image on the menu, we need to emphasize when the mouse is hovering over it to know when the button is clicked. First we have to use event.get() to use the mouse in game, then we look for the position with get_pos(). After that, we will wait for it, screen by clicking (coordinates of the rectangle) and make a decision after that.

**13** The first screen is different, and to get every element on the interface - it makes the code a little less time to process. We begin using the string/interactive allows us to keep our place in the story and call upon the relevant function from the script file.

We don't need many for the state of the novel world here. We've implemented the new game, our script as a module and the theme audio for aesthetic reasons - we're going to handle the code in bits rather than instantly change to the scene. We also initialize with a simple pygame().

We then use an iterative function to successfully add elements to create the illusion that it's building up the first screen. We finish by advancing the progression value.

## Start the story

**12** Our start_game is called when the mouse clicks the right position and we prepare the game, getting the characters, locations and positions through the game script. The rest of this function uses to fill in data from the script to make the game flow properly.

## Add variables and assets

**09** We add a mixture of information to need the novel. We define the size of the display (1000 pixels wide and 563 high), with some RGB colors for the code to use. We're also using Pygame font and how how for certain sections and loading images for the game.

> "Our next if statement iteration checks what is different from the next line"

```python
while turn == 0 and click_state() == 1:
    line_start = 0
    line = ''
    while line_start < len(line) and line[line_start] != ' ':
        screen.blit(location[line[line_start]], [0, 0])
        line_start += 1
    while line_start < len(line) and line[line_start] != ' ':
        screen.blit(character[line[line_start]], [377, 113])
        line_start += 1
    while line_start < len(line):
        screen.blit(font.render(line, (gray), pygame.Rect(130, 623, 120, 250)), (1, 255, 255))
    turn = 1
if game_state == 'next':
    game_script = line[3]
    game_state = line[4]
line_start = 1
pygame.display.flip()
```

## Start the game

**10** Pygame works by constantly updating the menu information. New freedom adds elements to the display (which we've titled screen), fill it with color, and also shapes and built to add images or in case text. With a buffer of changes to the scene, update it with the flip function.

![](img/c72194f2c3aec198936695a665a5167c_99_0.png)

# Make a visual novel game

# Create with Python

```python
def game():
    global game_running
    while game_running == True:
        menu_screen()
```

# Expand your code

16 The code is written very expandable, allowing you to add choices that are logged to take you to different scenes (or routes in visual novel terminology) and make your game feel more interactive. This would not require much more statements, and it would also be a good way for you to look into adding graphical buttons to use the collision function.

# game()

# Add variables and assets

# The starting function

14 Similarly to the way our original startup code works, our next if statement and iteration checks to see what is different on the next line, and if it moves to a different scene function. In addition, it will also change that without filling the buffer more than needed. Where we've made no change is labelled with a 0 in the scripts.

15 We finish our code bit with off the entire game. This is just to encapsulate the entire code and allows us to add different ways of turning it off (the UI, when running to load everything and then run the game() function at the end - this is how you can add a __main__ function at the end which will start the code in the command line.

# Move the assets

17 Currently the code has the script-specific assets in the main visualnovel file. These can be moved to script, allowing you to make the visual novel much more modular so that you have multiple scripts with different assets to load at startup.

![](img/c72194f2c3aec198936695a665a5167c_100_0.png)

Hey there, how's it going?

# Use Python with Pi

# Create amazing projects

![](img/c72194f2c3aec198936695a665a5167c_101_0.png)

# Use Python with Pi

Amazing creations with Python code and Raspberry Pi

From the tutorials up to this point, you'll have a firm grounding in Python. Now we're going to add the Raspberry Pi to a mobile phone. You'll discover exciting projects such as sending SMS texts from your Raspberry Pi to a mobile phone (p.102), a voice synthesiser (p.114), and this quadcopter (right, p.116). You'll also learn how to code a Twitter bot (p.122), and control an LED with Python (p.124).

# Create amazing projects

# Use Python with Pi

![](img/c72194f2c3aec198936695a665a5167c_102_0.png)

# Use Python with Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and lay the foundations for

# Use Python with Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and lay the foundations for

# Use Python with Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and lay the foundations for

# Use Python with Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

```python
#!/usr/bin/env python
# A Python program that will demonstrate basics
import sys

# Get the user's name
name = input('Please enter your name: ')

# Print a greeting
print(f'Hello, {name}!')

# A simple loop
for i in range(5):
    print(f'Iteration {i}')

# A function definition
def greet(person):
    return f"Welcome, {person}!"

# Call the function
print(greet("World"))

# Error handling
try:
    number = int(input("Enter a number: "))
    print(f"The square of {number} is {number**2}")
except ValueError:
    print("That's not a number!")

if __name__ == "__main__":
    print("Program finished.")
```

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

02 Start Geiger by going to the LXDE menu and going to Programs. From here, select Geiger. 

```python
#!/usr/bin/env python
# A Python program that will demonstrate basics
import sys

# Get the user's name
name = input('Please enter your name: ')

# Print a greeting
print(f'Hello, {name}!')

# A simple loop
for i in range(5):
    print(f'Iteration {i}')

# A function definition
def greet(person):
    return f"Welcome, {person}!"

# Call the function
print(greet("World"))

# Error handling
try:
    number = int(input("Enter a number: "))
    print(f"The square of {number} is {number**2}")
except ValueError:
    print("That's not a number!")

if __name__ == "__main__":
    print("Program finished.")
```

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# Using Python on Raspberry Pi

Program in Python with the Raspberry Pi, and

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets

# Using Python on Raspberry Pi

# What you'll need...

A Raspberry Pi with all necessary peripherals SD card with latest Debian image for Pi www.raspberrypi.org/downloads

# Using Python on Raspberry Pi

- This tutorial will cover topics as:
- Basic arithmetic
- Comparison operators
- Control structures
- File handling
- Functions
- Libraries
- Modules
- Object-oriented programming
- Strings
- Tuples
- Lists
- Variables
- Dictionaries
- Sets
