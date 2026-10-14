17 The next section of game calls upon a play_again function. Like the move function, we have human input, asking the player if they would like to play again via a text message with raw_input, with the simple 'y/n' suggestion in an attempt to elicit an expected response.

18 Giving users an option of y/n like we have should expect a response in kind. The if statement checks to see if any of our defined positive responses have been entered. As Python doesn't differentiate between upper and lower case, we've made sure that it accepts both y and Y. If this is the case, it returns a positive response to game, which will start it again.

19 If we don't get an expected response, we will assume the player does not want to play again. We'll print a goodbye message, and that will end this function. This will also cause the game function to move onto the next section and not restart.

```
def play_again():
    answer = raw_input("Would you like to play again? y/n: ")
    if answer in ("y", "Y", "yes", "Yes", "of course!"):
        return answer
    else:
        print "Thank you very much for playing our game. See you next time!"
```

```
def scores():
    global player_score, computer_score
    print "HIGH SCORES"
    print "Player: ", player_score
    print "Computer: ", computer_score
```

```
if __name__ == '__main__':
    start()
```

![](bbox=[0.11, 0.7, 0.58, 0.92])

# ELIF

IF also has the ELIF (elseif) operator, which can be used in place of the second IF statement we employed. It's usually used to keep code clean, but performs the same function.

20 Going back to the start function, after game finishes we move onto the results. This section calls the scores, which are integers, and then prints them individually after the names of the players. This is the end of the script, as far as the player is concerned. Currently, the code won't permanently save the scores, but you can have Python write it to a file to keep if you wish.

21 The final part allows for the script to be used in two ways. Firstly, we can execute it in the command line and it will work fine. Secondly, we can import this into another Python script, perhaps if you wanted to add it as a game to a collection. This way, it won't execute the code when being imported.