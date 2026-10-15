```
# to re-enter his/her code just to make sure that
# the user remembers the code that he/she has
# entered. It is done twice. If the user does not
# enter the same code, the program terminates
# after displaying a message for the user. The
# user is prompted to enter the original code. If
# the user enters the wrong code, the program
# keeps on prompting the user until he/she enters
# the original code. The keyboard is then unlocked,
# echo is turned on, and program exits, allowing
# the user to use his/her system again.
# Ignore terminal interrupt
onintr -

# Clear the screen, locate the cursor at the top-left corner,
# and turn off echo
clear
stty -echo

# Set the secret code
echo -n "Enter your code word: "
set secretcode = `head -1`
echo ""

# To make sure that the user remembers the code word
echo -n "Enter your code word again: "
set same = `head -1`
echo ""
if ( $secretcode != $same ) then
echo "Work on your short-term memory before using this code!"
exit 1
endif

# Keyboard locked. Hit <Enter> to continue.
clear
echo -n "Keyboard locked. Hit <Enter> to continue."
set ignore = `head -1`
clear

# Get user guess to unlock the terminal
echo -n "Enter the code word: "
set yourguess = `head -1`
echo ""

# As long as the user input is not the original code word, loop
# here: display a message and take user input gain. When the user
# input matches the secret code word, terminate the loop and
# execute the following echo command.
```