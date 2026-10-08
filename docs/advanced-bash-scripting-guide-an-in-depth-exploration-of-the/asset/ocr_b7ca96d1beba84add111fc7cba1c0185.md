# Advanced Bash-Scripting Guide

```
[ $ -eq 0 ] && $prefix"
# Every time we jump back add a 'blank' line
return $E_BL
# We return 80 to tell we added a blank line already.\}
```

```
### ### ###
### main program ###
### ### ###
rootdir="$"
[ -d "$rootdir" ] || \
echo $SELF: Usage: $SELF <directory> >&2; exit $E_DIR;
# We should be called with a directory name.
```

```
echo "Building inventory list, please wait..."
# Show "wait" message.
-akx "rootdir" 1 "$TMP" 2>/dev/null
# Build a temporary list of all files and their sizes
size=$(tail -1 "$TMP" | awk '{print $1}')
# What is our rootdirectory's size?
echo "Size: $size $rootdir"
# Display rootdirectory's entry.
tree 0 "0" "$rootdir"
# Display the tree below our rootdirectory.
```

```
rm "$TMP" 2>/dev/null
# Clean up $?
exit $?
```

Noah Friedman permitted using his string script. It essentially reproduces some of the C-library string manipulation functions.

# Example A-18. string functions: C-style string functions

```
#!/bin/bash

# string.bash --- emulation of string(3) library routines
# Author: Noah Friedman <friedman@prep.ai.mit.edu>
# -->
Used with his kind permission in this document.
# Created: 1992-07-01
# Last modified: 1992-09-29
# Public domain
```

```
# Conversion to bash v2 syntax done by Chet Ramey

# Commentary:
# Code:
```

```
#:string strcat:
# Usage: strcat sl s2

# Strcat appends the value of variable s2 to variable sl.

# Example:
a="foo"
b="bar"
strcat a b
```

Appendix A. Contributed Scripts