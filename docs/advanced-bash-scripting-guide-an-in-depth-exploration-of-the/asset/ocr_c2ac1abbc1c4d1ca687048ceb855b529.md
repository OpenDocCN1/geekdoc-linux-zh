# Advanced Bash-Scripting Guide

```
string1=initialized
if [ $string1 ] # Again, $string1 stands unquoted.
then
    echo "\$string1\" is not null.
else
    echo "\$string1\" is null. # Again, gives correct result.
fi

# Still, it is better to to quote it ("$string1"), because . .
```

```
string1="a = b"
if [ $string1 ] # Again, $string1 stands unquoted.
then
    echo "\$string1\" is not null.
else
    echo "\$string1\" is not null.
fi
# Not quoting "$string1" now gives wrong result!

exit 0 # Thank you, also, Florian Wisser, for the "heads-up".
```

# Example 7-7. zmore

```
#!/bin/bash
# zmore

# View zipped files with 'more' filter.

E_NOARGS=85
E_NOTFOUND=86
E_NOTZIP=8

if [ $ -eq 0 ] # same effect: as if [ -z "$1" ]
# $1 can exist, but be empty: zmore "" arg2 arg3
then
    echo "Usage: basename \$filename" >&2
    # Error message to stderr.
    exit $E_NOARGS
    # Returns 85 as exit status of script (error code).
fi

filename=1
if [ ! -f "$filename" ] # Quoting $filename allows for possible spaces.
then
    echo "File $filename not found!" >&2 # Error message to stderr.
    exit $E_NOTFOUND
fi

if [ ${filename##*.}] != "gz" ]
# Using bracket in variable substitution.
then
    echo "File $1 is not a zipped file"
    exit $E_NOTZIP
fi

zcat $1 | more
```

Chapter 7. Tests

69