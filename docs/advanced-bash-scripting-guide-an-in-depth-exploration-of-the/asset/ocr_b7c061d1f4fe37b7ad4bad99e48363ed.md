# Advanced Bash-Scripting Guide

```
echo
exit 0

# Exercise:
# ------
# Modify this script so it lists itself
#+ in its original format,
#+ complete with whitespace, line breaks, etc.
In an array context, Bash builds have a slightly altered meaning. For example, unset deletes
elements, or even an entire array.
```

# Example 27-6. Some special properties of arrays

```
#!/bin/bash

declare -a colors
# All subsequent commands in this script will treat
#+ the variable "colors" as an array.

echo "Enter your favorite colors (separated from each other by a space)"

read -a colors # Enter at least 3 colors to demonstrate features below.
# Special option to 'read' command,
# allowing assignment of elements in an array.

echo
element_count=${colors[@]}
# Special syntax to extract number of elements in array.
#     element_count=${colors[*]} works also.

# The "*" variable allows word splitting within quotes
# +(extracts variables separated by whitespace).

# This corresponds to the behavior of "$@" and "$*"
#+ in positional parameters.

index=0
while [ "$index" -lt "$element_count" ];
do
    # List all the elements in the array.
    echo ${colors[$index]} also works because it's within ${ } brackets.
    let index=$((index + 1))
    # Or:
    # ((index++))
done
# Each array element listed on a separate line.
# If this is not desired, use echo -n "${colors[$index]}" ""

# Doing it with a "for" loop instead:
# for i in "\${colors[@]}";
do
    echo "\$$i"
done
# (Thanks, S.C.)
```

Chapter 27. Arrays