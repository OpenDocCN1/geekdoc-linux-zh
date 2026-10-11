# # Output

```
$ ./blkusr
[kill -USR1 $(pidof ./blkusr)]
caught SIGUSR1
```

The output shows that the handler registered successfully. After it executes, the program exits.

> **TIP**
> 
> SIGUSR1 and SIGUSR2 have been specifically reserved as programmer-defined signals. You should use them to enable special behavior, such as re-reading a configuration file, rather than using a signal handler to redefine one of the standard signals, whose semantics are already well-defined.

# ## Detecting Pending Signals

sigpending allows a process to detect pending signals (signals that were raised while they were blocked) and then decide whether to ignore them or to let them be delivered. Why find out what signals are pending? Suppose you want to write to a file, and the write operation must not be interrupted in order to maintain the file’s integrity. During the write, then, you want to block SIGTERM and SIGQUIT, but ordinarily you want either to handle them or allow their default action. So, before you start the write operation, you block SIGTERM and SIGQUIT. Once the write completes successfully, you check for pending signals and, if SIGTERM or SIGQUIT are pending, you unblock them. Or, you can simply unblock them without bothering to check whether they are pending. Whether to check for pending signals is up to you. If you want to execute a special block of code if a certain signal is pending, check for it. Otherwise, just unblock it.

Like the other signal functions, sigpending is prototyped in <signal.h>sigpending’s prototype is

```
int sigpending(sigset_t *set);
```

The set of pending signals is returned in set. The call itself returns 0 on success and -1 on error. Use sigismember to determine whether the signals in which you are interested are pending, that is, whether they are in set.

# ### Example

![](bbox=[0.03, 0.83, 0.1, 0.89])

# ## Example

For the purposes of demonstration, this program blocks SIGTERM, determines whether it is pending, then ignores it and terminates normally.

```
/*
* pending.c - Fun with sigpending
*/
#include <sys/types.h>
```