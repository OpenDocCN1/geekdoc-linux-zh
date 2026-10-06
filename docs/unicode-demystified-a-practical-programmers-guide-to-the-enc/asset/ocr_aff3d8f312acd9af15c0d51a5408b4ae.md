# # Expansion and Substitution (Continued)

| Filename generation | Replaces pathnames that contain filename-matching patterns with their expanded lists of pathnames (page 805). |

The order in which zsh carries out these steps affects the interpretation of the commands you enter. For example, if you set a variable to a value that looks like the instruction for output redirection and you enter a command using the variable's value to perform redirection, you might expect zsh to redirect the output:

```
zsh % SENDIT=" /tmp/saveit
zsh % echo xxx $SENDIT
xxx > /tmp/saveit
zsh % cat /tmp/saveit
cat: No such file or directory
```

This does not work. The Z Shell recognizes input and output redirection before it evaluates variables. When it executes the command line, the Z Shell checks for redirection, and finding none, goes on to evaluate the SENDIT variable. After replacing the variable with > /tmp/saveit, zsh passes the arguments to echo, which dutifully copies its arguments to standard output. No /tmp/saveit file is created.

The following sections provide more detailed descriptions of each the steps involved in command processing.

# # History Expansion

The Z Shell provides a history mechanism similar to that found in tsh. This mechanism allows you to refer to words found in previous commands without having to retype them. A use of the history mechanism is called a history event and always starts with an exclamation point (!). Table 15-22 gives the various types of history events that you can use with the Z Shell. You can put history events anywhere on a command line. To escape an exclamation point so it is treated literally instead of the start of a history event, precede it with a backslash (\). Neither single nor double quotation marks prevent history substitution.

# # Event Specifier

| ! | Starts a history event unless followed immediately by a SPACE, NEWLINE, =, or (. |