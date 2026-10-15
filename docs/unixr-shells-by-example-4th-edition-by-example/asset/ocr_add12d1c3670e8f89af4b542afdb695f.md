# 14.6.6 Looping Control Commands

If some condition occurs, you may want to break out of a loop, return to the top of the loop, or provide a way to stop an infinite loop. The bash shell provides loop control commands to handle these kinds of situations.

# The shift Command.

The shift command shifts the parameter list to the left a specified number of times. The shift command without an argument shifts the parameter list once to the left. Once the list is shifted, the parameter is removed permanently. Often, the shift command is used in a while loop when iterating through a list of positional parameters.

# FORMAT

```
shift [n]
```

# EXAMPLE 14.43

```
(without a loop)
(The Script)
#!/bin/bash
# Scriptname: shifter
1 set joe mary tom sam
2 shift
3 echo $*
4 set $(date)
5 echo $*
6 shift 5
7 echo $*
8 shift 2

(The Output)
3 mary tom sam
5 Thu Mar 18 10:00:12 PST 2004
7 2002
8 shift: shift count must be <= $#
```

# EXPLANATION

+   1 The set command sets the positional parameters. $1 is assigned joe, $2 is assigned mary, $3 is assigned tom, and $4 is assigned sam. $* represents all of the parameters.
+   2 The shift command shifts the positional parameters to the left; joe is shifted off.
+   3 The parameter list is printed after the shift.
+   4 The set command resets the positional parameters to the output of the UNIX date command.
+   5 The new parameter list is printed.