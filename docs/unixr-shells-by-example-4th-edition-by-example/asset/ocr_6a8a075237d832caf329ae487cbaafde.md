Although the default name for the history file is .history, its name can be changed by assigning an alternative name to the built-in shell variable, histfile. The history shell variable is set to a number specifying how many commands to display and the histdup variable can be set so that duplicate entries are not added to the history file.

# EXAMPLE 9.74

```
(The Command Line)
> history
1 17:12 cd
2 17:13 ls
3 17:13 more /etc/fstab
4 17:24 /etc/mount
5 17:54 sort index
6 17:56 vi index
```

# EXPLANATION

The history list displays the last commands that were typed at the command line. Each event in the list is preceded with a number (called an event number) and the time that it was entered at the command line.

# The history Variable.

The TC shell history variable can be set to the number of events from the history list that will be displayed on the terminal. Normally, this is set in the /etc/.cshrc or ~/.tcshrc file, the user's initialization file. It is set to 100 by default. You can also provide an optional second value for the history variable to control the way the history is formatted. This value uses the same formatting sequences as the prompt variable. (See Table 9.10.) The default format string for history is %h\t%T\r\n.

# EXAMPLE 9.75

```
1 set history=1000
2 set history=( 1000 '%bh %B%t\n' )
3 history
136 history
137 set history = ( 1000 '%bh %B%t\n' )
138 history
139 ls
140 pwd
141 cal
141 pwd
142 cd
```

# EXPLANATION

+   1 The last 1,000 commands typed at the terminal can be displayed on the screen by typing the history command.