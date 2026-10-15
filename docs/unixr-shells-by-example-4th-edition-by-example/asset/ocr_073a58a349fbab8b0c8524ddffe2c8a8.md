The shell in which a variable is created is called the parent shell. If a new shell is started from the parent shell, it is called the child shell. Some of the environment variables, such as HOME, LOGNAME, PATH, and SHELL, are set before you log in by the /bin/login program. Normally, environment variables are set in the .profile file in the user's home directory.

# Setting Environment Variables.

To set environment variables, the export command is used either after assigning a value or when the variable is set. All variables in a script can be exported by turning on the allexport option to the set command (e.g., set -o allexport).

# EXAMPLE 11.37

```
1  $ TERM=wyse ; export TERM
2  $ export NAME ="John Smith"
   $ print $NAME
   John Smith
3  $ print $$ 
   319
4  $ ksh
5  $ print $$
   340
6  $ print $NAME
   John Smith
7  $ NAME="April Jenner"
   $ print $NAME
   April Jenner
8  $ exit
9  $ print $$
   319
10 $ print $NAME
    John Smith
```

# EXPLANATION

+   1 The TERM variable is assigned wyse. The variable is exported. Now processes started from this shell will inherit the variable.
+   2 The variable is exported and defined in the same step. (New with the Korn shell.)
+   3 The value of this shell's PID is printed.
+   4 A new Korn shell is started. The new shell is the child, the original shell is its parent.
+   5 The PID of the new Korn shell, stored in the $$ (340) variable, is printed.
+   6 The variable was exported to the new shell and is displayed.
+   7 The variable is reset to April Jenner and displayed.
+   8 This Korn child shell is exited. The parent shell will return.
+   9 The PID of the parent, 319, is displayed again.
+   10 The variable NAME contains its original value. Variables retain their values when exported from parent to child. The child cannot change the value of a variable for its parent.