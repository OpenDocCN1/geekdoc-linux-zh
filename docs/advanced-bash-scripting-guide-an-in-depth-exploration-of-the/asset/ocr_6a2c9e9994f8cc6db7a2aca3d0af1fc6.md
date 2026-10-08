# Advanced Bash-Scripting Guide

```
do
echo -n $rchar
let "number -= factor"
let remainder = number - factor
done

return $number
# Exercises:
#-
# 1) Explain how this function works.
# Hint: division by successive subtraction.
# 2) Extend to range of the function.
# Hint: use "echo" and command-substitution capture.

to_roman $num 100 C
num=$?
to_roman $num 90 LXXXX
num=$?
to_roman $num 50 L
num=$?
to_roman $num 40 XL
num=$?
to_roman $num 10 X
num=$?
to_roman $num 9 IX
num=$?
to_roman $num 5 V
num=$?
to_roman $num 4 IV
num=$?
to_roman $num 1 I
num=$?
# Successive calls to conversion function!
# Is this really necessary??? Can it be simplified?
echo
exit
```

See also Example 11-29.

> The largest positive integer a function can return 255. The return is closely tied to the concept of exit status, which accounts for this particular limitation. Fortunately, there are various workarounds for those situations requiring a large integer return value from a function.

# Advanced 24-9. Testing large return values in a function

```
#!/bin/bash
# return-test.sh

# The largest positive value a function can return 255.

return_test ()      # Returns whatever passed to it.
{
    return $1
}
```

Chapter 24. Functions

408