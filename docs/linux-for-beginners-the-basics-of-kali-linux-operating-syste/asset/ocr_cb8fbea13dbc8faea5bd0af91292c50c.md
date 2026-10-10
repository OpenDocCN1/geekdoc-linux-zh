```
```
}
```
```

This feature becomes a signal processor. The signum parameter determines which signal is sent to the handler (the same handler can be logged for multiple signals by several sigaction ( ) calls ). After logging in, the handler will always be called when it receives the appropriate signal:

```
```
#include <signal.h>
void sigint _handler (int signum)
{
// SIGINT processing
}
// ...... action.sa_handler = sigint_handler;
sigaction (SIGINT, & action, 0);
```
```

If we need to organize the wait for the signal, the simplest way is to open a system call pause ( ). In this case, the process enters standby mode, from which it will output any signal:

```
```
// ask the handlers for help with sigaction ()
pause (); // wait for a signal
```
```

# Signal Generation

Let's consider how to send a process signal. This uses the kill ( ) system call.

```
```
#include (signal.h>
int kill (pid_t pid, // process ID
int signum ); // signal number
```
```

For example, sending a SIGHUP signal to a process pid that is specified at the command line:

```
```
kill ( atoi ( argv [1], SIGHUP );
```
```

# Organization Of Asynchronous Execution Of Processes