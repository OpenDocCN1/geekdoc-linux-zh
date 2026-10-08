# history, fc

When you edit commands and you did not specify the -l option, the resulting lines are entered at the end of the history list and then reexecuted by sh. The fc editing command is not entered into the history list. If the editor returns a non-zero exit status, this status suppresses the entry into the history list and the command reexecution. command-line variable assignments or redirection operators used with fc affect both the fc command itself as well as the command that results. For example, the following command revokes the previous command, suppressing standard error for both fc and the previous command.

```
$ fc -s -- 2>//dev/null
```

# C Shell

Use the history command to display the history list; if you specify the number n display only the n most recent events.

+   -h Display the history list without leading numbers. Use this option to produce files suitable for sourcing with the -h option to the csh built-in source(1) command.

+   -r Reverse the order of printout to be most recent first instead of oldest first.

If you use any of the options together with n, specify the options first.

# History Substitution

History substitution enables you to use words from previous commands in the line you are typing. This substitution simplifies spelling corrections and the repetition of complicated commands or arguments. Command lines are saved in the history list, the size of which is controlled by the history variable. You can set the history variable to specify the maximum number of command lines that are saved in the history file; for example, the following command enables the history list to keep track of the most recent 200 lines.

```
castle set history = 200
```

If the history variable is not set, the C saves only the most recent command. Begin a history substitution with !(although you can change this character with the histchars variable). The ! can occur anywhere on the command line; history substitutions do not nest. You can escape the ! with a backslash (\) to suppress its special meaning.

Input lines containing history substitutions are echoed on the terminal after being expanded before any other substitutions take place or the command is executed.

# Event Designators

An event designator is a reference to a command-line entry in the history list.

+   ! Start a history substitution, except when followed by a space character, Tab, newline, or (.

+   !! Refer to the previous command. By itself, this substitution repeats the previous command.

+   !n Refer to command line n.

+   !-n Refer to the current command minus n.

+   !str Refer to the most recent command starting with str.