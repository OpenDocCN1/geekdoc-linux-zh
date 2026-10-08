# # Play poker dice using Python
## Put on your poker face and get ready to gamble as you hone your programming skill with a bit of poker dice

So you've learnt how to program rock, paper, scissors and guessed your way to victory at hangman. Now it's time to head to Las Vegas and play our cards right. Or in this case, virtual dice, as we continue with our Python game tutorials and introduce you to some poker dice.
We're again using some of the lessons we've already learnt, including random number generation, list creation and modification, human input, rule setting, scoring and more. But we'll also be adding some new skills in this tutorial. Namely, we'll be creating and appending lists with random numbers, and using functions multiple times in one block of code to cut down on bloat.
Again, we recommend using IDLE, and we're using Python 2 to ensure compatibility with a wider variety of distros, including the Raspberry Pi. So, we hope luck is a lady for you and that the odds are ever in your favour - just keep those fingers crossed that you don't roll a snake eyes (we are coding in Python, after all!)

# ## Resources

+   - Python 2: www.python.org/download
- IDLE: www.python.org/idle

# ### The Start

Here we're doing some minor setup so we can get our code to run with some extra modules not included with the basics

# ### The Rules

We're setting names for each dice roll so they can be properly identified to the player - much more interesting than numbers

# ### The Score

Again we've got some basic variables set up so we can keep score of the games if we want to

# ### The Script

The game is handled here, passing the player onto the next function to actually play, and handling the end of the session as well

# ### The Game

We access the full game loop via here, and the function that allows us to play again if we're so inclined

# ### The Throw

The initial hand is dealt, so to speak, at the start of the throws function. This function handles all the decision making in the game, while passing off the dice rolls to another function

# ### The Hand

We've also got a special function so we can inform the player exactly what style of hand they have

# ### The Decision

There are two rounds in this version of poker dice, and you can select how many dice you wish to re-roll in this small while loop that makes sure you're also using a correct number

```
```python
#!/usr/bin/python2
import random
from itertools import groupby

nine = 1
ten = 2
jack = 3
queen = 4
king = 5
ace = 6

names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A" }

player_score = 0
computer_score = 0

def start():
    print "Let's play a game of Linux Poker Dice."
    play_game()
    pass
    score()

def game():
    print "The computer will help you throw your 5 dice"
    throws()
    return play_again()

def throws():
    roll_number = 5
    dice = roll(roll_number)
    dice.sort()
    for i in range(len(dice)):
        print "Dice",i+1,":",names[dice[i]]

    result = hand(dice)
    print "You currently have", result

    while True:
        rereolls = input("How many dice do you want to throw again? ")
        try:
            if rereolls in (1,2,3,4,5):
                break
        except ValueError:
            pass
    print "Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5."
```
`Code listing`
```