# Advanced Bash–Scripting Guide

[17]

# Example 7–4. arithmetic and string comparisons

```
#!/bin/bash

a=4
b=5

# Here "a" and "b" can be treated either as integers or strings.
# There is some blurring between the arithmetic and string comparisons,
# + since Bash variables are not strongly typed.

# Bash permits integer operations and comparisons on variables
# whose value consists of all-integer characters.
# Caution advised.

if [ "$a" -ne "$b" ]
then
    echo "$a is not equal to $b"
    echo "(arithmetic comparison)"
fi

if [ "$a" != "$b" ]
then
    echo "$a is not equal to $b."
    echo "(string comparison)"
fi
```

echo

In this instance, both "-ne" and "!=" work.

echo

exit 0

# Example 7–5. testing whether a string is null

```
#!/bin/bash
# str-test.sh: Testing null strings and unquoted strings,
# but not strings and sealing wax, not to mention cabbages and kings...

# Using if [ ... ]

# If a string has not been initialized, it has no defined value.
# This state is called "null" (not the same as zero).
if [ -n $string1 ]
then
    echo "$string1\ is not null."
else
    echo "$string1\ is null."
fi
# Wrong result.
# Shows $string1 as not null, although it was not initialized.
```

echo

# 7.3. Comparison operators (binary)

50