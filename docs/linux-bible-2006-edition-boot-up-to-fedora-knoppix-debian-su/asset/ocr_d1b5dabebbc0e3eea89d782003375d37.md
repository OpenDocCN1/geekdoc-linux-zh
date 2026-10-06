# 46 Part I ♦ Linux First Steps

The first example causes $OS to expand to the $OSTYPE variable. In the next example, ~ro expands to the user's home directory (~root/). Next, fing expands to the finger command, the address of root@ expands to computer name localhost.

Of course, there will be times there are several possible completions for the string of characters you have entered. In that case, you can check the possible ways text can be expanded by pressing Esc+? (or by pressing Tab twice) at the point where you want to do completion. This shows the result you get if you checked for possible completions on $P.

```
$ echo Esc+?
$PATH PPID $PS1 PS2 PS4 $PWD
$ echo $
```

In this case, there are six possible variables that begin with $P. After possibilities are displayed, the original command line returns, ready for you to complete it as you choose.

If you want to complete is not preceded by a $, ~, or @, you can still try to complete the text with a variable, username, or host name, as shown in Table 2-4.

| Table 2-4
Key Combinations for Text Completion |
| Press Key Combination | To |
| Alt+~ | Complete the text before this point as a username. |
| Alt+$ | Complete the text before this point as a variable. |
| Alt+@ | Complete the text before this point as a host name. |
| Alt+! | Complete the text before this point as a command name (alias, referred shell, shell function, built-in command, and filenames are checked in order). In other words, complete this key sequence with a command that previously ran. |
| Ctrl+X+/ | List possible username completions. |
| Ctrl+X$ | List possible environment variable completions. |
| Ctrl+X@ | List possible host name completions. |
| Ctrl+X! | List possible command name completions. |