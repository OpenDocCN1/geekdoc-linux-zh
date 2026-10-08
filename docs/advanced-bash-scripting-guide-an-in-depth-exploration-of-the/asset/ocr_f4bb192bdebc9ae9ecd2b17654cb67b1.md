# Advanced Bash-Scripting Guide

```
echo "---"

for ((i=START; i<=END; i++))
do
    echo $i | awk '{printf("%3d %%2x %%c\n", $1, $1, $1}'
    # Bash printf builtin will not work in this context:
    printf "%%c" "$i"
done
```

| Decimal | Hex | Character |
|---|---|---|
| 33 | 21 | ! |
| 34 | 22 | " |
| 35 | 23 | # |
| 36 | 24 | $ |

# Redirect the output of this script to a file
# or pipe it to "more": sh pr-asc.sh | more

# Example 36-5. A shell wrapper around another awk script

```
#!/bin/bash

# Adds up a specified column (of numbers) in the target file.
# Floating-point (decimal) numbers okay, because awk can handle them.

ARGS=2
E_WRONGARGS=85

if [ $# -ne "$ARGS" ]; then Check for proper number of command-line args.
then
    echo "Usage: basename $0 filename column-number"
    exit $E_WRONGARGS
fi

filename=$1
column_number=$2

# Passing variables to the awk part of the script is a bit tricky.
# One method is to strong-quote the Bash-script variable
# within the awk script.
awk "$BASH_SCRIPT_VAR*"
# This is done in the embedded awk script.
# See the awk documentation for more details.

# A multi-line awk script here is invoked by
awk
```

# Chapter 36. Miscellany

506