```
exit 55
Ctrl-d
$ chmod 700 tryexit
$ tryexit
$ echo $?
55
```

The variable $? is just one of several special variables used by bash for various status applications and which are available within a shell script. The main ones are:

+   - $? This variable holds the exit status returned by the last command to be executed by the shell.
- $$ This variable contains the PID of the current shell. This value is very often used for generating unique temporary file names for use within the script (e.g. /tmp/tmp$$).
- $# This holds the number of command line parameters that were passed to the current script. This value corresponds to the number of the $1, $2, etc., variables currently in use.
- $* This variable contains a list of all command line parameters ($1, $2, etc.) that were passed to the current script.

Each of these special variables may only have its value read. Assignment to them is not allowed, except by the shell, which automatically updates them as given in the previous table.

# 6.7 Flow Control

In common with other high level programming languages, the shell provides a set of commands which are used to control the flow of execution around the code. These include several selection and looping constructs which allow really sophisticated programs to be constructed.

As you will see, the only slightly unusual thing about these constructs is the way that commands and strings are used to specify conditional values, where in a more conventional language a boolean expression would be used.

# 6.7.1 if Command

You have seen that when the shell executes a command or pipeline, an exit status is returned. One way to determine what action is to be performed next is to use a construct which can test the value returned by a command and use it to make a