# # Build a multiple-choice quiz



# ## Fill out the answers

**02** Repeat this process for three new lists, each with an answer. It pays to arrange them side by side while doing this so you can ensure you get a right answer in each one. Create a final list that has a number one to three. This identifies which number list has the right answer.

![](bbox=[0.06, 0.38, 0.38, 0.52])

# ## Set it up

**03** Now create three new variables called ‘Capital’, ‘YourScore’ and ‘counter’. Untick all the variables in the list so they disappear from the stage. Set the ‘counter’ to 1 and ‘YourScore’ to 0. Position the sprite and warn the player to be ready.

![](bbox=[0.05, 0.78, 0.4, 0.95])

# ## Create loop, set question

**04** Drag a ‘Repeat’ loop from Control and set it to 10 for the number of questions. Add function ‘Set Capital’ to 0. Drag in an Operator called ‘Join ()’. Make the first half text. Add a variable to the other half and put ‘Counter’ into ‘Questions’.

# ## Display the answers

**05** From Looks add a ‘Say ()’ and drop in ‘Capital’. Then create the three answers by using the ‘Say’ command and adding a ‘Join ()’. The first entry is simply the number of the answer, the second part is the text.

![](bbox=[0.44, 0.38, 0.76, 0.52])

# ## Scan for the answers

**06** There are pauses between the answers being displayed. Add ‘Say’ to prompt to press 1, 2 or 3. Drag in a ‘Wait until’ Control. Go into Operators. There are only ones with two conditions so use that, then put an extra two conditions into the second box to make three.

![](bbox=[0.45, 0.78, 0.78, 0.95])

# ## Is the answer right?

**07** Drag in an ‘If ()’ Control. Drop a ‘)’ and ‘()’ Operator into the space. In the first space add ‘Key 1 pressed’ and ‘0 = [?] Operator’. In the second put another ‘[?] = [?] Operator’. In the first part add Item ‘[?] of [?]’ from ‘Variable’ with ‘Counter’, and in the second type ‘1.’

![](bbox=[0.81, 0.38, 0.99, 0.6])

# ## Repeat and add score

**08** Add a ‘Change Your Score by 1’ for a correct answer. Repeat this twice for the other answers. Then increase the ‘Counter’ variable by 1 and clear the screen. Outside the loop add some pauses to show the quiz is over and then display the score in ‘YourScore’. Well done, you’ve finished your first quiz game!