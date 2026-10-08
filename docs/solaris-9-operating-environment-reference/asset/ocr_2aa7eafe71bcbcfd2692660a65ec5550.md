# ksh, rksh 605

```
exp1 -ne exp2
true if exp1 is not equal to exp2
```

```
exp1 -lt exp2
true if exp1 is less than exp2
```

```
exp1 -gt exp2
true if exp1 is greater than exp2
```

```
exp1 -le exp2
true if exp1 is less than or equal to exp2
```

```
exp1 -ge exp2
true if exp1 is greater than or equal to exp2
```

In each of the above expressions, if file of the form /dev/fd/n, where n is an integer, the test is applied to the open file whose descriptor number is n. You can construct a compound expression from these primitives using any of the following, listed in decreasing order of precedence.

```
(expression)
true if expression is true. To group expressions.
```

```
! expression
true if expression is false.
```

```
expression1 && expression2
true if expression1 and expression2 are both true.
```

```
expression1 || expression2
true if either expression1 or expression2 is true.
```

Environment Variables
The (see environ(5)) is a list of name-value pairs that is passed to an executed program in the shell as a normal argument list. The names must be identifiers, and the values are character strings. The shell interacts with the environment in several ways. On invocation, the shell scans the environment and creates a variable for each name found, giving the corresponding value and marking it. Export commands inherit the environment. If the user modifies the values of these variables creates new ones using the export or typeset -x commands, they become part of the environment. The environment seen by any executed command is thus composed of any name-value pairs originally inherited by the shell, whose values are modified by the current shell, plus any additions that must be noted in export -x commands.

You can augment the environment for any simple command or function by prefixing it with one or more variable assignments. A variable assignment argument is a word of the form identifier=value. Thus:

```
TERM=450 cmd args
```

and