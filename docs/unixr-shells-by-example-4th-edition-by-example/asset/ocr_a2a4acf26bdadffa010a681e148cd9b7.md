# EXPLANATION (CONTINUED)

+   5 If the file is readable, writable, and executable, then . . .
+   6 The fi terminates the innermost if command. The program exits with an argument of 2 if the file does not have read, write, and execute permission.
+   7 The else commands are executed if lines 2 and 3 fail. The program exits with a value of 3.
+   8 This fi goes with the if on line 3 in the example.
+   9 The file called testing does not exist.
+   10 The $? variable holds the exit status, 1.

# 12.5.15 The null Command

The null command is a colon. It is a built-in, do-nothing command that returns an exit status of 0. It is used as a placeholder after an if command when you have nothing to say, but need a command or the program will produce an error message because it requires something after the then statement. Often the null command is used as an argument to the loop command to make the loop a forever loop or for testing variable expression modifiers such as {EDITOR:=/bin/vi}.

# EXAMPLE 12.25

```
(The Script)
1 name=Tom
2 if grep "$name" databasefile > /dev/null 2>&1
then
3 :
4 else
    print "$1 not found in databasefile"
    exit 1
fi
```

# EXPLANATION

+   1 The string Tom is assigned to the variable name.
+   2 The if command tests the exit status of the grep command. If Tom is found in databasefile, the null command is executed and does nothing.
+   3 The colon is the null command. It always exits with a 0 exit status.
+   4 What we really want to do is print an error message and exit if Tom is not found. The commands after the else will be executed if the grep command fails.

# EXAMPLE 12.26

```
(The Script)
1 : ${EDITOR:=/bin/vi}
2 echo $EDITOR
```