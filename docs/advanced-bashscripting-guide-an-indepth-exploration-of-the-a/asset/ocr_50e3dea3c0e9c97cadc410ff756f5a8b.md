# Advanced Bash–Scripting Guide

```
let "index+=1"
dnecho # $@ sees all arguments as single word.
done
echo "Entire arg list seen as single word."
echo
index-1=
echo "Listing args with \\$@":"
for arg in "$@"
do
echo "Arg $index = $arg"
  let "index+=1"
done
echo # $@ sees arguments as separate words.
echo "Arg list seen as separate words."
echo
exit 0
```

Following a shift, the $@ holds the remaining command-line parameters, lacking the previous $1, which was lost.

```
#!/bin/bash
# Invoke ./scriptname 1 2 3 4 5
echo "$@" 1 2 3 4 5
shift
echo "$@" 2 3 4 5
shift
echo "$@" 3 4 5

# Each "shift" loses parameter $1.
# "$@" contains the remaining parameters.
```

The special parameter finds a use for filtering input into shell scripts. The cat "$@" construction accepts input to a script either from stdin or from files as parameters to the script. See Example 12-17 and Example 12-18.

The $* and $@ parameters sometimes display inconsistent and puzzling behavior, depending on the setting of $IFS.

# Example 9–7. Inconsistent *$ and $@ behavior

```
#!/bin/bash
# Erratic behavior of the "$*" and "$@" internal Bash variables,
# depending on whether these are quoted or not.
# Word splitting and linefeeds handled inconsistently.

# This example script by Stephane Chazelas,
# and slightly modified by the document author.

set -- "First one" "second" "third:one" "Fifth: :one"
# Setting the script arguments, $1, $2, etc.
```

Chapter 9. Variables Revisited