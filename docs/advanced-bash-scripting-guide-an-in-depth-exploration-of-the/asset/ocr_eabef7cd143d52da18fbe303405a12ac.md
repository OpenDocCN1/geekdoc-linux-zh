# Advanced Bash-Scripting Guide

```
if [ -z $1 ]
then
    echo "Usage: $0 number"
    exit $E_NOARGS
fi

if [ "$1" -lt "$MIN" ]
then
    echo "Number to factor must be $MIN or greater."
    exit $E_TOOSMOALL
fi

# Exercise: Add type checking (reject non-integer arg).
echo "Factors of $1:"
#
echo "$1[p2]s[2]|lip/di%0-1dsvr]s12sid2%0=s12dsvr[di%0-l1rl1l2-ds!]..ds,xd1<2" | dc
# Above code written by Michel Chapert <charpov@cs.unh.edu>
# (as a one-liner, here broken into two lines for display purposes)
# Used in ABS Guide with permission (thanks!).

exit

# $ sh factor.sh 270138
# 2
# 3
# 11
# 4093
```

Yet another way of doing floating point math in a script is awk's built-in math functions in a shell wrapper.

# Example 16-53. Calculating the hypotenuse of a triangle

```
#!/bin/bash
# hypotenuse.sh: Returns the "hypotenuse" of a right triangle.
#    (square root of sum of squares of the "legs")

ARGS=2
# Script needs sides of triangle passed.
E_BADGARS=85
# Wrong number of arguments.
if [ $# -ne "$ARGS" ] # Test number of arguments to script.
then
    echo "Usage: basename $0 side_1 side_2"
    exit $E_BADGARS
fi

AWKSCRIPT=' printf("%.3.7f\n", sqrt($1*$1 + $2*$2) ) '
# / parameters passed to awk

# Now, pipe the parameters to awk.
echo -n "Hypotenuse of $1 and $2 = "
echo $1 $2 | awk "$AWKSCRIPT"\^^^^^^^^"
# An echo-and-pipe is an easy way of passing shell parameters to awk.
```

Chapter 16. External Filters, Programs and Commands