# Advanced Bash-Scripting Guide

```
# -----------
# Convert this to an interactive script,
# that is, have the script ask for input (two numbers).
```

For a function to return a status or array, use a dedicated variable.

```
count_lines_in_etc_passwd()
{
    [[ -r /etc/passwd ]] && REPLY=$(echo $(wc -l </etc/passwd))
    # If /etc/passwd is readable, set REPLY to line count.
    # Returns both a value and status information.
    # The 'echo' seems unnecessary, but . .
    # + it removes whitespace from the output.
}

if count_lines_in_etc_passwd
then
    echo "There are $REPLY lines in /etc/passwd."
else
    echo "Cannot count lines in /etc/passwd"
fi

# Thanks, S.C.
```

# 24-8. Converting numbers to Roman numerals

```
#!/bin/bash

# Arabic number to Roman numeral conversion
# Range: 0 - 200
# It's crude, but it works.

# Extending the range and otherwise improving the script is left as an exercise.

# Usage: roman number-to-convert
```

```
LIMIT=200
E_ERR=65
E_OUT_OF_RANGE=66

if [ -z "$1" ];
then
    echo "Usage: basename $0 number-to-convert"
    exit $E_ERR
fi

num=$1
if [ "$num" -gt $LIMIT ];
then
    echo "Out of range!"
    exit $E_OUT_OF_RANGE
fi

to_roman() {
    # Must declare function before first call to it.
    number=$1
    factor=$2
    rchar=$3
    let remainder = number - factor
    while [ "$remainder" -ge 0 ]
```

24. Functions

407