# Advanced Bash-Scripting Guide

```
echo "Number of elements in array1" = ${array1[*]} # 1 (Surprise!)
echo "Number of elements in array2" = ${array2[*]} # 0
echo "Number of elements in array3" = ${array3[*]} # 0
```

```
==================================================================
```

ListArray

# Try extending those arrays.

```
# Adding an element to an array.
array0="${array0[@]} new"
array1="${array1[@]} new"
array2="${array2[@]} new"
array3="${array3[@]} new"
```

ListArray

```
# or
array0="${array0[*]}\}=new"
array1="${array1[*]}\}=new"
array2="${array2[*]}\}=new"
array3="${array3[*]}\}=new"
```

ListArray

```
# When extended above, arrays are 'stacks'
# Above is the 'push'...
# The stack 'height' is:
height=$${array2[@]}
echo
echo "Stack height for array2 = $height"
```

```
# The 'pop' is:
unset array2[${array2[@]}-1] # Arrays are zero-based,
height=$${array2[@]} ## which means first element has index 0.
echo
echo "New stack height for array2 = $height"
```

ListArray

```
# List only 2nd and 3rd elements of array0.
from=1 # Zero-based numbering.
to=2
array3=(\${array0[@]:1:2 )
echo
echo "Elements in array3: ${array3[@]}"
```

# Works like a string (array of characters).
# Try some other "string",

```
# Replacement:
array4=${array0[@]}/second/2nd)
echo
echo "Elements in array4: ${array4[@]}"
```

```
# Replace all matching wildcarded string.
array5=${array0[@]//new?old}
echo
echo "Elements in array5: ${array5[@]}"
```

# Chapter 27. Arrays

435