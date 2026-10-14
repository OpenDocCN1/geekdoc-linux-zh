
## Python essentials

```
def result(player, computer):
    new_score = 0
    if player == computer:
        result_set.set("Tie game.")
    else:
        if rules[player] == computer:
            result_set.set("Your victory has been assured.")
            new_score = player_score.get()
            new_score += 1
            player_score.set(new_score)
        else:
            result_set.set("The computer laughs as you realise you have been defeated.")
            new_score = computer_score.get()
            new_score += 1
            computer_score.set(new_score)

rps_window = Toplevel()
rps_window.title("Rock, Paper, Scissors")

player_choice = IntVar()
computer_choice = StringVar()
result_set = StringVar()
player_choice.set(1)
player_score = IntVar()
computer_score = IntVar()
```

![](img/3b256f430f51c98f1315671f6e4eec19_47_0.png)

## 15 Result function

The result function still takes the same two variables as before, which we set in the game function. While technically we can use the variables set up for the interface, these are not pure integers and can cause an error if not handled correctly. With that in mind, we've created an empty new_score variable that we can use to effectively clean the interface value before adding it back into it.

## 16 Tie

The logic for determining the result is the same as before. We first do the easy check – whether or not the numeric value for the player and computer variable is the same. What changes this time is that, instead of printing the text, we send the "Tie game" message to our result variable using the set function from Tkinter.

## 17 Win

The if statement continues by seeing if the player has won. Like before, we use the rules we set to make the comparison for the code to make. We set the result_set like we did in the tie game, with a different message to the user. Finally, we set the new_score variable to be the current player score, using the get function to obtain it, plus one to the score, and then use set again to put it back into the player_score variable. We can't use += with the player_score variable, as it is not a standard variable.

## 18 Lose

This part of the overall if statement works in the same way as before, by assuming that if it isn't a tie or a win, it's a loss. Like the new version of the win code, it then uses set to change the message that will be displayed to the player, and calls upon and changes the computer score by putting it through the new_score variable.

## 19 New window

As the original window is part of the mainloop, we cannot have the window be created using Tk() like in the main interface code. As this window is coming off it, though, we instead create it using Toplevel(). This allows the window to run separately and on top of the main window. We've also given it a name, which will not change the main window's name in the process.

## 20 Interface variables

Here is the reason we had to call and change the variables in a different manner. For Tkinter, we need to let the interface know whether or not a variable is an integer or a text value. IntVar and StringVar allow for these respectively. We've also set the player_choice variable to be one, which we have already set as the choice for rock. This means there will at least be a default choice when the game is started, and it won't cause an error.

## 21 Game frame

We've created the frame for our interface items slightly differently. Instead of using the pack command in the main interface, we're using grid to make sure they're orientated in such a way that makes sense for the user. Padding does just that, setting up values to make sure the items in the frame don't touch the edge of the window. Using the .grid command, we then create this frame. The row and column variables allow for rows and columns to be included in the structure of

```
```python
rps_frame = Frame(rps_window, padding = '3 12 12', width = 300)
rps_frame.grid(column=0, row = 0, sticky=(N,W,E,S))
rps_frame.columnconfigure(0, weight=1)
rps_frame.rowconfigure(0,weight=1)

Label(rps_frame, text='Player').grid(column=1, row = 1, sticky = W)
Radiobutton(rps_frame, text = 'Rock', variable = player_choice, value = 1).grid(column=1, row=2, sticky=W)
Radiobutton(rps_frame, text = 'Paper', variable = player_choice, value = 2).grid(column=1, row=3, sticky=W)
Radiobutton(rps_frame, text = 'Scissors', variable = player_choice, value = 3).grid(column=1, row=4, sticky=W)

Label(rps_frame, text='Computer').grid(column=3, row = 1, sticky = W)
Label(rps_frame, textvariable = computer_choice).grid(column=3, row=3, sticky = W)

Button(rps_frame, text='Play', command = start).grid(column = 2, row = 2)

Label(rps_frame, text = 'Score').grid(column = 1, row = 5, sticky = W)
Label(rps_frame, textvariable = player_score).grid(column = 1, row = 6, sticky = W)

Label(rps_frame, text = 'Score').grid(column = 3, row = 5, sticky = W)
Label(rps_frame, textvariable = computer_score).grid(column = 3, row = 6, sticky = W)

Label(rps_frame, textvariable = result_set).grid(column = 2, row = 7)

if __name__ == '__main__':
    gui()
```
```

the window, and the sticky allows us to justify items with specific directions – in this case top, left, right and bottom justification. Finally, we then make sure each column and row is treated equally by giving them the same weighting, and starting from zero.

## 22 Player’s choice

We create a label for the player’s move and assign it to a grid location, on the first row, on the first column. We also justify it to the left using ‘sticky = W’. We then add the radio buttons for the player’s move, each on the same column but the following row down. We give each choice a name, then assign it to the player_choice variable. We then make each choice have a numerical value that corresponds to the moves we’ve determined in the first set of rules.

## 23 Computer’s move

First of all, we label what this is and then create a second label to display the actual move. We do this by adding the textvariable option to Label, and using the computer_choice variable we updated earlier in the game function. This merely prints the text from the names list and justifies this to the left.

## 24 Press Play

The running of the code all hinges on the Play button. It’s very simple: we put it in the row between the Player and Computer move as part of our three-column system; and it runs the start function using the command option. Due to the loop of the interface, we can keep pressing this without needing to be asked to play again. Simply exiting the window will go back to the main interface window as well, meaning we do not need a specific quit button.

## 25 Running score

We have two sets of scores to display – one for the player and the other for the computer. We label these the same way we’ve done with labelling the Player and Computer move, having them on a lower row but still in the relevant columns. Below that, we use the textvariable option again to get the numerical score we assigned to the separate score variable. Finally, we create another label to display the message for the game’s outcome.

## 26 End game

The final part of the code allows for the script to be used by the main window, and also allows for it to run on its own when used in the command line or shell. You’ll need to perform some modifications to make it run on its own, such as making it the mainloop and not the Toplevel window. However, it will run just fine from both without the need to be launched from the main interface.
