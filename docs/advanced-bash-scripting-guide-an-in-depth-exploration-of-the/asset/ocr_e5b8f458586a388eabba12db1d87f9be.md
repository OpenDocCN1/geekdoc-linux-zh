# Chapter 8. Operations and Related Topics

# 8.1. Operators

assignment

variable assignment
Initializing or changing the value of a variable

= All-purpose assignment operator, which works for both arithmetic and string assignments.

```
var=27
category=minerals # No spaces allowed after the "="
```

Do not confuse the "=" assignment operator with the = test operator.

```
# as a test operator
if [ "$string1" = "$string2" ]
then
  command
fi

# if [ "$string1" = "Xstring2" ] is safer,
# to prevent an error message should one of the variables be empty.
# (The prepended "X" characters cancel out.)
```

arithmetic operators

+   + plus
- minus
* multiplication
/ division
** exponentiation

```
Bash, version 2.02, introduced the """ exponentiation operator.
let z=5\*\*3 # 5 * 5 * 5
echo "z = $z" # z = 125
```

% modulo, or mod (returns the remainder of an integer division operation)

```
bash$ expr 5 % 3
2
5/3 = 1, with remainder 2
```