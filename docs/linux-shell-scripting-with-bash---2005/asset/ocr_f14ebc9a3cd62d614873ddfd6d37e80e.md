For example, to round to the nearest 10, do this:

```
```
$ declare -i COST=5234
$ COST=$(COST+5)/10*10
$ printf '%d\n' $COST
5230
```
```

The parentheses must be escaped to prevent the shell from treating them as a reference to a subshell.

The let command will also handle octal and hexadecimal values.

```
```
$ declare -i OCTAL=0
$ let "OCTAL=0775"
$ printf '%d\n' "$OCTAL"
509
```
```

The operations are described in the next section.

# ## Logical Expressions

In let, true is represented by the value of 1, and false by 0. Any value other than 1 or 0 is treated as true, but the logical operators themselves only return 1 or 0.

Remember that logical truth (a value greater than zero) is not the same as the success of a command (a status code of zero). In this respect, test and let are opposites of each other.

To use logical negation at the shell prompt, you must disable the shell history option or Bash will interpret the ! as a history look-up request.

```
```
$ let "RESULT=!0"
$ printf "logical negation of 0 is %d\n" "$RESULT"
logical negation of 0 is 1
```
```

```
```
$ let "RESULT=!1"
$ printf "logical negation of 1 is %d\n" "$RESULT"
logical negation of 1 is 0
```
```

```
```
$ let "RESULT=1 && 0"
$ printf "logical and of 1 with 0 is %d\n" "$RESULT"
logical and of 1 with 0 is 0
```
```

```
```
$ let "RESULT=1 || 0"
$ printf "logical or of 1 with 0 is %d\n" "$RESULT"
logical or of 1 with 0 is 1
```
```

There is no logical exclusive-or operator.