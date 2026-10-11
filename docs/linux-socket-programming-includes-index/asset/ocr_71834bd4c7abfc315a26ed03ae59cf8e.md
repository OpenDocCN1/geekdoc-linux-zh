Parameter
**mutex** The semaphore variable

Possible Errors
**EINVAL** The mutex has not been properly initialized.
**EPERM** The calling thread does not own the mutex (error-checking mutexes only).

Example
(see **pthread_mutex_lock()**)

# # Signals

When working with tasks, your program may get signals (or asynchronous notifications). This section describes system calls that let you capture and process them.

# ## signal()

Register the **sig_fn** routine to answer the **signum** signal. The default behavior is a single shot; the signal handler reverts to the default after getting the first signal. Use **sigation()** instead if you want to control the behavior more.

**Prototype**

```
```
#include <signal.h>
void (*signal(int signum, void (*sig_fn)(int signum)))(int signum);
- or -
typedef void (*TSigFn)(int signum);
TSigFn signal(int signum, TSigFn sig_fn);
```
```

**Return Value**
A positive value if successful. If the thread-create call encountered any errors, the call returns a negative value and sets **errno** to the error.

**Parameters**
**signum** The signal number to capture
**sig_fn** The program routine that the schedule calls

**Possible Error**
(**errno** not set)