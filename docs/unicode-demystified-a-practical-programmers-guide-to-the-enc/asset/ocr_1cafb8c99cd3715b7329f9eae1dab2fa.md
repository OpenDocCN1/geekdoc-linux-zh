# Chapter 15 The Shell and Advanced Shell Programming

# print Options (Continued)

-R (raw input) | Ignores the special meaning of the escapes; displays as ordinary characters. Also treats any fields as string arguments, even if they start with a hyphen (except for -n).

-D (directory) | Treats arguments as directory names. Replaces prefixes with ~expressions where appropriate.

-i (insensitive) | Performs case-insensitive sorts. Use the -o or -O option.

-l (line) | Outputs the arguments separated by NEWLINES instead of SPACES. Using the -l option, the example on page 778 can be written as

```
zsh % print -l "Columbus" ships: "\tThe Nina" \n"tThe Pinta" "\tThe Santa Maria"
```

-N (null) | Outputs the arguments separated by NEWLINES. Terminates the final argument with a null.

-P (prompt) | Allows you to use the escape sequences available when setting the PS1 prompt (page 749).

-S | Directs output to history file.

-U | Sends output to file descriptor n. For more information, refer to "File Descriptors" on page 781.

The following example demonstrates the effect of several print options:

```
zsh % print -R -n -p "NEWLINE \will not be recognized"; ; echo "done"
-p NEWLINE \will not be recognized done
zsh % print "NEWLINE \will not be recognized"; echo "done"
NEWLINE
will not be recognized
done
```

You must (almost) always double quotation marks around the arguments to print and echo. Without the quotation marks a \n will be displayed as n. In the preceding example the second command on the first command line to show that the -n option suppresses the trailing NEWLINE. The -R option causes the -p and the \n not to be interpreted as or special characters. The second command line shows what happens without these options. Because the shell quickly erases the command line before displaying another prompt -n if it is the only command on the command line.