# Advanced Bash–Scripting Guide

```
tcsh$ echo $SHELL
/bin/tcsh
tcsh$ echo $TERM
rxvt

bash$ echo $LOGNAME
bozo
bash$ echo $SHELL
/bin/tcsh
bash$ echo $TERM
rxvt
```

# Positional Parameters

$0, $1, $2, etc.

positional parameters, passed from command line to script, passed to a function, or set to a variable (see Example 5–5 and Example 11–10)

$#

number of command line arguments [191] or positional parameters (see Example 34–2)

$*$

All of the positional parameters, seen as a single word

$0

Same as *, but each parameter is a quoted string, that the parameters are passed on intact, without interpretation or expansion. This means, other things, that each parameter in the argument list is seen as a separate word.

# Example 9–6. listing arguments with $* and @@

```
#!/bin/bash
# Invoke this script with several arguments, such as "one two three".n
E_BADARGS=65

if [ -n "$1" ]
then
    echo "Usage: basename $0" argument1 argument2 etc."
    exit $E_BADARGS
fi

echo
index=1
echo "Listing args with \"\*\:\*"
for arg in "$*" # Doesn't work properly if "$*" isn't quoted.
do
    echo "Arg \$index = $arg"
```

# Chapter 9. Variables Revisited