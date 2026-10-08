# Advanced Bash-Scripting Guide

-N
file modified since it was last read

f1 -nt f2
file f1 is newer than f2

f1 -ot f2
file f1 is older than f2

f1 -ef f2
files f1 and f2 are not hard links to the same file

!
"not" -- reverses the sense of the tests above (returns true if condition absent)

# Chapter 7-4. Testing for broken links

```
#!/bin/bash
# broken-link.sh
# Written by Lee bigelow <ligelowbee@yahoo.com>
# Used in ABS Guide with permission.

# A pure shell script to find dead symbols and output them quoted
# so they can be fed by xargs and deal with :
# eg. sh broken-link.sh /somedir/someotherdir|xargs rm

# This, however, is a better method:

# find somedir -type l -1 -print0|\nxargs -r0 file|\ngrep "broken symbolic"|\nsed -e 's/\\:broken symbolic.*\\"/g'

# but that wouldn't be pure Bash, now would it.
# Caution: beware the /proc file system and any circular links!
############################################################################
```

```
# If no args are passed to the script set directories-to-search
# to the current directory. Otherwise set the directories-to-search
# to the args passed.
############################################################################

[ -eq 0 ] && directorys=\`pwd\` | || directorys=$@
```

```
# Setup the function linkchk to check the directory it is passed
# for files that are links and don't exist, then print them quoted.
# If one of the elements in the directory is a subdirectory then
# send that subdirectory to the linkchk function.
############################################################
```

```
linkchk() {
  for element in \$@; do
    [ -d "$element" ] -a -e "$element" && echo "$element"
    [ -d "$element" ] 44 linkchk $element
    # OF course, '-h' tests for symbolic link, '-d' for directory.
  done
}
```

```
# Send each arg that was passed to the script to the linkchk() function
# if it is a valid directory. If not, then print the error message
```

# Chapter 7. Tests