
# EXAMPLE 10.8

(Echo and Verbose)

```
1 % cat practice
#!/bin/csh
echo Hello $LOGNAME
echo The date is `date`
set echo
echo Your home shell is $SHELL
unset echo
echo Good-bye $LOGNAME

% chmod +x practice
```

```
2 % practice
Hello ellie
The date is Sun May 26 12:25:16 PDT 2004
---> echo Your login shell is /bin/csh
---> Your login shell is /bin/csh
---> unset echo
Good-bye ellie
```

## EXPLANATION

- 1 The echo option is set and unset within the script. This enables you to debug certain sections of your script where you have run into a bottleneck, rather than echoing each line of the entire script.
- 2 The ---> marks where the echoing was turned on. Each line is printed after variable and command substitution and then executed.

# EXAMPLE 10.9

```
1 % cat practice
#!/bin/csh
echo Hello $LOGNAME
echo The date is `date`
set verbose
echo Your home shell is $SHELL
unset verbose
echo Good-bye $LOGNAME
```

```
2 % practice
Hello ellie
The date is Sun May 23 12:30:09 PDT 2004
---> echo Your login shell is $SHELL
---> Your login shell is /bin/csh
---> unset verbose
Good-bye ellie
```

## EXPLANATION

- 1. The verbose option is set and unset within the script.
- 2. The --> marks where verbose was turned on. The lines are printed just as they were typed in the script and then executed.

# 10.5 Command-Line Arguments

Shell scripts can take command-line arguments. Arguments are used to modify the behavior of the program in some way. The C shell assigns command-line arguments to positional parameters and enforces no specific limit on the number of arguments that can be assigned (the Bourne shell sets a limit of nine positional parameters). Positional parameters are number variables. The script name is assigned to $0, and any words following the scriptname are assigned to $1, $2, $3 ... ${10}, ${11}, and so on. $1 is the first command-line argument. In addition to using positional parameters, the C shell provides the argv built-in array.

### 10.5.1 Positional Parameters and argv

If using the argv array notation, a valid subscript must be provided to correspond to the argument being passed in from the command line or the error message Subscript out of range is sent by the C shell. The argv array does not include the script name. The first argument is $argv[1], and the number of arguments is represented by $#argv. (There is no other way to represent the number of arguments.) See Table 10.4.

# Table 10.4 Command-Line Arguments

| Argument | Meaning |
|---|---|
| $0 | The name of the script. |
| $1, $2, ... ${10} ... | The first and second positional parameters are referenced by the number preceded by a dollar sign. The curly braces shield the number 10 so that it does not print the first positional parameter followed by a 0. |
| $* | All the positional parameters. |
| $argv[0] | Not valid; nothing is printed. C shell array subscripts start at 1. |
| $argv[1] $argv[2]... | The first argument, second argument, and so on. |
| $argv[*] | All arguments. |
| $argv | All arguments. |
| $#argv | The number of arguments. |
| $argv[$#argv] | The last argument. |

# EXAMPLE 10.10

(The Script)

```
#!/bin/csh -f
# The greetings script
# This script greets a user whose name is typed in at the command line.
echo $0 to you $1 $2 $3
echo Welcome to this day `date | awk '{print $1, $2, $3}'`
echo Hope you have a nice day, $argv[1]!
echo Good-bye $argv[1] $argv[2] $argv[3]
```

(The Command Line)

```
% chmod +x greetings
% greetings Guy Quigley
greetings to you Guy Quigley
Welcome to this day Fri Aug 28
Hope you have a nice day, Guy!
Subscript out of range
```

## EXPLANATION

- 1. The name of the script and the first three positional parameters are to be displayed. Because there are only two positional parameters coming in from the command line, Guy and Quigley, $1 becomes Guy, $2 becomes Quigley, and $3 is not defined.
- 2. The awk command is quoted with single quotes so that the shell does not confuse awk's field numbers $1, $2, and $3 with positional parameters. (Do not confuse awk's field designators $1, $2, and $3 with the shell's positional parameters.)
- 3. The argv array is assigned values coming in from the command line. Guy is assigned to argv[1] and its value is displayed. You can use the argv array to represent the command-line arguments within your script, or you can use positional parameters. The difference is that positional parameters do not produce an error if you reference one that has no value, whereas an unassigned argv value causes the script to exit with the Subscript out of range error message.
- 4. The shell prints the error message Subscript out of range because there is no value for argv[3].

# 10.6 Conditional Constructs and Flow Control

When making decisions, the if, if/else, if/else if, and switch commands are used. These commands control the flow of the program by allowing decision making based on whether an expression is true or false.
