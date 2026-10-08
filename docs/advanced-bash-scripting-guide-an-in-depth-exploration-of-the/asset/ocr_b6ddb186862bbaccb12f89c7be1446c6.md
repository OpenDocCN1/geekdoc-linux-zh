# Advanced Bash-Scripting Guide

This is the rough equivalent of the C const type qualifier. An attempt to change the value of a readonly variable fails with an error message.

```
declare -r varl=1
echo varl = $varl    # varl = 1

(( varl++ ))
# x.sh: line 4: readonly variable
```

-i integer

```
declare -i number
# The script will treat subsequent occurrences of "number" as an integer.

number=3
echo Number = $number    # Number = 3

number-three
echo Number = $number    # Number = 0
# Tries to evaluate the string "three" as an integer.
```

Arithmetic operations are permitted for declared integer variables without the need for expr or let.

```
n=6/3
echo "n = $n"    # n = 6/3

declare -i n
n=6/3
echo "n = $n"    # n = 2
```

-a array

```
declare -a indices
The variable indices will be treated as an array.
```

-f function(s)

```
declare -f
A declare -f line with no arguments in a script creates a listing of all the functions defined in this script.
```

```
declare -f function_name
A declare -f function_name in a script lists the function named.
```

-x export

```
declare -x var3
This declares a variable as available for exporting the environment of the script itself.
```

-x var=$value

```
declare -x var3=373
The declare command permits assigning a value to a variable in the same statement as setting its properties.
```

# Example 9-10. Using declare to type to variables

```
#!/bin/bash
```

Chapter 9. Another Look at Variables