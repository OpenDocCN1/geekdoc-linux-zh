```
POSIX #include <unistd.h>
int pause(void);
```

pause( ) suspends a process; it only returns after both a signal has been delivered and the signal handler has returned. pause( ), by definition, is only useful with caught signals—ignored signals are ignored when they come in, and signals with a default action that terminates the process (with or without a core file) still do so.

The problem with the high-level application structure just described is the Process signal part. When that code is running, you don't want to have to handle another signal; you want to finish processing the current signal before going on to the next one. One solution is to structure the signal handler to set a flag and check for that flag within the main loop:

```
volatile sig_atomic_t signal_waiting = 0; /* true if undeliv-with signals */

void handler(int sig)
{
    signal_waiting = 1;
    Set any other data indicating which signal
}
```

In the mainline code, check the flag:

```
for (;;) {
    if (! signal_waiting) {
        pause();
        signal_waiting = 1;
    }
    Determine which signal came in
    signal_waiting = 0;
    Process the signal
}
```

Unfortunately, this code is rife with race conditions:

```
for (;;) {
    if (! signal_waiting) {
        pause();
        signal_waiting = 1;
    }
    Determine which signal came in
    signal_waiting = 0;
    Process the signal
}
```

/* Another signal came in / Signal could arrive here, after condition checked! This code is skipped */ pause() would be called anyway

<---- A signal here could overwrite global data <---- Same here, especially if multiple signals