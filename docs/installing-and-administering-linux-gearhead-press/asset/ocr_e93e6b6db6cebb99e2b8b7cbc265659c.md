example, if you are testing a procedure or performing several repetitive operations) need to re-enter commands that are identical or similar to those you have previously entered. In this section, we'll introduce three commands which, over time, will save you a lot of time and countless keystrokes: history, fc, and ! (which is called “bang”). All three can reduce your frustration and speed your progress, especially on those busier days.

# The history Command

The history command reads, numbers, and displays the text of the previous commands from the buffer and also from the .bash_history file in the user’s home directory or from whatever file is named as a value for the HISTFILE variable (we discuss environment variables such as HISTFILE later in Chapter 11, “Shell Variables and the User Environment”). The default value is HISTFILE=$HOME/.bash_history, but you can change the default by adding or modifying HISTFILE=filename to your $HOME/bash_profile file.

The maximum number of commands that history can access is the number of commands already in the buffer from the current session plus the number of commands stored in the $HOME/.bash_history file. The maximum size of that file is specified in the HISTFILESIZE variable. The maximum number of previous commands that history can display, however, is the number specified in the HISTSIZE variable. If no number is specified, the default is 17 (although many reference materials say 16).

The history command has several options and arguments. For example, history -a appends the current session’s commands to the .bash_history file immediately and not upon your logout. Another example is history n, which displays only the previous n commands as long as n is less than or equal to the value of the HISTSIZE variable. For further information, check your information sources.

# The fc Command

You can also use the fc command to display your command history as well as to edit those commands. Used with its options and arguments, fc can be handier than history. For example, fc -1 5 120 lists all previous commands in your history list sequentially from number 5 to number 120. To list the same commands but in reverse order, use fc -1 -r 5 120. The limitations on this maneuverability are, like HISTSIZE, HISTFILESIZE, and other variable values must accommodate what you want to do.