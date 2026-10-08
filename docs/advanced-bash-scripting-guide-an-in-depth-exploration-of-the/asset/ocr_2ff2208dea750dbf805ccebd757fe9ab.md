# Advanced Bash-Scripting Guide

Array variables have a syntax all their own, and even standard Bash commands and operators have special options adapted for array use.

# Example 27-3. Various array operations

```
#!/bin/bash
# array-ops.sh: More fun with arrays.

array=( zero one two three four five )
# Element 0 1 2 3 4 5\n
echo ${array[0]}      # zero
echo ${array:0}       # zero
                      # Parameter expansion of first element,
                      # starting at position # 0 (lst character).

echo ${array:1}       # ero
                      # Parameter expansion of first element,
```

# Chapter 27. Arrays