Lines 89–90 initialize *kids*. Line 92 initializes *emptyset*. Lines 94–97 set up and install the signal handler for SIGCHLD. Note the use of SA_NOCLDSTOP on line 94, while line 96 blocks all signals when the handler is running.

Lines 99–100 create a signal set representing just SIGCHLD, and line 102 installs it as the process signal mask for the program.

Lines 104–109 create five child processes, each of which sleeps for three seconds. Along the way, it updates the *kids* array and *nkids* variable.

Line 111 then gives the children a chance to terminate by sleeping longer than they did. (This doesn’t *guarantee* that the children will terminate, but the chances are pretty good.)

Finally, lines 113–114 print a message and then pause, replacing the process signal mask that blocks SIGCHLD with an empty one. This allows the SIGCHLD signal to come through, in turn causing the signal handler to run. Here’s what happens:

```
```
$ ch10-reap1                    Run the program
waiting for signal
Entered childhandler
    reaped process 23937
    reaped process 23938
    reaped process 23939
    reaped process 23940
    reaped process 23941
Exited childhandler
```
```

The signal handler reaps all of the children in one go.

The following program, *ch10-reap2.c* is similar to *ch10-reap1.c*. The difference is that it allows SIGCHLD to arrive at any time. This behavior increases the chance of receiving more than one SIGCHLD but does *not* *guarantee* it. As a result, the signal handler still has to be prepared to reap multiple children in a loop.

```
```c
1   /* ch10-reap2.c -- demonstrate SIGCHLD management, one signal per child */
2
    ... unchanged code omitted ...
12
13  pid_t kids[MAX_KIDS];
14  size_t nkids = 0;
15  size_t kidsleft = 0;                     /* << Added */
16
    ... unchanged code for format_num() omitted ...
41
42  /* childhandler --- catch SIGCHLD, reap all available children */
43
```
```