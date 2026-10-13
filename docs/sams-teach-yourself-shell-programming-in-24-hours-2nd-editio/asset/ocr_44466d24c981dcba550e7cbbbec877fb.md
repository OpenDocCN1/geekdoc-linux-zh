# Summary

This chapter covered the concept of signals. Signals inform a program that an important event has occurred.

First we examined the most common signals encountered in shell programming. This was followed by a discussion of the methods for obtaining a list of the signals supported on your system. This section also covered the concept of delivering signals and the default actions associated with a signal.

The second section demonstrated two methods of signal handling. The first method is to catch signals and handle them using a signal handler. The second method is to ignore signals. Finally, we explored the use of signals to set up a timer.

# Questions

1. The following is the main body of the "live" script presented earlier in this chapter. Change the script such that SIGQUIT causes it to exit after the wait command returns.

```
# main()

trap Cleanup 2 3 15
trap Init 1

PROG=$1
Init

while : ;
do
  wait $!
  SPROG &
done
```

2. Add a signal handler to the timer script to handle SIGINT.

# Terms

Signal  A signal is a software interrupt sent to a program to indicate that an important event has occurred.

Default Action  The default action is the action that the system takes on behalf of the program in the absence of a signal handler.

Signal Handler  A signal handler is a function provided by a program that defines the actions to take when a signal is received.