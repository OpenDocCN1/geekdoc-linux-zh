+   - Catch the signal and perform some signal-specific commands. This method requires the program to define a function that is executed when a signal is received. This is the most complex and powerful method of dealing with a signal.

The first method is the default behavior for all shell scripts. All the scripts that you have looked at thus far handle signals using this method. This section illustrates scripts that use the second and third methods.

# The trap Command

The trap command sets and unsets the action taken when a signal is received. Its syntax is

```
trap name sigs
```

Here name is either a list of commands or the name of a shell function to execute and sigs is a list of signals. When a signal listed in sigs is received by the script, the commands specified by name are executed. If name is omitted, trap resets the action for the given sigs to the default action.

Some common uses for trap are

+   - Clean up temporary files
+   - Always ignore signals
+   - Ignore signals only during critical operations

We will look at a fourth use, setting up a timer, later in this chapter.

# Cleaning Up Temporary Files

If a script creates temporary files, it is common practice to remove these files before the script exits. Most scripts perform this type of cleanup correctly during normal execution, but few scripts perform the appropriate cleanup actions when signals occur. Consider the following script:

```
#!/bin/sh
TMPF=`.arch*
uname -m > $TMPF*
read ARCH < $TMPF*
rm -f $TMPF*
echo $ARCH
exit 0
```

This script creates a temporary file .arch, which is removed before exiting. Under normal circumstances, the temporary file will not be present after the script exits. However,