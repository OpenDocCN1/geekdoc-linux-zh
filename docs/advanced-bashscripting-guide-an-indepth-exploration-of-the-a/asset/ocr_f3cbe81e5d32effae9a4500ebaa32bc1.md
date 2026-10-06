# Advanced Bash–Scripting Guide

pop
status_report

```
echo

push garbage
pop
status_report # Garbage in, garbage out.
value1=23; push $value1
value2=skidoo; push $value2
value3=FINAL; push $value3

pop # FINAL
status_report
pop # skidoo
status_report
pop # 23
status_report # Last-in, first-out!
```

# Notice how the stack pointer decrements with each push
# + increments with each pop.

```
echo
====================================================
```

# Exercises:

+   # 1) Modify the "push()" function to permit pushing
  + multiple element on the stack with a single function call.
# 2) Modify the "pop()" function to permit popping
  + multiple element from the stack with a single function call.
# 3) Using this script as a jumping-off point,
  + write a stack-based 4-function calculator.

exit 0

Fancy manipulation of array "subscripts" may require intermediate variables. For projects involving this, again consider using a more powerful programming language, such as Perl or C.

# Example 26–7. Complex array application: Exploring a weird mathematical series

```
#!/bin/bash

# Douglas Hofstadter's notorious "Q-series":

# Q(1) = Q(2) = 1
# Q(n) = Q(n - Q(n-1)) + Q(n - Q(n-2)), for n>2
```

# This is a "chaotic" integer series with strange and unpredictable behavior.
# The first 20 terms of the series are:
# 1 2 3 4 5 5 6 6 8 8 9 10 10 11 11 12

# 26. Arrays