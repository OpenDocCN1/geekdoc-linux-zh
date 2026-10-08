# Advanced Bash-Scripting Guide

Similar to the if-test construct, a while loop can omit the test brackets.

```
while condition
do  command(s) ...ndo
```

By coupling the power of the read command with a while loop, we get the handy read construct, useful for reading and parsing files.

```
cat $filename | # Supply input from a file.
while read line # As long as there is another line to read ...
do
done
========= Snippet from "sd.sh" example script ==========
while read one data point at a time.
do  rt=$(echo "scale=$SC; $rt + $value" | bc)
  ((++))
done
am=$(echo "scale=$SC; $rt / $ct" | bc)
echo $am; # This function "returns" TWO VALUES!
# Caution: This little trick will not work if $ct > 255!
# To handle a larger number of data points,
# simply count the "return $ct" above.
) $datafile # Feed in data file.
```

> A while loop may have its stdin redirected to a file by a < at its end.

> A while loop may have its stdin supplied by a pipe.

until This construct tests for a condition at the top of a loop, and keeps looping as long as condition is false (opposite of while loop).

```
until [ condition-is-true ]
do  command(s)...ndo
```

Note that an until loop tests for the terminating condition at the top of the loop, differing from a similar construct in some programming languages.

As is the case with for loops, placing the do on the same line as the condition test requires a semicolon.

```
until [ condition-is-true ] ; do
```

Example 11-19. until

# Chapter 11. Loops and Branches