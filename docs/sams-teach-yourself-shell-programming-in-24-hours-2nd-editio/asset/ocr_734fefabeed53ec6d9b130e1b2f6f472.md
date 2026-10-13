sends the HUP (hang-up) signal to the program that is running with PID 1001. You can also use the numeric value of the signal as follows:

```
$ kill -1 1001
```

This command also sends the hang-up signal to the program that is running with PID 1001. Although the default action for this signal is to terminate the process, many UNIX programs use this signal as an indication that they should reinitialize themselves. For this reason, you should use a different signal if you are trying to terminate or kill a process.

# SIGQUIT and SIGINT

In some cases, SIGTERM will not be sufficient to terminate a process. In such cases, you can try to send the process either a SIGQUIT (quit) or a SIGINT (interrupt):

```
$ kill -s SIGQUIT 1001
```

or

```
$ kill -s SIGINT 1001
```

One of these signals should terminate a process, either by asking it to quit (the QUIT signal) or by asking it to interrupt its processing (the INT signal).

# SIGKILL

To terminate a truly pernicious program that refuses to die, you can resort to using SIGKILL. This signal is usually referred to by its integer value, 9. SIGKILL has the special property that it cannot be caught; any process receiving it terminates immediately.

The following command sends a SIGKILL to the program running with PID 1001:

```
$ kill -9 1001
```

The downside to using SIGKILL is that the process receiving it is never given a chance to properly clean up and therefore might leave data files it was using in a corrupted state. For this reason, you should only use this signal when all other signals fail to terminate a process.

# Dealing with Signals

A program can deal with a signal in three ways:

+   - Do nothing and let the default action occur. This is the simplest method for a program to deal with a signal because it requires no extra code.
+   - Ignore the signal and continue executing. This method is not the same as doing nothing because ignoring a signal requires the program to have some code that explicitly ignores the signal.