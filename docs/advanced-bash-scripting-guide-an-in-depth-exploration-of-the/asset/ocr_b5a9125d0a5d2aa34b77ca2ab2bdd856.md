# Advanced Bash-Scripting Guide

```
echo "----------------------"; echo
var=41 # Global variable
( let "var=1"; echo "$var INSIDE subshell = $var" ) # 42
echo \$var OUTSIDE subshell = $var* # 41
# Variable operations inside a subshell, even to a GLOBAL variable
# + do not affect the value of the variable outside the subshell!
```

```
exit 0

# Question:
#
# Once exiting a subshell,
# + is there any way to reenter that very same subshell
# + to modify or access the shell variables?
See $BASHPID and Example 3-2
```

**Definition**: The scope of a variable is the context in which it has meaning, for example, the scope of a local variable lies only within the function, block of code, subshell within which it is defined, while the scope of a global variable is the entire script in which it appears.

While the $BASH SUBSHELL internal variable indicates the nesting level of a subshell, the $SHLVL variable shows no change within a subshell.

```
echo "$BASH_SUBSHELL outside subshell = $BASH_SUBSHELL" # 0
( echo "$BASH_SUBSHELL inside subshell = $BASH_SUBSHELL" ) # 1
( echo "$BASH_SUBSHELL inside nested subshell = $BASH_SUBSHELL" ) # 2
*** ***
```

```
echo
echo $SHLVL outside subshell = $SHLVL # 3
( echo "$SHLVL inside subshell = $SHLVL" ) # 3 (No change!)
```

Directory changes in a subshell do not carry over to the parent shell.

# Example 21-2. List User Profiles

```
#!/bin/bash
# allprofs.sh: Print all user profiles.

# This script written by Helner Steven, and modified by the document author.

FILE=.bashrc # File containing user profile,
# += ".profile" in original script.

for home in $(awk -F: '{print $6}' /etc/passwd)
do
[ -d "$home" ] || continue # If no home directory, go to next.
[ -r "$home" ] || continue # If not readable, go to next.
(cd $home; -e $FILE) && less $FILE
```

Chapter 21. Subshells