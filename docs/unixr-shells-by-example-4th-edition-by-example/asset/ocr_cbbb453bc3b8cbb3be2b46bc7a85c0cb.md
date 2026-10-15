# EXPLANATION

+   1 The user is asked to enter an integer. The number is assigned to the variable number.
+   2 The expr command evaluates the expression. If addition can be performed, the number is a whole number and expr returns a successful exit status. All output is redirected to the bit bucket /dev/null.
+   3 If expr is successful, it returns a 0 exit status, and the colon command does nothing.
+   4 If the expr command fails, it returns a nonzero exit status, the echo command displays the message, and the program exits.
+   5 The fi ends the if block.

# 14.5.8 The case Command

The case command is a multiway branching command used as an alternative to if/elif commands. The value of the case variable is matched against value1, value2, and so forth, until a match is found. When a value matches the case variable, the commands following the value are executed until the double semicolons are reached. Then execution starts after the word esac (case spelled backward).

If the case variable is not matched, the program executes the commands after the *), the default value, until ;; or esac is reached. The *) value functions the same as the else statement in if/else conditionals. The case values allow the use of shell wildcards and the vertical bar (pipe symbol) for ORing two values.

# FORMAT

```
case variable in
value1)
  command(s)
  ;;
value2)
  command(s)
  ;;
*)
command(s)
;;
esac
```

# EXAMPLE 14.30

(The Script)
#!/bin/bash
# Scriptname: xcolors

+   1 echo -n "Choose a foreground color for your xterm window: "
+   read color