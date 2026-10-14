![](bbox=[0.07, 0.11, 0.92, 0.55])

# Figure 16-15: Piping the output of ls to the less pager

just press [Q].

Actually, we've already been using pipes, before we even discussed what they were. In previous references to man pages, we used the following to print out the man page entry:

```
man ls | col -b | lpr
```

Here, we're sending the output of man ls to a filter called col with an option of -b to help format the text for the printer, then we sent the output of that to the printer using the lpr command.

+   - Summary: Piping allows you to send the output of one command and as the input of another command. For example: ls -al /etc | more pipes the output of the ls command to the more utility for easy viewing.