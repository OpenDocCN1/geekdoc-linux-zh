# Python essentials

```
#!/usr/bin/env python2

#linux User & Developer presents: Mega Microgames Collection

from Tkinter import *

import rockpaperscissors
import hangman
import pokerdice

root = Tk()
root.title ("Linux User & Developer's Mega Microgames Collection")

mainframe = Frame(root, height = 200, width = 500)
mainframe.pack_propagate(0)
mainframe.pack(padx = 5, pady = 5)

intro = Label(mainframe, text = """Welcome to Linux User & Developers Mega Microgames Collection.
Please select one of the following games to play:
""")
intro.pack(side = TOP)

rps_button = Button(mainframe, text = "Rock, Paper, Scissors", command = rockpaperscissors.gui)
rps_button.pack()

hm_button = Button(mainframe, text = "Hangman", command = hangman.start)
hm_button.pack()

pd_button = Button(mainframe, text = "Poker Dice", command = pokerdice.start)
pd_button.pack()

exit_button = Button(mainframe, text = "Quit", command = root.destroy)
exit_button.pack(side = BOTTOM)

root.mainloop()
```

# MAIN WINDOW

The main interface window that this code creates is fairly basic, but contains the functions we require. The window exit button will do the same job as the Quit button, and the Hangman and Poker Dice buttons run the old scripts in the Python shell.

![](bbox=[0.7, 0.32, 0.88, 0.39])

+   **01 First line** We use this line to enter the path to the Python interpreter. This lets us run the program inside a terminal or otherwise outside of a Python-specific IDE like IDLE. Note that we're also using Python 2 for this particular script.

+   **02 Import graphics** Tkinter is the graphical interface we're using and while it's a standard Python function, you'll need to import the module so you can use it. We used the "from [module] import " method so that we can use the functions from it without having to add Tkinter at the beginning.

+   **03 Import games** We're importing the modules for the three games. We added the line at the bottom

of each script so we can do this. To make sure to differentiate the functions in each game, we will have to specify [module].[function] so there are no errors in the code.

+   **04 Root window** Using the Tk() function creates the window we're going to be placing everything into. We've decided to call it root for now; however, you can call it anything you like, as long as you're consistent with it. We've also named it using the title command from Tkinter and a string of text.

+   **05 Main frame** The first line has us set the variable mainframe as a Frame in the interface. We've attached it to root, the main window, and given

it a minimum height and width in pixels. We use pack_propagate to create the window, and then make sure it's the size that we've defined. We've then used pack to pad the borders, allowing the contents of the window to not touch the sides of it.

+   **06 Introductions** We create the intro variable as a label that lives in the main frame. We give it text to introduce the interface, using the triple quote marks to have it go across multiple lines and format better. We then use pack to display it, and tell Tkinter to put it at the top of the interface.

+   **07 Rock, Paper, Scissors** We create a button for the Rock, Paper, Scissors game using the Button function. We attach to it the main frame, give it a label using