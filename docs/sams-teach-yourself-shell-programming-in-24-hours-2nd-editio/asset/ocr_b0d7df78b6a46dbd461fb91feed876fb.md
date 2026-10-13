The KillSubProcs function kills all the child processes of the script, which are stored in the variable CHPROCSIDS:

```
KillSubProcs() {
  kill $CHPROCSIDS
  if [ $? -eq 0 ] ; then
    echo "Sub-processes killed."
  fi
}
```

# SetTimer

Once the signal handler for SIGALARM is in place, we need a function that sets up the timer. The function we are using is SetTimer:

```
SetTimer() {
  DEF_TOUT=${1:-10}
  if [ $DEF_TOUT -ne 0 ] ; then
    sleep $DEF_TOUT & kill -s 14 $$
    CHPROCSIDS=$CHPROCSIDS $!
    TIMERPROC=$!
  fi
}
```

This function takes a single argument that indicates the number of seconds the timer should be set. The default is 10 seconds.

The timer itself is fairly trivial; it is just the command
sleep $DEF_TOUT & kill -s 14 $$
executing in the background. This command uses sleep to wait for some period of time (stored in $DEF_TOUT), after which, it uses kill to send the script SIGALRM (recall that the PID of the script is stored in $$).

Because the timer runs in the background, we need to update the list of child processes, $CHPROCSIDS, with its PID. We also save the PID of the timer in $TIMERPROC so that we can use it later when we need to unset the timer.

# UnsetTimer

Finally, we need a function to unset the timer started by SetTimer. The UnsetTimer function does this by using kill to terminate the timer (SetTimer saved the PID of the timer in $TIMERPROC):

```
UnsetTimer() {
  kill $TIMERPROC
}
```