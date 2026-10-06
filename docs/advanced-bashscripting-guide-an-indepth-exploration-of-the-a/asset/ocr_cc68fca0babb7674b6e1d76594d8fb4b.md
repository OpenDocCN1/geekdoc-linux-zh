# Advanced Bash–Scripting Guide

```
MAXCOUNT=10
count=1
echo "$MAXCOUNT random numbers:"
echo "------------------"
while [ "$count -le $MAXCOUNT ]; do
  # Generate 10 ($MAXCOUNT) random integers.
  number=$RANDOM
  echo $number
  let count += 1  # Increment count
done
echo "------------------"
```

# If you need a random int within a certain range, use the 'modulo' operator.
# This returns the remainder of a division operation.

```
RANGE=500
echo
number=$RANDOM
let "number %= $RANGE"
echo "Random number less than $RANGE  --- $number"
echo
```

# If you need a random int greater than a lower bound,
# then set up a test to discard all numbers below.

```
FLOOR=200
number=0  #initialize
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
done
echo "Random number greater than $FLOOR  --- $number"
echo
```

# May combine above two techniques to retrieve random number between two numbers.

```
number=0  #initialize
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
  let "number %= $RANGE"  # Scales number down within $RANGE.
don
echo "Random number between $FLOOR and $RANGE  --- $number"
echo
```

# Generate binary choice, that is, "true" or "false" value.

```
BINARY=2
number=$RANDOM
T=1
let "number >= 14"  gives a better random distribution
# (right) shifts out everything except last binary digit.
if [ "$number" -eq $T ];
then
```

# 9.6. $RANDOM: generate random integer