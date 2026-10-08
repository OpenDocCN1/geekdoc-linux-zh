# 4.2. Variable Assignment

the assignment operator *no space before and after*)

> Do not confuse this with = and -eq which test, rather than assign!

Note that = can be either an assignment or a test operator, depending on context.

Example 4-2. Plain Variable Assignment

```
#!/bin/bash
# Naked variables
echo
# When is a variable "naked", i.e., lacking the '$' in front?
# When it is being assigned, rather than referenced.

# Assignment
a=879
echo "The value of \"a\" is $a."

# Assignment using 'let'
let=16+5
echo "The value of \"a\" is now $a."

echo
# In a 'for' loop (really, a type of disguised assignment)
echo -n "Values of \"a\" in the loop are: ""
for a in 7 8 9 11
do
  echo -n "$a ""
done
echo
echo
# In a 'read' statement (also a type of assignment)
echo -n "Enter \"a\""
read a
echo "The value of \"a\" is now $a."

echo
exit 0
```

Example 4-3. Variable Assignment, plain and fancy

```
#!/bin/bash
a=23	# Simple case
echo $a
nb=$a
```