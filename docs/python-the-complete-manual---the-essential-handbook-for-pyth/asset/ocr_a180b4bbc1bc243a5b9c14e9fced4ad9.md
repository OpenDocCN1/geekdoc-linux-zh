# Getting started

# Full code listing

```
#!/usr/bin/env python2

# We're going to write a program that will ask the
user to input an arbitrary
# number of integers, store them in a collection,
# and then demonstrate how the
# collection would be used with various control
structures.

import sys # Used for the sys.exit
function
    target_int = raw_input("How many
integers?")

# By now, the variable target_int contains a string
representation of
# whatever the user typed. We need to try and
convert that to an integer but
# be ready to # deal with the error if it's not.
Otherwise the program will
    # crash.
try:
        target_int = int(target_int)
except ValueError:
        sys.exit("You must enter an
integer")

ints = list()

    count = 0
```

The number of integers we want
in the list

A list to store the
integers

These are used
to keep track
of how many
integers we
currently have

![](bbox=[0.031, 0.584, 0.996, 0.996])