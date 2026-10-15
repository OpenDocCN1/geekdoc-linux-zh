# EXAMPLE 8.36

(With a loop)

(The Script)

```
#!/bin/sh
# Name: doit
# Purpose: shift through command-line arguments
# Usage: doit [args]
1  while [ $# -gt 0 ]
    do
2      echo $*
3      shift
4  done
```

(The Command Line)

```
$ doit a b c d e
a b c d e
b c d e
c d e
d e
e
```

# EXPLANATION

+   1. The while command tests the numeric expression. If the number of positional parameters ($#) is greater than 0, the body of the loop is entered. The positional parameters are coming from the command line as arguments. There are five.
+   2. All positional parameters are printed.
+   3. The parameter list is shifted once to the left.
+   4. The body of the loop ends here; control returns to the top of the loop. Each time the loop is entered, the shift command causes the parameter list to be decreased by 1. After the first shift, $# (number of positional parameters) is four. When $# has been decreased to zero, the loop ends.

# EXAMPLE 8.37

(The Script)

```
#!/bin/sh
# Scriptname: dater
# Purpose: set positional parameters with the set command
# and shift through the parameters.
```