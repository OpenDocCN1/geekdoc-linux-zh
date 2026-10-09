```
```
printf("parent\n");
ec_negl( close(pfd[0]) )
ec_negl( close(pfd[1]) )
return;

EC_CLEANUP_BGN
        EC_FLUSH("try6")
EC_CLEANUP_END
}
```
```

Here the child blocks in read until the parent closes the writing end of the pipe, resulting in the child getting a zero return.

# ## 9.3  Miscellaneous Signal System Calls

You can find out whether a signal is pending with `sigpending`, which returns a set of the pending signals:

```
**sigpending**—examine pending signals
```c
#include <signal.h>

int sigpending(
        sigset_t *set        /* returned set of pending signals */
); /* Returns 0 on success or -1 on error (sets errno) */
```
```

You can test which signals are pending by using `sigismember` (Section 9.1.5) on the returned set. Of course, it may not still be pending by the time you test it unless it’s blocked.

Recall from Section 9.1.6 that the SA_ONSTACK flag arranges for a signal’s handler to execute on an alternate stack. You manage the stack with `sigaltstack`:

```
**sigaltstack**—set and get alternate stack context
```c
#include <signal.h>

int sigaltstack(
        const stack_t *stack,      /* new stack */
                stack_t *ostack    /* old stack */
); /* Returns 0 on success or -1 on error (sets errno) */
```
```

See your system’s documentation or the SUS for details of this system call.