```
        exit(EXIT_SUCCESS);
    }

    void err_quit(char *msg)
    {
        perror(msg);
        exit(EXIT_FAILURE);
    }
```

![](bbox=[0.04, 0.21, 0.15, 0.27])

# ### Output

```
$  ./mkset
SIGCHLD is in signal mask
SIGTERM not in signal mask
```

mkset first creates an empty signal set, passing the address of a `sigset_t` structure to `sigemptyset`. Next it adds `SIGCHLD` to the process's signal mask. Finally, using `sigismember`, it confirms that `SIGCHLD` is part of the set and that `SIGTERM` is *not* part of the mask.

![](bbox=[0.04, 0.43, 0.13, 0.48])

# ### Example

+   2. This example illustrates the process of removing a signal from a process's signal mask.

```
/*
 *  rmset.c  -Remove signals from a set
 */
#include <signal.h>
#include <stdlib.h>
#include <stdio.h>

void err_quit(char *);

int main(void)
{
    sigset_t newset;

    /* Create the set */
    if((sigfillset(&newset)) < 0)
        err_quit("sigfillset");
    /* Remove SIGALRM from the set */
    if((sigdelset(&newset, SIGALRM)) <0)
        err_quit("sigaddset");
```