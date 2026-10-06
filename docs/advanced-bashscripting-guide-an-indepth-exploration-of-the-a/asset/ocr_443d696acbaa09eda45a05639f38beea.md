```
hyp=$ (bc -1 << EOF
scale = 9
sqrt ( $1 * $1 + $2 * $2 )
EOF
# Unfortunately, can't return floating point values from a Bash function.
)
hypotenuse 3.68 7.31
echo "hypotenuse = $hyp"      # 8.18403934

exit 0
```

Another way of doing floating point math in a script is awk's built-in math functions in a shell wrapper.

# Example 12–33. Calculating the hypotenuse of a triangle

```
#!/bin/bash
# hypotenuse.sh: Returns the "hypotenuse" of a right triangle.
# square root of squares of the "legs"

ARGS=2      # Script needs sides of triangle passed.
E_BADARGS=65  # Wrong number of arguments.

if [ $# -ne "$ARGS" ]; then  # Test number of arguments to script.
then
    echo "Usage: basename $0' side_1 side_2"
    exit $E_BADARGS
fi

AWKSCRIPT='printf("%3.3f\n", sqrt($1 + $2*$2))' ' 
  # parameters passed to awk
  command(s)

echo -n "Hypotenuse of $1 and $2 = "
echo $1 $2 | awk "$AWKSCRIPT"

exit 0
```

# 12.9. Miscellaneous Commands

# Command Listing

These utilities emit a sequence of integers

The normal separator character between each integer is a newline, but this can be changed with the -s option.