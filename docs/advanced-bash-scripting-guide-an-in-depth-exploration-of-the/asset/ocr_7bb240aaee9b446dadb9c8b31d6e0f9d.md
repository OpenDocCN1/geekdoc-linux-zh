# Advanced Bash-Scripting Guide

Even such unlikely candidates as the vi editor lend themselves to here documents.

# Example 19-2, dummyfile: Creates a 2-line dummy file

```
#!/bin/bash

# Noninteractive use of 'vi' to edit a file.
# Emulates 'sed'.

E_BADARGSGS=85

if [ -z "$1" ]
then
    echo "Usage: basename $0 filename"
    exit $E_BADARGSGS
fi

TARGETFILE=1

# Insert 2 lines in file, then save.
#------Begin document------
$ TARGETFILE <<x23LimitString23
i
This is line 1 of the example file.
This is line 2 of the example file.
^'
ZZ
x23LimitString23
#------End document------
```

# Note that ^ above is a literal escape
# typed by Control-<Esc.

# Bram Moolenaar points out that this may not work with 'vim'
# because of possible problems with terminal interaction.

exit

The above script could have been effectively implemented with ex, rather than vi. Here documents containing a list of ex commands are common enough to form their own category, known as ex scripts.

```
#!/bin/bash
# Replace all instances of "Smith" with "Jones"
# in files with a ".txt" filename suffix.

ORIGINAL=Smith
REPLACEMENT=Jones

for word in $(grep -l $ORIGINAL *.txt)
d
    #
    ex $word <<EOF
    :s/$ORIGINAL/$REPLACEMENT/g
    wq
EOF
    # % is the "ex" substitution command.
    # wq is write-and-quit.
    ------------------------------------
done
```

Chapter 19. Here Documents