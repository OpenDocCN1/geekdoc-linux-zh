# Code listing continued

The actual game starts here, with a while loop to let you continually play the game until you decide otherwise, then ending the program

The game rules are decided here, as well as the setup for the word and keeping track of tries and incorrect answers

Each round of the game is played here, asking for an input, then telling you if you were correct or not. It prints out the graphic and changes any variables that need to be updated, especially incorrect and correct guesses

After each round, the code checks if you’ve won or lost yet – the win condition being that you guessed the word, or losing if you’ve made six guesses

The human input for the game takes the letter and turns it into something the code can use. It’s verified in the previous block of code and then referred back to if you’ve entered an unsupported or already used character

The same class as last time, which allows you to select whether or not you wish to play again

Upon quitting the game, scores are given for the duration of the play session. We also end the script with the if\_\_name\_\_ code like before

# CODE HIGHLIGHTING

IDLE automatically highlights the code to make reading your work that little bit easier. It also allows you to change these colours and highlighting in IDLE’s Preferences, in case you’re colour blind or are just used to a different colour scheme in general.

```
```
def start():
    print("Let's play a game of Linux Hangman.")
    while game():
        pass
    scores()

def game():
    dictionary = ["gnu", "kernel", "linux", "magics", "penguin", "ubuntu"]
    word = choice(dictionary)
    word_length = len(word)
    clue = word[:length + ["-"]
    tries = 6
    letters_tried = ""
    guesses = 0
    letters_right = 0
    letters_wrong = 0
    global computer_score, player_score

    while (letters_wrong != tries) and ("".join(clue) != word):
        letter = guess_letter()
        if len(letter) == 1 and letter.isalpha():
            if letters_tried.find(letter) != -1:
                print("You've already picked", letter)
            else:
                letters_tried = letters_tried + letter
                first_index = word.find(letter)
                if first_index == -1:
                    letters_wrong += 1
                    print("Sorry", letter + " isn't what we're looking for.")
                else:
                    print("Congratulations", letter + " is correct.")
                    for i in range(word_length):
                        if letter == word[i]:
                            clue[i] = letter
                    else:
                        print("Choose another")
                    hangman(letters_wrong)
                    print = "".join(clue)
                    print "Guesses: ", letters_tried
        if letters_wrong == tries:
            print "Game Over!"
            print "The word was", word
            computer_score += 1
            break
        if "".join(clue) == word:
            print "You Win!"
            print "The word was", word
            player_score += 1
            break
    return play_again()

def guess_letter():
    print
    letter = raw_input("Take a guess at my mystery word:")
    letter.strip()
    letter.lower()
    print
    return letter

def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("Y", "y", "yes", "Yes", "of course!"):
        return answer
    else:
        print "Thank you very much for playing our game. See you next time!"

def scores():
    global player_score, computer_score
    print "HIGH SCORES"
    print "Player: ", player_score
    print "Computer: ", computer_score

if __name__ == "__main__":
    start()
```
```