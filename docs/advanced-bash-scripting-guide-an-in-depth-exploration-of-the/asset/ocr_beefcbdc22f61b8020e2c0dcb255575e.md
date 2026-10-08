# Advanced Bash-Scripting Guide

```
echo "7-- = $a"    # 7- = 6
# Of course, ++a, etc., also allowed . . 
echo

# Trinary operator.

# Note that $a is 6, see above.
let "t = a7??:11"    # True
echo $ # 7

let a++
let "t = a7??:11"    # False
echo $ # 11

exit
```

The let command can, in certain contexts, return a surprising exit status.

```
# Evgeny Ivanov points out:
var=0
echo $?    # 0
# As expected.

let var++
echo $?    # 1
# The command was successful, so why isn't $?=0 ???
# Anomaly!

let var++
echo $?    # 0
# As expected.

# Likewise . .
let var=0
echo $?    # 1
# The command was successful, so why isn't $?=0 ???
```

```
# However, as Jeff Gorak points out,
#+this is part of the design spec for 'let' . .
#+If the last ARG evaluates to 0, let returns 1;
#+let returns 0 otherwise." 'help let'
```

eval argl[arg2] . . [argN]

Combines arguments in an expression or list of expressions and evaluates them. Any variables within the expression are expanded. The result is to convert a string to a command.

> The eval command can be used for code generation from the command-line or within a script.

```
bash$ command_string="ps ax"
bash$ process="ps ax"
bash$ eval "$command_string" | grep "$process"
2973 pts/3 R    0:00 grep --color ps ax
```

Chapter 15. Interaction and Builtins

194