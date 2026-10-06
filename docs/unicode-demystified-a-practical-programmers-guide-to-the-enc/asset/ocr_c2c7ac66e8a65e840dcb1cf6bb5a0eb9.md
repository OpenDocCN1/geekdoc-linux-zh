# Special Parameters

Special parameters make it possible to access useful values containing command line arguments and the execution of shell commands. You reference by preceding a special character with a dollar sign ($). As with positional parameters, it is not possible to modify the value of a special parameter.

# $* @@ Value of Command Line Arguments

The $* parameter represents all the command line arguments, as the display_all script on page 582 demonstrates. The $@ and $* parameters are the same except when they are enclosed within double quotation marks. Using "*$" yields a single argument (with SPACES between the positional parameters), whereas "@" produces a list where each positional parameter is a separate argument. This difference makes $@ more useful than $* in shell scripts, as the whos script on page 642 demonstrates.

# ## Number of Command Line Arguments

As the showargs script on page 582 and the following example demonstrate, the $# parameter contains the number of arguments on the command line. This string parameter represents a decimal number.

```
$ cat num_args
echo "This shell script was called with $# arguments."
$ num_args helen alex jenny
This shell script was called with 3 arguments.
```

You can use test to perform logical tests on this number (for information on test, see page 627 and 1352 in Part III; for tcsh refer to "Numeric Variables" on page 701).
The echo builtin in the preceding example displays a quoted string that spans two lines. Because the NEWLINE is quoted, the shell passes the entire string that is between the quotation marks, including the NEWLINE, to echo as an argument.

# $$ PID Number

The shell stores in the $$ parameter the PID number of the process is executing it. In the following interaction echo displays the value of this variable, and the ps utility confirms its value (ps lists a more processes if you are running X). Both commands show that the shell has a PID number of 5209: