# EXPLANATION (CONTINUED)

+   4 The value stored in the line variable is printed to the screen.
+   5 The user is asked if the word is correct.
+   6 The read command gets the user's response from the terminal, /dev/tty. If the input is not redirected directly from the terminal, it will continue to be read from the file tmp, still opened for input.
+   7 The user is again asked for input, and the input is redirected from the terminal, /dev/tty.
+   8 The new word is displayed.

# 12.6.11 The IFS and Loops

The IFS, the shell's internal field separator, evaluates to spaces, tabs, and the newline character. It is used as a word (token) separator for commands that parse lists of words such as read, set, for, and select. It can be reset by the user if a different separator will be used in a list. It is a good idea to save the original value of the IFS in another variable before changing it. Then it is easy to return to its default value.

# EXAMPLE 12.49

(The Script)

```
#!/bin/ksh
# Scriptname: runit
# IFS is the internal field separator and defaults to
# spaces, tabs, and newlines.
# In this script it is changed to a colon.

1 names=Tom:Dick:Harry:John
2 OLDIFS="$IFS"      # Save the original value of IFS
3 IFS=":"
4 for persons in $names
do
5     print Hi $persons
done
6 IFS="$OLDIFS"      # Reset the IFS to old value
7 set Jill Jane Jolene   # Set positional parameters
8 for girl in $*
do
    print Howdy $girl
done
```