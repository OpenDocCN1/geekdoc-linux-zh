```
trap "commands" signal_list
```

In this form, trap will execute the commands in the quotes when any of the signals corresponding to the numbers in the signal_list is received by the script.

To restore signals to their default action, use the trap command in the form:

```
trap signal_list
```

without any commands specified.

The third form, which allows signals to be ignored, has the format:

```
trap "" signal_list
```

which just specifies a null commands string.

A typical example of the use of trap is to clean up temporary files when abnormal termination of a program occurs which might otherwise leave these files cluttering up your file space. The following code fragment assumes that a unique temporary file, called /tmp/tmp$$, is to be created for use within the script and that if abnormal termination of the script occurs, on receipt of either an interrupt or a quit signal, the temporary file needs to be deleted as a clean up operation before the script terminates:

```
trap "rm -f /tmp/tmp$$; exit 0" 2 3
touch /tmp/tmp$$
#
# Rest of shell script here
#
trap 2 3
```

This script starts by setting itself up to trap signals 2 and 3 (Ctrl-c and Ctrl-\ from the keyboard). If either of these two signals occurs, it will usually be because the user is trying to break into the script and abort its operation. After the trap has executed, signals 2 and 3 will cause execution of the commands:

```
rm -f /tmp/tmp$$; exit 0
```

The rm command will remove the temporary file and the exit command then terminates the script. Notice that multiple commands can be entered on the same line if they are separated by semi-colons.

Once the trap command has executed, the rest of the shell script will execute as normal, starting with the creation of the temporary file by the touch command. The last line of this script fragment restores the operation of signals 2 and 3 to their default state, presumably after the temporary file is no longer needed and has thus already been deleted.