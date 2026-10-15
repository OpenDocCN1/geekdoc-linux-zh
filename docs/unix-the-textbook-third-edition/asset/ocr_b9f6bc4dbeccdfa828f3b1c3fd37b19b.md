# EXERCISE 9.7

Write a command to copy a file Scores to Scores.bak and send a sorted version of Scores to professor@university.edu via the mail command.

# EXERCISE 9.8

Write a C shell command for copying a file Phones in your home directory to a file called Phones.bak (also in your home directory) by using the cat command and the >& operator.

The C shell has a special built-in variable that allows you to protect your files from being overwritten with output redirection. This variable is called noclobber and, when set, prevents the overwriting of existing files with output redirection. You can set the variable by using the set command and unset it by using the unset command. Or, you can place the set noclobber command in your ~/.cshrc file (or some other startup file).

```
% set noclobber
[y our interactive session]
...
% unset noclobber
%
```

If the noclobber variable is set, the command cat file1 > file2 generates an error message if file2 already exists. If file2 does not exist, it is created and the data from file1 is copied into it. The command cat file1 >> file2 works if file2 exists and noclobber is set, but an error message is generated if file2 does not exist. You can use the >, >>!, and >>&! operators to override the effect of the noclobber variable if it is set. Therefore, even if the noclobber variable is set and file2 exists, the command cat file1 >! file2 copies data from file1 to file2. For the cat file1 >>! file2 command, if the noclobber variable is set and file2 does not exist, file2 is created and the data from file1 is copied into it. The >>&! operator works in a manner similar to the >>! operator.

# 9.14 RECAP OF I/O AND ERROR REDIRECTION

Table 9.1 summarizes the input, output, and error redirection operators in the Bourne, Korn, and C shells. We did not discuss some of these operators in this chapter; we discuss them in detail in Chapters 12 through 15 under shell programming. We included these operators in this table because it seems to be the most appropriate place to show all of them together. Note that all of the operators that work for the Bourne and Korn shells work for the Bash shell also.

# 9.15 FIFOS

FIFOs, also known as named pipes, can also be used for communication between two processes executing on a system. Whereas processes communicating with pipes must be related to each other through a common ancestor process that you execute, processes