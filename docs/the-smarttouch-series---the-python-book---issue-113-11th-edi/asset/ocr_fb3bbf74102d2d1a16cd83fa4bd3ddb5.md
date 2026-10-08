# The breakdown

01 We need to start with the path to the Python interpreter here. This allows us to run the program inside a terminal or otherwise outside of a Python-specific IDE like IDLE. Note that we're also using Python 2 rather than Python 3 for this particular script, which needs to be specified in the code to make sure it calls upon the correct version from the system.

02 We're importing two extra modules on top of the standard Python code so we can use some extra functions throughout the code. We'll use the random module to determine what move the computer will throw, and the time module to pause the running of the code at key points. The time module can also be used to utilise dates and times, either to display them or otherwise.

03 We're setting each move to a specific number so that once a selection is made by the player during the game, it will be equated to that specific variable. This makes the code slightly easier later on, as we won't need to parse any text for this particular function. If you so wish, you can add additional moves, and this will start here.

```
```python
#!/usr/bin/env python2

# linux User & Developer presents: Rock, Paper, Scissors: The Video Game

import random
import time

rock = 1
paper = 2
scissors = 3

names = { rock: "Rock", paper: "Paper", scissors: "Scissors" }
rules = { rock: scissors, paper: rock, scissors: paper }

player_score = 0
computer_score = 0
```
```

04 Here we specify the rules for the game, and the text representations of each move for the rest of the code. When called upon, our script will print the names of any of the three moves, mainly to tell the player how the computer moved. These names are only equated to these variables when they are needed - this way, the number assigned to each of them is maintained while it's needed.

05 Similar to the way the text names of the variables are defined and used only when needed, the rules are done in such a way that when comparing the results, our variables are momentarily modified. Further down in the code we'll explain properly what's happening, but basically after determining whether or not there's a tie, we'll see if the computer's move would have lost to the player move. If the computer move equates the losing throw to the player's move, you win.

06 Very simply, this creates a variable that can be used throughout the code to keep track of scores. We need to start it at zero now so that it exists, otherwise if we defined it in a function, it would only exist inside that function. The code adds a point to the computer or player depending on the outcome of the round, although we have no scoring for tied games in this particular version.

# Python modules

There are other modules you can import with basic Python. Some of the major ones are shown to the right. There are also many more that are included as standard with Python.

| Module | Description |
|---|---|
| string | Perform common string operations |
| *datetime* and *calendar* | Other modules related to time |
| *math* | Advanced mathematical functions |
| *json* | JSON encoder and decoder |
| *pydoc* | Documentation generator and online help system |