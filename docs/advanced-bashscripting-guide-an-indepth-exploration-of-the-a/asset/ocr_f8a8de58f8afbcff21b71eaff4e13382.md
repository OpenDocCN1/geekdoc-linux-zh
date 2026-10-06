# Chapter 17. Here Documents

A here document uses a special form of I/O redirection to feed a command script to an interactive program, such as | telnet or ex. Typically, the script consists of a command list to the program, delineated by a limit string. The special symbol << precedes the limit string. This has the effect of redirecting the output of a file into the program, similar to interactive-program < command-file, where command-file contains

```
command #1
command #2
...
```

The "here document" alternative looks like this:

```
#!/bin/bash
interactive-program <<LimitString
command #1
command #2
...
LimitString
```

Choose a limit sufficiently unusual that it will not occur anywhere in the command list and confuse matters.

Note that here documents may sometimes be used to good effect with non-interactive utilities and commands.

# Example 17–1. dummyfile: Creates a 2-line dummy file

```
#!/bin/bash

# Non-interactive use of 'vi' to edit a file.
# Emulates 'sed'.

E_BADARGS=65

if [ -z "$1" ]
then
  echo "Usage: basename $0 filename"
  exit $E_BADARGS
fi

TARGETFILE=$1

# Insert 2 lines in file, then save.
#------Begin here document------
vi $TARGETFILE <<x23LimitStringx23
i
This is line 1 of the example file.
This is line 2 of the example file.
'\nZZ
x23limitStringx23
#------End here document------
```