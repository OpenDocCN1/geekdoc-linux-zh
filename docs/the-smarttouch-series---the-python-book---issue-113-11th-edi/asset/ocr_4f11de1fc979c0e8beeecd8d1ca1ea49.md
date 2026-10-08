# Python essentials

**17 Start over**
The usual *array* of command-line compatibility and module importing here. The **groupby** function is specifically imported here for dice analysis.

**18 Outside dice**
For Poker Dice, there’s only one variable to show at any one time, the dice. Again, due to the nested functions, and because we’re using Python 2, we need to call it with **global** from here to make sure the game can be reset properly.

**19 Dice rolls**
The roll function has been removed from the **gui** function as so not to create any code errors with some of its variables. It can be easily called within the nested functions. It hasn’t changed at all from the original code.

**20 Hand of dice**
Like roll, nothing has changed for the **hand** function. It’s simply now placed outside the **gui** function for the exact same reasons. It also means that you can easily import this function into another script if you wish.

**21 GUI start**
As we’ve mentioned last month and in the Hangman code, we put all the GUI code into a function so that we can call on it when we want to. In this case, pressing the Poker Dice button on the main interface activates **pokerdice.gui**, which is this function.

**22 First roll**
As the window opens, we immediately make the first roll. This is then sorted, each number is attributed to a card, and then the result is created to be displayed in the main window. This is similar to how it worked before, but instead it’s now entered into the StringVars for the interface towards the end of the script

**23 Start game**
When we activate the button that starts **game**, it immediately sends us to the rest of the code. This would also work if you had the button go to the **throws** function instead; however, you can add more functions to this part if you wish.

**24 Dice selection**
The first thing we do is find out what checkboxes have been ticked by the player. We then put these in a list so we can change out the correct dice numbers. We’ve also brought in **dice** so we can check against what the current dice rolls are.

```
#!/usr/bin/env python2
from Tkinter import *
from ttk import *
import random
from itertools import groupby
dice = 0
```

```
def roll(roll_number):
    numbers = range(1,7)
    dice = range(roll_number)
    iterations = 0
    while iterations < roll_number:
        iterations = iterations + 1
        dice[iterations-1] = random.choice(numbers)
    return dice
```

```
def hand(dice):
    dice_hand = [len(list(group)) for key, group in groupby(dice)]
    dice_hand.sort(reverse=True)
    straight1 = [1,2,3,4,5]
    straight2 = [2,3,4,5,6]
    if dice == straight1 or dice == straight2:
        return "a straight!"
    elif dice_hand[0] == 5:
        return "five of a kind!"
    elif dice_hand[0] == 4:
        return "four of a kind!"
    elif dice_hand[0] == 3:
        if dice_hand[1] == 2:
            return "a full house!"
        else:
            return "three of a kind."
    elif dice_hand[0] == 2:
        if dice_hand[1] == 2:
            return "two pair."
        else:
            return "one pair."
    else:
        return "a high card."
```

```
def gui():
    global dice
    dice = roll(5)
    dice.sort()
    nine = 1
    ten = 2
    jack = 3
    queen = 4
    king = 5
    ace = 6
    names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A"}
    result = ("You have " + hand(dice))
```

```
def game():
    throws()
```

```
def throws():
    global dice
    dice1_check = dice1.get()
    dice2_check = dice2.get()
    dice3_check = dice3.get()
    dice4_check = dice4.get()
    dice5_check = dice5.get()
    dice_rolls[] = [dice1_check, dice2_check, dice3_check, dice4_check, dice5_check]
```

![](bbox=[0.66, 0.2, 0.88, 0.28])

![](bbox=[0.66, 0.47, 0.88, 0.67])