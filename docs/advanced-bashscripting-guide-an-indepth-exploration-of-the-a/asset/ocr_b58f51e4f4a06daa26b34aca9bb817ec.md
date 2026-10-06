# Advanced Bash–Scripting Guide

```
# The author of this script explains the action of 'sed', as follows.

# head -c4 /dev/urandom | od -NA -tu4 | sed -ne '1s/..* //p'
#                                            

# Assume output to "sed" |------>
# is 0000000 1198195154n

# sed begins reading characters: 0000000 1198195154n.
# Here it finds a newline character,
# so it is ready to process the first line (0000000 1198195154).
# It looks at its <range><a>-s. The first and only one is

# range           action
# 1               s/. // pp

# The text line is in the range, it executes the action:
# tries to substitute the longest string with a space in the line
# ("0000000" with nothing (//), and if it succeeds, prints the result
# ("*p" is a flag to the "s" command, which is different from the "p" command

# sed is now ready to continue reading its input. (Note that before
# continuing, if -n option had not been passed, sed would have printed
# the line once).

# Now, sed reads the remainder of the characters, and finds the end of the file.
# It is now ready to process its second line (which is also numbered '$') as
# it's the last one.
# it sees no matched by <range>, so its job is done.

# In few this sed command means:
# "On the first line only, remove any character up to the right-most space,
# then print it."

# A better way to do this would have:
# sed -e '$s/. //q'

# Here, two <range><a>-s (could have been written
# sed -e '$s.*/' -e q):

# range           action
# nothing (matches line)  s/. //
# nothing (matches line)  q (quit)

# sed, only reads its first line of input. (substituted) before quitting
# It performs both actions, and prints the line (because of the "q" command)
# since the "-n" option is not passed.


# A simpler alternative to the above 1-line script would be:
# head -c4 /dev/urandom od -An -tu4

exit 0
```

See also Example 12–28.

# 12. 4. Text Processing Commands