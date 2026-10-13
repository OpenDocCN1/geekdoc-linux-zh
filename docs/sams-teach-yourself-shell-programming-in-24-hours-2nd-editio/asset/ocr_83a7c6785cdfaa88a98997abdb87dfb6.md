grep. Then it extracts the process IDs for these processes using awk and uses kill to terminate these processes

Although the basic script is serviceable, there are a few problems that you need to solve in order to make it much more usable:

+   - The script has no error reporting when the program stored in $PGM does not exist or is not executable.
+   - The script has no error reporting when the program stored in $PGM is already running.
+   - No usage information is supplied if an invalid argument (or no arguments) is supplied to the script.

To solve the first and second problems, you can change the start clause of the case statement to the following:

```
start)
if [ ! -x "$PGM" ] ; then
    echo "Error: Not executable: $PGM" 1>&2
    exit 1
fi
RUNNING=`/bin/ps -ef | grep "$PGM" | grep -v grep | head`
if [ -n "$RUNNING" ] ; then
    echo "Error: Already running: $PGM" 1>&2
    exit 1
fi
"$PGM" $PGM_OPTS
;;
```

As you can see, the start clause now includes two if statements that perform the necessary error checking. First, you verify if the program is executable using the -x file test option. If it is not executable (or does not exist), an error message is reported and the script exits. Otherwise, the script proceeds to the next step in the error checking.

In order to check if the program is already running, you use the following compound command:

`RUNNING=`/bin/ps -ef | grep "$PGM" | grep -v grep | head``

If the program is already running, the value of the variable RUNNING will contain the output of ps for at least one instance of the program. Otherwise RUNNING will be null. You use the -z option to check the variable RUNNING; if it is not null an error message is reported.