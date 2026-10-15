# EXAMPLE 12.40 (CONTINUED)

```
3 print $5
4 set $(date)
5 print $*
6 shift 5
7 print $*
8 shift 2
```

(The Output)

```
$ doit0
3 mary tom sam
5 Sun Sep 9 10:00:12 PDT 2004
7 2004
8 ksh: shift: bad number
```

# EXPLANATION

+   1 The set command sets the positional parameters. $1 is assigned joe, $2 is assigned mary, $3 is assigned tom, and $4 is assigned sam.
+   2 The shift command shifts the positional parameters to the left; joe is shifted off.
+   3 The parameter list is printed after the shift. $* represents all of the parameters.
+   4 The set command resets the positional parameters to the output of the UNIX date command.
+   5 The new parameter list is printed.
+   6 This time the list is shifted five times to the left.
+   7 The new parameter list is printed.
+   8 By attempting to shift more times than there are parameters, the shell sends a message to standard error.

# EXAMPLE 12.41

(With a Loop)

(The Script)

```
#!/bin/ksh
# Usage: doit [args]
1 while (( $# > 0 ))
do
2     print $*
3     shift
4 done
```