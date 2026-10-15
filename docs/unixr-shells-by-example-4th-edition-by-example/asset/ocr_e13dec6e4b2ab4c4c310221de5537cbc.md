# 12.4 Positional Parameters and Command-Line Arguments

Command-line arguments can be referenced in scripts with positional parameters: for example, $1 is set to the first argument, $2 to the second argument, and $3 to the third argument. Positional parameters can be reset with the set command. See Table 12.5.

# Table 12.5 Positional Parameters

| Variable | Function |
|---|---|
| $0 | References the name of the script |
| $# | Holds the value of the number of positional parameters |
| $* | Contains a list of all the positional parameters |
| $@ | Means the same as $*, except when enclosed in double quotes |
| "$*" | Expands to a single argument, for example, "$1 $2 $3" |
| "$@" | Expands to separate arguments, for example, "$1" "$2" "$3" |

# 12.4.1 The set Command and Positional Parameters

The set command sets the positional parameters. If the positional parameters have already been set, the set command will reset them, removing any values in the old list. To unset all of the positional parameters, use set --.

# EXAMPLE 12.12

```
(The Script)
$ cat args
#!/bin/ksh
# Script to test command-line arguments
1 print The name of this script is $0.
2 print The arguments are $*.
3 print The first argument is $1.
4 print The second argument is $2.
5 print The number of arguments is $#.
6 oldparameters=$*
7 set Jake Nicky Scott
8 print All the positional parameters are $*.
9 print The number of positional parameters is $#.
10 print $oldparameters
```