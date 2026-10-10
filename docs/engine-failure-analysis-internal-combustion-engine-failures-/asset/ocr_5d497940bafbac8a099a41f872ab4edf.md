# EXAMPLES

| This Command | Does the Following |
| --- | --- |
| dir $pwd | Displays the contents of the current directory. |
| dir `pwd` | Displays the contents of the current directory. |

# History Expansion

The shell keeps track of the commands you have entered. It does so by creating a *history list* in which each command is given a unique identifying number. Although this capability is most useful in shell scripts, you can use history list expansion to insert commands from the history list. This table shows the history expansion command forms you can use.

# HISTORY EXPANSION SYNTAX

| Command Form | Meaning |
| --- | --- |
| In | Enter the *n*th command in the history list. |
| !1 | Enter the previous command. |
| !-n | Enter the *n*th command back from the current command. |
| !string | Enter the most recent command that starts with *string*. |
| !?string? | Enter the most recent command that contains *string*. |
| !?string% | Enter the most recent argument that contains *string*. |
| !$ | Enter the last argument of the previous command. |
| !!string | Enter the previous command and append *string*. |
| !n string | Enter the *n*th command in the history list and append *string*. |
| !(string1)string2 | Enter the most recent command that starts with *string1* and append *string2*. |
| ^string1^string2^ | Change *string1* from the previous command to *string2*, and execute command. |