# Advanced Bash-Scripting Guide

```
echo; echo GCD of $1 and $2 = $dividend;
```

# Exercises :
#
# 1) Check command-line arguments to make sure they are integers,
#+ and exit the script with an appropriate error message if not.
# 2) Rewrite the gcd () function to use local variables.

exit 0

+=

plus-equal (increment variable by a constant) [38]

let var = "5" results in var being incremented by 5.

-

minus-equal (decrement variable by a constant)

*==

times-equal (multiply variable by a constant)

let var = "4" results in var being multiplied by 4.

/==

slash-equal (divide variable by a constant)

%=

mod-equal (remainder of dividing variable by a constant)

Arithmetic operators often occur in an expr or let expression.

# Example 8-2. Using Arithmetic Operations

```
#!/bin/bash
# Counting to 11 in 10 different ways.
n=1; echo -n "$n"

let "n = $n + 1"  # let "n = n + 1"  also works.
echo -n "$n"
```

```
$((n = n + 1))
# ":" necessary because otherwise Bash attempts
#+ to interpret $($($n + 1)) as a command.
echo -n "$n"
```

```
((n = n + 1))
# A simpler alternative to the method above.
# Thanks, David Lombard, for pointing this out.
echo -n "$n"
```

```
$[$n = n + 1]
# ":" necessary because otherwise Bash attempts
#+ to interpret "[$n = n + 1]" as a command.
# Works if "$n" was initialized as a string.
```

# 8. Operations and Related Topics