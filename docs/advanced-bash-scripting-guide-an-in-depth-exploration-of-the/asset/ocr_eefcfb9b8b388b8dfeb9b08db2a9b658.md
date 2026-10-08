# Advanced Bash-Scripting Guide

```
variable=`bc << LIMIT_STRING
options
statements
Operations
LIMIT_STRING

...or...

variable=$(bc << LIMIT_STRING
options
statements
operations
LIMIT_STRING
)
```

# Example 16-49. Invoking bc using a here document

```
#!/bin/bash
# Invoking 'bc' using command substitution
# in combination with a 'here document'

var1=`bc << EOF
18.33 * 19.78
EOF
echo $var1      # 362.56

# $( ... ) notation also works
v1=23.53
v2=17.881
v3=83.501
v4=171.63

var2=$(bc << EOF)
scale = 4
a = ($v1 + $v2)
b = ($v3 * $v4)
a * b + 15.35
EOF
echo $var2      # 593487.8452

var3=$(bc -1 << EOF)
scale = 9
s ( 1.7 )
EOF
# Returns the sine of the 1.7 radians.
# The "-1" option calls the 'bc' math library.
echo $var3      # .991664810

# Now, try it in a function...
hypotenuse ()  # Calculate hypotenuse of a right triangle.
```

# Chapter 16. External Filters, Programs and Commands