![](bbox=[0.55, 0.0, 0.98, 0.09])

```
```python
#!/usr/bin/env python2

# Linux User & Developer presents: Rock, Paper, Scissors: The Video Game: The Module

from Tkinter import *
from ttk import *
import random

def gui():
    rock = 1
    paper = 2
    scissors = 3
    names = { rock: "Rock", paper: "Paper", scissors: "Scissors" }
    rules = { rock: scissors, paper: rock, scissors: paper }
    def start():
        while game():
            pass
    def game():
        player = player_choice.get()
        computer = random.randint(1, 3)
        computer_choice.set(names[computer])
        result(player, computer)
```
    10
    11
    12
    13
    14
```

![](bbox=[0.69, 0.32, 0.92, 0.56])

text that appears on the button, and then have it run a command. In this case, we use the modified rockpapershotgun.py code that has a gui function, hence rockpapershotgun.py. We then use pack to place it in the window

# 08 Other games

For the other two games, the code is mostly the same; however, we call upon the start function in both of them. In the final interface, this will cause the games to run in the shell or command line as they’ve been running before.

# 09 Break the loop

The exit button works similarly to the other buttons we’ve created, but instead it uses the command root.destroy(). This ends the loop that we’ve created with root.mainloop(), which allows the interface code to continue looping, allowing us to continually use it. We place the exit button at the bottom of the window with ‘side = BOTTOM’.

# 10 Game code

Nothing much has changed in the start of this code, other than a few import changes. The code for running it in the command line is still

there, and with a few modifications the code will run independently of the main interface. We’ve removed the time module, as we no longer need it, and imported not only the Tkinter module, but the ttk module. The ttk module allows us to arrange the GUI in a grid, which will be slightly easier to use and understand.

# 11 Game interface

One of the biggest changes we’re making to this script is having it all contained in one function, ‘def gui’. The interface code needs to be put into a function, otherwise it will be run during import. While we’ve chosen to put the entirety of the code in a function, you can also try just having the graphical interface code in one. All our variables are kept in here so that they still work properly.

# 12 Game variables

The variables are staying the same so that we can do the same comparisons we made in the original code. We’ve put them into the function if so that they don’t affect the other imported code into the main interface – and so that when calling just this function, we don’t need to use global to bring them in.

Our other code will run in the shell or via a command line in the same way as before when the buttons are pressed.

# 13 Start function

We’ve removed the part that calls the score function from the start function, as we have the interface handle the scoring now. It still calls upon the game function, though, putting it into a loop so it can be used continuously. This function is called by the interface to begin the game by setting a computer move and then comparing it to the player’s choice.

# 14 Game function

The game function has had a few modifications to make sure it works with the interface. First of all, the player variable is retried using get() on the special variable we’ve created to contain the player choice. We do a similar thing for the computer, using ‘set’ to change the variable in our interface-friendly computer_choice variable. We still use the name variable to set the text that goes into computer_choice. This then passes the player and computer variables along in the same way we did before.

The Python Book 53