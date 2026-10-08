# Advanced Bash-Scripting Guide

```
# Another way of assigning array variables...
# array_name=( XXX YYY ZZZ ... )

area2=( zero one two three )

echo -n "area2[0] = ""
echo ${area2[0]}
# Aha, zero-based indexing (first element of array is [0], not [1]).

echo -n "area2[1] = ""
echo ${area2[1]} # [1] is second element of array.
--------------------------------------------------------------------------------
echo; echo; echo

--------------------------------------------------------------------------------
# Yet another array, "area3"
# Yet another way of assigning array variables...
# array_name=([xx]=XXX [yy]=YYY ...)
area3=([17]=seventeen [24]=twenty-four)

echo -n "area3[17] = ""
echo ${area3[17]}

echo -n "area3[24] = ""
echo ${area3[24]}
--------------------------------------------------------------------------------
exit 0
```

As we have, a convenient way of initializing an entire array is the array=(element1 element2 ... elementN) notation.

```
base64_charset=((A..Z) [a..z] (0..9) + /=)
# Using extended brace expansion
# + to initialize the elements of the array.
# Excerpted from vladz's "base64.sh" script
# + in the "Contributed Scripts" appendix.
```

Bash permits operations on variables, even if the variables are not explicitly declared as.

```
string=ABC123ABCabc
echo ${string[#]} # ABC123ABCabc
echo ${string[*]} # ABC123ABCabc
echo ${string[0]} # ABC123ABCabc
echo ${string[1]} # No output!
echo ${string[@]} # Why?
# 1
# One element in the array.
# The string itself.
```

# Thank you, Michael Zick, for pointing this out.
Once again this demonstrates that Bash variables are untyped.

# 27-2. Formatting a poem

Chapter 27. Arrays