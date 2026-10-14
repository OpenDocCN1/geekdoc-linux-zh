
# I see ASCII

Here’s a close-up of the seven stages we’ve used for Hangman’s graphics. You can change them yourself, but you need to make sure the quote marks are all in the correct place so that the art is considered a text string to be printed out.

![](img/3b256f430f51c98f1315671f6e4eec19_33_0.png)

```
```python
#!/usr/bin/env python2

from random import *

player_score = 0
computer_score = 0

def hangman(hangman):
    graphic = [
        """
             +------+ 
             |      |
             |
             |
             |
             |
             =============
        """,
        """
        ]

def start():
    print “Let’s play a game of Linux Hangman.”
    while game():
        pass
scores()
```
```

## The rules

Although we’ve moved some of the rules to the ‘game’ function this month, you can always put them back here and call upon them using the global variable, as we would do with the scores. For the words, you could also create a separate file and import them like the random module.

01  We begin by using this line to enter the path to the Python interpreter. This allows us to run the program inside a terminal or otherwise outside of a Python-specific IDE like IDLE. Note that we’re also using Python 2 for this particular script, as it is installed by default on most Linux systems and will therefore ensure compatibility.

02  We’re importing the ‘random’ module slightly differently this time, importing the actual names of the functions from random rather than just the module itself. This allows us to use the functions without having syntax like random.function. The asterisk imports all the functions from random, although you can switch that for specific names of any of random’s functions. We’ll be using the random function to select a word for the player to guess.

03  Very simply, this creates a variable that can be used throughout the code to keep track of scores. We need to start it at zero now so that it exists; otherwise if we defined it in a function, it would only exist inside that function. The code adds a point to the computer or player depending on the outcome of the round.

04  Our simple graphics consist of a series of ASCII hangman stages. We’re storing these in a function as a list of separate string objects so we can call upon them by passing on the number of incorrect guesses to it. There are seven graphics in all, like in the pen-and-paper version. We also include the print command with the function, so when it’s called it will completely handle the selection and display of the hanging man, with the first one being printed after the first letter is guessed.

05  Here we define the actual beginning of the code, with the function we’ve called ‘start’. It’s quite simple, printing our greeting to the player and then starting a while loop that will allow us to keep playing the game as many times as we wish. The pass statement allows the while loop to stop once we’ve finished, and could be used to perform a number of actions.

```
def game():
    dictionary = ["gnu","kernel","linux","mageia","penguin","ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    clue = word_length * ["_"]
    tries = 6
    letters_tried = ""
    guesses = 0
    letters_right = 0
    letters_wrong = 0
    global computer_score, player_score
    while (letters_wrong != tries) and ("".join(clue) != word):
        letter=guess_letter()
        if len(letter)==1 and letter.isalpha():
            if letters_tried.find(letter) != -1:
                print "You've already picked", letter
```

of other tasks if so wished. If we do stop playing the game, the score function is then called upon –we'll go over what that does when we get to it.

it's checking against letters already played. Finally, we create empty variables for the number of guesses made, letters correct and letters incorrect, to make the code slightly easier. We also import the global scores here.

### 06

We have put a majority of the game code in the 'game' function this time around, as there's not as much that needs to be split up. You can split it up further if you wish, using the style of code from last issue, if it would make the code cleaner for you or help you understand the building blocks a bit more.

### 09

We're starting a while loop to perform the player selection and check the status of the game. This loop continues until the player wins or loses. It starts by checking if all the tries have been used up by seeing if letters_wrong is not equal to tries. As each try will only add one point to wrong, it will never go above six. It then concatenates 'clue' and sees if it's the same as the word the computer selected. If both these statements are true, it goes on to the next turn.

### 07

The first four lines quickly set up the word for the player to guess. We've got a small selection of words in a list here. However, these can be imported via HTML or expanded upon. Choice is used to select a random element from the list, which comes from the random module we imported. Finally, we ascertain how long the string is of the word to guess, and then create the clue variable with a number of underscores of that length. This is used to display the word as you build it up from guesses.

### 10

We call upon the function we're using to input a letter and give it the variable 'letter'. We check what it returns by first of all making sure it's only a single letter, with len(letter), then by using isalpha to see if it's one of the 26 letters of the alphabet. If these conditions are satisfied, we start a new if statement to make sure it's a new guess, and tell the player if it's already been chosen so they can start again. If all this is acceptable, we move on to the next section of the code to see if it's a correct guess or not.

### 08

We start to set up the rules and the individual variables to keep track of during the game. There can only be six incorrect guesses before the hanging man is fully drawn, or in our case displayed, so we set the tries variable to six. We'll keep track of the letters through letters_tried to make sure that not only will the player know, but also the code for when

## Indentations

While IDLE will keep track of the indents in the code, if you're using a text editor to write some Python, you'll have to make sure you're using them correctly. Python is very sensitive to whether or not indents are used correctly, and it does aid in readability as well.

![](img/3b256f430f51c98f1315671f6e4eec19_34_0.png)
