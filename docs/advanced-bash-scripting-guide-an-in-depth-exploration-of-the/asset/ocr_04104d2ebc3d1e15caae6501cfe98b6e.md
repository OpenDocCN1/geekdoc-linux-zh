# Advanced Bash-Scripting Guide

```
echo "----------------------------------"
# starting at position # 1 (2nd character)
echo ${#array[0]}      # 4
# Length of first element of array.
echo ${#array}         # 4
# Length of first element of array.
# (Alternate notation)

echo ${#array[1]}      # 3
# Length of second element of array.
# Arrays in Bash have zero-based indexing.

echo ${#array[*]}      # 6
# Number of elements in array.
echo ${#array[@]}      # 6
# Number of elements in array.

echo "----------------------------------"
array2=( [0]="first element" [1]="second element" [3]="fourth element" )
# Quoting permits embedding whitespace within individual array
echo ${array2[0]}      # first element
echo ${array2[1]}      # second element
echo ${array2[2]}      # 
echo ${array2[3]}      # fourth element
# Skipped in initialization, and therefore null.
echo ${#array2[0]}      # 13 (length of first element)
echo ${#array2[*]}      # 3 (number of elements in array)
exit
```

Many of the standard string operations work on arrays.

# Example 27-4. String operations on arrays

```
#!/bin/bash
# array-strops.sh: String operations on arrays.

# Script by Michael Zick.
# Used in ABS Guide with permission.
# Fixups: 05 May 2008, 04 Aug 08.
```

> # In general, any string operation uses the ${name} ... notation
## can be applied to all string elements in an array,
## with the ${name[@]} ... ) or ${name[*]} ... notation.

```
array2={ one two three four five }
echo

# Trailing Substring Extraction
echo ${array2[@]:0}0      # one two three four five
# All elements.
```

Chapter 27. Arrays

430