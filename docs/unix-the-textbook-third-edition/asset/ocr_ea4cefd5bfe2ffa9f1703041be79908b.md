![](bbox=[0.35, 0.09, 0.75, 0.65])

FIGURE 9.16 Semantics of the cat names students | grep "John Doe" | tee file1 file2 | wc -l command.

# SYNTAX

```
command >& file
```

Purpose: Redirect stdout and stderr of command to file

For example, the following command redirects output and errors of the ls -l foo command to the error.log file. The standard input of the command is still attached to the keyboard. Note that we have used the % sign as the shell prompt, which is the default for the C shell.

```
% ls -l foo >& error.log
%
```

The C shell does not have an operator to redirect stderr alone. However, the stdout and stderr of a command can be attached to different files, if the command is executed in a