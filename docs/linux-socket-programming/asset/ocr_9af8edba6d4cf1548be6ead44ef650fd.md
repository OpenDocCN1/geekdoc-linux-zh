# Prototype

```
#include <signal.h>
void (*signal(int sig_num, void (*sig_fn)(int sig_num)))(int sig_num);
-Or-
typedef void (*TSigFn)(int sig_num);
TSigFn signal(int sig_num, TSigFn sig_fn);
```

# Return Value

A positive value if successful. If the thread-create call encountered any errors, the call returns a negative value and sets `errno` to the error.

# Parameters

| sig_num | The signal number to capture |
| :------ | :-------------------------- |
| sig_fn  | The program routine that the schedule calls |

# Possible Error

(`errno` not set)

# Example

```
void sig_handler(int sig_num)
{
    switch( sig_num )
    {
        case SIGFPE:
    }
    ...
}
...
if( signal(SIGFPE, sig_handler) == 0 )
    perror("signal() failed");
```

# sigaction()

Similar to `signal()`, `sigaction()` establishes the receiver of certain signals. Unlike `signal()`, however, this call gives you a lot more control over how the signaling notification behaves. It is also a little more complicated to use.

# Prototypes

```
#include <signal.h>
int sigaction(int sig_num, const struct sigaction *sigact,
               struct sigaction *oldsigact);
```

# Return Value