
# Advanced Bash–Scripting Guide

```bash
# Bash, version 2.02, introduced the """ exponentiation operator.
let z=5**3
echo "z = $z" # z = 125
```

modulo, or returns the remainder of an integer division operation

```bash
bash$ echo `expr 5 % 3'
2
```

This operator finds use in among other things, generating numbers within a specific range (see Example 9–21 and Example 9–22) and formatting program output (see Example 26–7 and Example A–6). It can even be used to generate prime numbers, (see Example A–14). Modulo turns up surprisingly often in various numerical recipes.

# Example 8–1. Greatest common divisor

```bash
#!/bin/bash
# gcd.sh greatest common divisor
# Uses Euclid's algorithm

# The "greatest common divisor" (gcd) of two integers
+# is the largest integer that will divide both, leaving no remainder.

# Euclid's algorithm uses successive division.
# In each pass,
## dividend < divisor
## divisor <- remainder
## until remainder = 0.
# The gcd = excellent, on the final pass.

# For an excellent discussion of Euclid's algorithm, see
# Jim Loy's site, http://www.jimloy.com/number/euclids.html

# Argument check
ARGS=2
E_BADARGES=65

if [ "$#" -ne "$ARGS" ];
then
    echo "Usage: `basename` first-number second-number"
    exit $E_BADARGES
fi
```

```bash
gcd () {
    # Arbitrary assignment.
    # It does not matter
    dividend=$1
    divisor=$2
    +# which of the two is larger.
    # Why?
}
```

Chapter 8. Operations and Related Topics

# Advanced Bash–Scripting Guide

```bash
remainder=1              # If uninitialized variable used in loop,
# ++ it results in an error message
# + on first pass through loop.

until [ "$remainder" -eq 0 ]
do
    let remainder = $dividend % $divisor
    dividend=$divisor      # Now repeat with 2 smallest numbers.
    divisor=$remainder      # Euclid's algorithm
done
# Last $dividend is the gcd.
```

gcd $1 $2
echo; "GCD of $1 and $2 = $dividend"; echo

+   Exercise :
-------
# Check command-line arguments to make sure they are integers,
+# and exit the script with an appropriate error message if not.

exit 0

"plus-equal" (increment variable by a constant)

let var += 5 results in var being incremented by 5.

"minus-equal" (decrement variable by a constant)

"times-equal" (multiply variable by a constant)

let var *= 4 results in var being multiplied by 4.

"slash-equal" (divide variable by a constant)

"mod-equal" (remainder of dividing variable by a constant)

Arithmetic operators often occur in an expr or let expression.

# Example 8–2. Using Arithmetic Operations

```bash
#!/bin/bash
```

# Counting in 6 in 5 different ways.

```bash
n=1; echo -n "$n"

let n = $n + 1  # let n = n + 1 also works.
echo -n "$n"

$((($n + 1)))
# " necessary because otherwise Bash attempts
#+ to interpret "$(n = $n + 1)" as a command.
echo -n "$n"

n=$($n + 1)
echo -n "$n"

$: n = $n + 1
# necessary because otherwise Bash attempts
#+ to interpret "$(n = $n + 1)" as a command.
# Works even if "n" was initialized as a string.
echo -n "$n"

