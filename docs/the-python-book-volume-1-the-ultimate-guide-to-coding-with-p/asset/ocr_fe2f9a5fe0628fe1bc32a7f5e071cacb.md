# Python essentials

11 The result function only takes the variables player and computer for this task, which is why we set that in result(player, computer). We're starting off by having a countdown to the result. The printed numbers are self-explanatory, but we've also thrown in sleep from the time module we imported. Sleep pauses the execution of the code by the number of seconds in the brackets. We've put a one-second pause between counts, then half a second after that to show the results.

12 To print out what the computer threw, we're using string.format(). The {0} in the printed text is where we're inserting the move, which we have previously defined as numbers. Using names[computer], we're telling the code to look up what the text version of the move is called from the names we set earlier on, and then to insert that where {0} is.

13 Here we're simply calling the scores we set earlier. Using the global function allows for the variable to be changed and used outside of the variable, especially after we've appended a number to one of their scores.

```
def result(player, computer):
    print "1..."
    time.sleep(1)
    print "2..."
    time.sleep(1)
    print "3!"
    time.sleep(0.5)
print "Computer threw {0}!".format(names[computer])
global player_score, computer_score
if player == computer:
    print "Tie game."
else:
    if rules[player] == computer:
        print "Your victory has been assured."
        player_score += 1
    else:
        print "The computer laughs as you realise you have been defeated."
        computer_score += 1
```

14 The way we're checking the result is basically through a process of elimination. Our first check is to see if the move the player and computer used were the same, which is the simplest part. We put it in an if statement so that if it's true, this particular section of the code ends here. It then prints our tie message and goes back to the game function for the next step.

15 If it's not a tie, we need to keep checking, as it could still be a win or a loss. Within the else, we start another if statement. Here, we use the rules list from earlier to see if the losing move to the player's move is the same as the computer's. If that's the case, we print the message saying so, and add one to the player_score variable from before.

16 If we get to this point, the player has lost. We print the losing message, give the computer a point and it immediately ends the result function, returning to the game function.

![](bbox=[0.35, 0.64, 0.92, 0.88])