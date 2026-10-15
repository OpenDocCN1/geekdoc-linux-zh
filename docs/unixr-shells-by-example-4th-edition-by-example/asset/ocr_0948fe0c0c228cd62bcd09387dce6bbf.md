# EXPLANATION

+   1. The time command will display the total amount of time elapsed to run the command, the time the user part of the program took to run, and the time the kernel spent running the program. The sleep command took 3.15 seconds to run.
+   2. The time is measured for the ps command and wc command.

# 11.15.2 The TMOUT Variable

The TMOUT variable is an integer type. It can be set to force users to type commands within a certain period of time. TMOUT, by default, is set to zero, allowing the user an infinite amount of time to type commands after the PS1 prompt. If TMOUT is set to a value greater than zero, the shell will terminate after the time has expired. Sixty additional seconds will be allotted as the grace period before actually exiting the shell.

# EXAMPLE 11.70

```
$ TMOUT=600
time out in 60 seconds due to inactivity
ksh: timed out waiting for input
```

# EXPLANATION

The TMOUT variable is set to 600 seconds. If the user does nothing for 600 seconds, a message will appear on the screen and then an additional 60 seconds grace period will be allotted before the shell exits. If you do this at the prompt, your current shell exits.