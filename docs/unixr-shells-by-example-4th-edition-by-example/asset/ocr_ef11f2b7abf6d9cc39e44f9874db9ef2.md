# EXPLANATION (CONTINUED)

+   3 The variable x is not assigned a value. The shell will assign the null value. The null value, an empty string, is displayed.
+   4 The period in the variable name is illegal. The only characters allowed in a variable name are numbers, letters, and the underscore. The shell tries to execute the string as a command.

The Scope of Local Variables. A local variable is known only to the shell in which it was created. It is not passed on to subshells. The double dollar sign variable is a special variable containing the PID of the current shell.

# EXAMPLE 7.19

```
1 $ echo $$ 
1313
2 $ round=world
$ echo $round
world
3 $ sh   # Start a subshell
4 $ echo $$
1326
5 $ echo $round

6 $ exit   # Exits this shell, returns to parent shell
7 $ echo $$
1313
8 $ echo $round
world
```

# EXPLANATION

+   1 The value of the double dollar sign variable evaluates to the PID of the current shell. The PID of this shell is 1313.
+   2 The local variable round is assigned the string value world, and the value of the variable is displayed.
+   3 A new Bourne shell is started. This is called a subshell, or child shell.
+   4 The PID of this shell is 1326. The parent shell's PID is 1313.
+   5 The variable round is not defined in this shell. A blank line is printed.
+   6 The exit command terminates this shell and returns to the parent shell. (Ctrl-D will also exit this shell.)
+   7 The parent shell returns. Its PID is displayed.
+   8 The value of the variable round is displayed.