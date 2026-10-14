
## Play poker dice using Python

Put on your poker face and get ready to gamble as you hone your programming skill with a bit of poker dice

So you've learnt how to program tic-tac-toe and guessed your way to victory at hangman. Now it's time to head to Las Vegas and play our cards right. Or in this case, virtual dice, and more like Reno as we continue with our Python game tutorials and introduce you to some poker dice.

We're again using some of the lessons we've already learnt, including random number generation, list creation and modification, human input, rule setting, scoring and more. But we'll also be adding some new skills in this tutorial. Namely, we'll be creating and appending lists with random numbers, and using functions multiple times in one block of code to cut down on bloat.

Again, we recommend using IDLE, and we're using Python 2 to ensure compatibility with a wider variety of distros, including the Raspberry Pi. So, we hope luck is a lady for you and that the odds are ever in your favour – just keep those fingers crossed that you don't roll a snake eyes (we are coding in Python, after all!)

## Resources

Python 2: www.python.org/download

IDLE: www.python.org/idle

## The Start

Here we're doing some minor setups so we can get our code to run with some extra modules not included with the basics

## The Rules

We're setting names for each dice roll so they can be properly identified to the player – much more interesting than numbers

## The Score

Again we've got some basic variables set up so we can keep score of the games if we want to

## The Script

The game is handled here, passing the player onto the next function to actually play, and handling the end of the session as well

## The Game

We access the full game loop via here, and the function that allows us to play again if we're so inclined

## The Throw

The initial hand is dealt, so to speak, at the start of the throws function. This function handles all the decision making in the game, while passing off the dice rolls to another function

## The Hand

We've also got a special function so we can inform the player exactly what style of hand they have

## The Decision

There are two rounds in this version of poker dice, and you can select how many dice you wish to re-roll in this small while loop that makes sure you're also using a correct number

## Code listing

```
#!/usr/bin/env python2
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
    while game():
        pass
    scores()

def game():
    print "The computer will help you throw your 5 dice"
    throw()
    return play_again()

def throws():
    roll_number = 5
    dice = []
    dice.sort()
    for i in range(len(dice)):
        print "Dice", i + 1, ":", names[dice[i]]

    result = hand(dice)
    print "You currently have", result

    while True:
        rerolls = input("How many dice do you want to throw again? ")
        try:
            if rerolls in (1,2,3,4,5):
                break
        except ValueError:
            pass
        print "Oops! I didn't understand that. Please enter 1, 2, 3, 4 or 5."
```

## The Re-roll

We're doing the second set of rolls and starting the end of the game here by calling on the same function as before, but we're also aware that choosing no re-rolls means the end of the game

## The Dice

Here we're finding out which dice the player wants to re-roll, and also making sure that they enter a valid number. Just so they know they're doing something, we print something after every turn

## Second Hand

We change and display the new dice hand to end the game. Again, we make sure to tell the player what the actual hand they have is

## The Rolls

The function we reuse to roll our virtual six dice using a simple while loop. This allows us to keep the codebase smaller

## The Analysis

There are eight possible types of hands in poker dice, and we can use a bit of logic to work out all but one of them without checking against all 7,776 outcomes – in fact, we only specifically have to check for two

## The Question

Our simple 'play again' function that parses player input so we can restart or end the script

## The End

Scores are displayed at the end of the script, and the very final part allows us to import this into other Python scripts as a module

## EXTRA FUNCTIONS

Splitting up actions into functions makes it easier to not only perform them multiple times, but reduce the amount of code. On larger projects, this can aid with speed.

## Code listing continued

```
if rerolls == 0:
    print("You finish with", result)
else:
    roll_number = rerolls
    dice, changes = roll_number
    dice changes = range(rerolls)
    print("Enter the number of a dice to reroll: ")
    iterations = 0
    while iterations < rerolls:
        iterations = iterations + 1
        while True:
            selection = input("")
            try:
                if selection in ("1", "2", "3", "4", "5"):
                    break
            except ValueError:
                pass
            print("Oops I didn't understand that. Please enter 1, 2, 3, 4 or 5.")
        dice_changes[iterations-1] = selection-1
        print("You have changed dice", selection)
    iterations = 0
    while iterations < rerolls:
        iterations = iterations + 1
        replacement = dice[ dice_changes[iterations-1] ]
        dice[ dice_changes[iterations-1] ] = replacement
    dice.sort()
    for i in range(len(dice)):
        print("Dice", i + 1, ":", names[dice[i]])
    result = hand(dice)
    print("You finish with", result)

def roll(roll_number):
    numbers = range(1,7)
    dice = []
    iterations = 0
    while iterations < roll_number:
        iterations = iterations + 1
        dice[iterations-1] = random.choice(numbers)
    return dice

def hand(dice):
    dice_hand = [len(list(group)) for key, group in groupby(dice)]
    dice_hand.sort(reverse=True)
    straight1 = [1,2,3,4,5]
    straight2 = [2,3,4,5,6]
    if dice == straight1 or dice == straight2:
        return "a straight!"
    elif dice_hand[0] == 5:
        return "Five of a kind!"
    elif dice_hand[0] == 4:
        return "four of a kind!"
    elif dice_hand[0] == 3 and dice_hand[1] == 2:
        return "a full house!"
    elif dice_hand[0] == 3:
        return "three of a kind."
    elif dice_hand[0] == 2:
        if dice_hand[1] == 2:
            return "two pair."
        else:
            return "one pair."
    else:
        return "a high card."

def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("y", "Y", "yes", "Yes", "of course!"):
        return answer
    else:
        print "Thank you very much for playing our game. See you next time!"

def scores():
    global player_score, computer_score
    print "FINAL SCORE"
    print "Player: ", player_score
    print "Computer: ", computer_score

if __name__ == '__main__':
    start()
```
