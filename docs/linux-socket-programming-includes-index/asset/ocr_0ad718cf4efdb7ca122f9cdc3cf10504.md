# Example

```
void sig_handler(int signum)
{
    switch ( signum )
    {
        case SIGFPE:
...
    }
}

...

if ( signal(SIGFPE, sig_handler) == 0 )
    perror("signal() failed");
```

# sigaction()

Similar to signal(), sigaction() establishes the receiver of certain signals. Unlike signal(), however, this call gives you a lot more control over how the signaling notification behaves. It is also a little more complicated to use.

# Prototype

```
#include <signal.h>
int sigaction(int signum, const struct sigaction *sigact,
              struct sigaction *oldsigact);
```

# Return Value

Zero upon success; otherwise, nonzero.

# Parameters

+   - signum
+     The signal to capture.
+   - sigact
+     The desired behavior and signal handler, using the following structure:
+     ```
+     struct sigaction
+     {
+         void (*sa_handler)(int);
+         sigset_t sa_mask;
+         int sa_flags;
+         void (*sa_restorer)(void);
+     };
+     ```
+   - sa_handler
+     Signal handler function pointer.
+   - sa_mask
+     The set of signals to block while servicing a signal in the signal handler.