s={ $n + 1 }
# Works even if "n" was initialized as a string.
# Avoid this type of construct, since it is obsolete and non-portable.
echo -n "$n"; echo
```

# Thanks, Stephanie Chazelas.

exit 0

![](img/1ce1edffaa36e4f698a85430e716d3b_62.png)

Integer variables in Bash are actually long (32-bit) integers, in the range of -2147483648 to 2147483647. An operation that takes a variable outside these limits will give an error.

| Operator | Description |
| :--- | :--- |
| << | bitwise left shift (multiplies by 2 for each shift) |
| >> | bitwise right shift (divides by 2 for each shift) |
| & | bitwise and |
| \| | bitwise OR |
| ~ | bitwise negate |
| ^ | bitwise XOR |
| <<= | bitwise left shift-equal
| >>= | bitwise right shift-equal |
| &= | bitwise and-equal |
| \|= | bitwise OR-equal |
| ^= | bitwise XOR-equal |

Bash does not understand floating point arithmetic. It treats numbers containing a decimal point as strings.

```bash
a=1.5
let b = $a + 1.3 # error in expression (token is ".5 + 1.3")
echo $b
```

Use bc in scripts that need floating point calculations or math functions. Bitwise operators seldom appear in shell scripts. Their chief use seems to be manipulating and testing values on the fly, such as C and C++.

# Chapter 8. Operations and Related Topics

# logical operators

&& (logical)

```bash
if [ $condition1 ] && [ $condition2 ];
# Same as: if [ $condition1 -a $condition2 ]
# Returns true if both condition hold true...
if [[ $condition1 && $condition2 ]]; # Also works.
# Note that && not permitted within [ ] construct.
```
![](img/1ce1edffaa36e4f698a85430e716d3b_64.png)

&& may also, depending on context, be used to concatenate commands.

or (logical)

```bash
if [ $condition1 ] || [ $condition2 ];
# Same as: if [ $condition1 -o $condition2 ]
# Returns true if either condition or condition2 holds true...
if [[ $condition1 || $condition2 ]]; # Also works.
# Note that || not permitted within [ ] construct.
```

![](img/1ce1edffaa36e4f698a85430e716d3b_64.png)

Bash tests the exit status of each statement with a logical operator.

# Example 8–3. Compound Tests Using && and ||

```bash
#!/bin/bash
a=24
b=47
if [ "$a" -eq 24 ] && [ "$b" -eq 47 ];
then
  echo "Test #1 succeeds."
else
  echo "Test #1 fails."
fi
# ERROR: if [ "$a" -eq 24 ] && [ "$b" -eq 47 ]
# attempts to execute ' "$a" -eq 24 '
# and fails to finding matching ''.
if [ "$a" -eq 24 ] && [ "$b" -eq 44 ]; # works
# (The "&&" has a different meaning in line 17 than in line 6.)
# Thanks, Stephanie Chazelas.
if [ "$a" -eq 98 ] || [ "$b" -eq 47 ];
then
  echo "Test #2 succeeds."
else
  echo "Test #2 fails."
fi
```

# -a and -o options provide an alternative compound condition test.
# Thanks to Patrick Callahan for pointing this out.

```bash
if [ "$a" -eq 24 -a "$b" -eq 47 ];
then
  echo "Test #3 succeeds."
else
  echo "Test #3 fails."
fi

if [ "$a" -eq 98 -o "$b" -eq 47 ];
then
  echo "Test #4 succeeds."
else
  echo "Test #4 fails."
fi
```

```bash
a=rhino
b=crocodile
if [ "$a" = rhino ] && [ "$b" = crocodile ];
then
  echo "Test #5 succeeds."
else
  echo "Test #5 fails."
fi

exit 0
```

The bitwise operators find use mainly for loops. See Example 10–12.

# 8.2. Numerical Constants

A shell script interprets a number as decimal (base 10), unless number has a special prefix or notation. A number preceded by 0 is octal (base 8). A number preceded by 0x is hexadecimal (base 16). A number with an embedded # is BASE#NUMBER (this option is of limited usefulness because of restrictions)

# Example 8-4. Representation of numerical constants:

```bash
#!/bin/bash
# numbers.sh: Representation of numbers.

# Decimal
let "dec = 32"
echo "decimal number = $dec"      # 32

# Octal: numbers preceded by '0' (zero)
let "oct = 071"
echo "octal number = $oct"      # 57
# Expresses result in decimal.

# Hexadecimal: numbers preceded by '0x' or '0X'
let "hex = 07a"
echo "hexadecimal number = $hex"  # 122
# Expresses result in decimal.

# Other bases: BASE#NUMBER
# BASE between 2 and 64.

let "bin = 2#11110011100111"
echo "bin = $bin"                # 31181

let "b32 = 32#77"
echo "base-32 number = $b32"     # 231

let "b64 = 64#"
echo "base-64 number = $b64"      # 4094

# This notation only works for a limited range (2 - 64)
# 10 digits + 26 lowercase characters + 26 uppercase characters + @ + _

echo
echo $((36#kz)) $((2#10101010)) $((16#AF16)) $((53#1aa))
                                # 1295 170 44822 3375
```

# Important note:
# Using a digit out of range of the specified base notation
# + will give an error message.

```bash
let bad_oct = 081"
```
