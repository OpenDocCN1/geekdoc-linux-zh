# EXAMPLE 14+7

(The Script)

```
#!/bin/bash
# Scriptname: dater
# Purpose: set positional parameters with the set command
# and shift through the parameters.
```

```
1  set $(date)
2  while (( $# > 0 ))
    do
3      echo $1
4      shift
done
```

(The Output)

```
Wed
Mar
17
19:25:00
PST
2004
```

# EXPLANATION

+   1 The set command takes the output of the date command and assigns the output to positional parameters $1 through $6.
+   2 The while command tests whether the number of positional parameters ($#) is greater than 0. If true, the body of the loop is entered.
+   3 The echo command displays the value of $1, the first positional parameter.
+   4 The shift command shifts the parameter list once to the left. Each time through the loop, the list is shifted until the list is empty. At that time, $# will be zero and the loop terminates.

# The break Command.

The built-in break command is used to force immediate exit from a loop, but not from a program. (To leave a program, the exit command is used.) After the break command is executed, control starts after the done keyword. The break command causes an exit from the innermost loop, so if you have nested loops, the break command takes a number as an argument, allowing you to break out of a specific outer loop. If you are nested in three loops, the outermost loop is loop number 3, the next nested loop is loop number 2, and the innermost nested loop is loop number 1. The break is useful for exiting from an infinite loop.