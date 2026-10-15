# EXAMPLE 8.20

(The Script)

```
1 name=Tom
2 if grep "$name" databasefile > /dev/null 2>&1
then
3 :
4 else
echo "$1 not found in databasefile"
exit 1
fi
```

# EXPLANATION

+   1 The variable name is assigned the string Tom.
+   2 The if command tests the exit status of the grep command. If Tom is found in the database file, the null command, a colon, is executed and does nothing.
+   3 The colon is the null command. It does nothing other than returning a 0 exit status.
+   4 What we really want to do is print an error message and exit if Tom is not found. The commands after the else will be executed if the grep command fails.

# EXAMPLE 8.21

(The Command Line)

```
1 $ DATAFILE=
2 $ : ${DATAFILE:=$HOME/db/datafile}
$ echo DATAFILE
/home/jody/ellie/db/datafile
3 $ : ${DATAFILE:=$HOME/junk}
$ echo DATAFILE
/home/jody/ellie/db/datafile
```

# EXPLANATION

+   1 The variable DATAFILE is assigned null.
+   2 The colon command is a "do-nothing" command. The modifier (: =) returns a value that can be assigned to a variable or used in a test. In this example, the expression is passed as an argument to the do-nothing command. The shell will perform variable substitution; that is, assign the pathname to DATAFILE if DATAFILE does not already have a value. The variable DATAFILE is permanently set.
+   3 Because the variable has already been set, it will not be reset with the default value provided on the right of the modifier.