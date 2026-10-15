# EXAMPLE 12.18 (CONTINUED)

```
2 if [ "$answer" = Y -o "$answer" = y ]   # Old-style test
then
    print "Glad to hear it."
3 fi
```

# EXPLANATION

+   1 The user is asked the question, Are you ok (y/n) ?. The read command causes the program to wait for user input.
+   2 The test command, represented by a [, is used to test expressions and returns an exit status of 0 if the expression is true and nonzero if the expression is false. If the variable answer evaluates to Y or y, the commands after the then statement are executed. (The test command does not allow the use of wildcards when testing expressions.)
+   3 The fi terminates the list of commands following the then statement.

# 12.5.9 Using the New-Style Korn test

The new-style Korn shell testing allows expressions to contain shell metacharacters and Korn shell operators such as && and ||.

# EXAMPLE 12.19

```
#!/bin/ksh
# Scriptname: are_you_ok2
1 print "Are you ok (y/n) ?"
read answer
2 if [[ "$answer" = [Yy]* ]]   # New-style test
then
    print "Glad to hear it."
3 fi
```

# EXPLANATION

+   1 The user is asked the question, Are you ok (y/n) ?. The read command causes the program to wait for user input.
+   2 The [[ ]] is a special Korn shell construct used to test expressions. If the answer evaluates to Y or y followed by any number of characters, the commands after the then statement are executed.
+   3 The fi statement terminates the if.