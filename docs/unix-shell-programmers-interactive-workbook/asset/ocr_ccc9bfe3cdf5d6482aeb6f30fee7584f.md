# Lab 4.2: Evaluating and Assigning Values

c) What does this command do?

You can see an individual variable's entry in the shell's list of variables by piping the output of set to a grep command.

# FOR EXAMPLE

The following command line will print the line for the variable RANDOM that you looked at earlier:

```
set | grep ^RANDOM=
```

The UNIX grep is used to find strings in files (stdin). If you aren't already familiar with this command, you can get an idea of how to use it by working through this and other exercises in this book. But grep is one of the most commonly used UNIX commands in shell programs, so you should study your UNIX reference material to become familiar with its rich set of features. Or better yet, pick up the UNIX Awk, Sed, and Grep Interactive Workbook by Peter Patis (Prentice Hall, 1999). It's one of the “tools of the trade” that you will use a lot.

![](bbox=[0.135, 0.445, 0.235, 0.515])

Unfortunately, there are several different versions of the grep command that have different rules for constructing the regular expressions (or patterns) the command searches for. Each has its own special uses.To avoid confusion in this book, we'll only use those grep commands that should work with all versions, even if they are not as fast or elegant as using a different version.

![](bbox=[0.135, 0.642, 0.235, 0.712])

Run the previous command, and observe the output.