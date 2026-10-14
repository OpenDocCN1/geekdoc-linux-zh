
# Bring graphics to simple Python games

Complete your trio of games with a graphical interface for the hangman and poker dice code

We have now created a simple selector for the trio of Python games we made previously. This interface was able to launch a GUI for our rock, paper, scissors game, and run the other two in the terminal. Now, we’re going to convert the hangman and poker dice codes to work in a similar way to rock, paper, scissors.

The trick with hangman comes in allowing for a different type of input, text, and the ability to have multiple rounds of the game. Tkinter allows for text entry, and we rely a lot less on

'while' loops to play the game in its entirety. Poker Dice needs to keep the dice analysis code, and the option to change specific dice using checkboxes.

We’ll be modifying a large amount of the original code to fit in with the new graphical scheme. This mainly involves cutting specific parts and having the Tkinter-specific code handle these itself. The code listings on these pages include the modified code – we’ll discuss the graphical part on the following pages.

## Resources

Python 2: www.python.org/download
IDLE: www.python.org/idle

1 Imported
Here we’re doing the same minor setup, including getting the Tkinter module that helps us create a simple graphical interface

2 Words
We’re keeping our variables that determine the word to guess here so it can be easily accessed anywhere in the code

3 Function
Like last time, we’re putting the majority of our original code into a new function, gui

4 Analysis
We select the word and analyse it before continuing on with the rest of the code

5 Graphics
The hangedman function is largely unchanged, albeit with new code to display our ASCII graphics on the interface

6 Guesses
We check the number of mistakes made, and call the guess_letter function to check the letter entered

## Hangman Code Listing

```
from Tkinter import *
from ttk import *
from random import *
word = 0
word_length = 0
clue = []
```

```
def gui():
    global word, word_length, clue
    dictionary = ["gnu", "kernel", "linux", "mageia", "penguin", "ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    tries = 0
```

```
def hangedman(hangman):
    graphic = [
        "     ",
        "  ---------",
        "  |       |",
        "  |       0",
        "  |      /|\",
        "  |       |",
        "  |      / \ ",
        "  |",
        "=========",
    ]
    graphic_set = graphic[hangman]
    hm_graphic.set(graphic_set)
```

```
def game():
    letters_wrong = incorrect_guesses.get()
    letter=guess_letter()
    first_index = word.find(letter)
    if first_index == -1:
        letters_wrong +=1
        incorrect_guesses.set(letters_wrong)
    else:
        for i in range(word_length):
```

```
if letter == word[i]:
    clue[i] = letter
hangedman(letters_wrong)
clue_set = "".join(clue)
word_output.set(clue_set)
if letters_wrong == tries:
    result_text = "Game Over. The word was " + word
    result_set.set(result_text)
    new_score = computer_score.get()
    new_score += 1
    computer_score.set(new_score)
    if "".join(clue) == word:
        result_text = "You Win! The word was " + word
        result_set.set(result_text)
        new_score = player_score.get()
        new_score += 1
        player_score.set(new_score)
```

```
def guess_letter():
    letter = letter_guess.get()
    letter = letter.strip()
    letter = letter.lower()
    return letter
```

```
def reset_game():
    global word, word_length, clue
    incorrect_guesses.set(0)
    hangedman(0)
    result_set.set("")
    letter_guess.set("")
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    new_clue = "".join(clue)
    word_output.set(new_clue)
```

```
if __name__ == '__main__':
    gui()
```

## Poker Dice Code Listing

# 1 More imports

We've added the new imported modules we need to make Tkinter work and keep the rest the same

# 2 Dice list

The list that holds the dice is kept outside the main function so that it can be accessed everywhere

# 3 Rolls

Same goes for the roll function. It doesn't specifically need to be inside the gui function anyway

# 4 Decisions

The checkboxes in the graphical code we're going to create later will give us numbers we can analyse for the code. We retrieve these numbers and check them to find out which dice the user wishes to re-roll

# 5 Hands

Finally, our hand analysis function is the last part of the original code that is kept outside the gui function. Both this and the above function pass the necessary details back up the chain to then be added into the new graphical elements of the new interface

# 6 No dice

If no dice have been selected to re-roll, the hand output is changed to show a final message

# 7 Re-roll

This part is almost the same as before - a new set of dice are rolled and then inserted into the list of dice like before, then re-sorted to make the hand analysis easier

# 8 More functions

The new gui function is the main change to the Poker Dice code, and as before includes the Tkinter elements and other parts of the original code

# 9 Game start

A simple function that we can use to activate the re-rolls of the dice

# 10 New hand

The new dice are named, analysed, and everything is then set for the gui to display the final outcome

# 11 Reset

Like with the hangman code, we have a function to reset all the variables, allowing you to start the game again

```
from Tkinter import *
from ttk import *
import random
from itertools import groupby
dice = 0

def roll(roll_number):
    numbers = range(1,7)
    dice = range(roll_number)
    iterations = 0
    while iterations < roll_number:
        iterations = iterations + 1
        dice[iterations-1] = random.choice(numbers)
    return dice

choice(numbers)

def hand(dice):
    dice_hand = [len(list(group)) for key, group in itertools.groupby(dice)]
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
    names = { nine: "9", ten: "10", jack: "J", queen: "Q", king: "K", ace: "A" }
    result = "You have " + hand(dice)

def game():
    throws()

def throws():
```

```
global dice
dice1_check = dice1.get()
dice2_check = dice2.get()
dice3_check = dice3.get()
dice4_check = dice4.get()
dice5_check = dice5.get()
dice_re rolls = [dice1_check, dice2_check, dice3_check, dice4_check, dice5_check]
for i in range(len(dice_re rolls)):
    if i in range(dice_re rolls):
        dice_re rolls.remove(0)
    if len(dice_re rolls) == 0:
        result = "You finish with " + hand(dice)
        hand_output.set(result)
    else:
        roll_number = len(dice_re rolls)
        number_re rolls = roll(roll_num ber)
        dice_changes = range(len(dice_ re rolls))
        iterations = 0
        while iterations < roll_number:
            iterations = iterations + 1
            dice_changes[iterations-1] = number_re rolls[iterations-1]
        iterations = 0
        while iterations < roll_number:
            iterations = iterations + 1
            replacement = number_ re rolls[iterations-1]
            dice[iterations-1] = replacement
        changes[iterations-1] = replacement
        dice.sort()
        new_dice_list = [0,0,0,0,0]
        for i in range(len(dice)):
            new_dice_list[i] = names[dice[i]]
        final_dice = " ".join(new_dice_ list)
        dice_output.set(final_dice)
        final_result = "You finish with " + hand(dice)
        hand_output.set(final_result)

def reset_game():
    global dice
    dice = roll(5)
    dice.sort()
    for i in range(len(dice)):
        empty_dice[i] = names[dice[i]]
    first_dice = " ".join(empty_dice)
    dice_output.set(first_dice)
    result = "You have " + hand(dice)
    hand_output.set(result)

if __name__ == '__main__':
    gui()
```
