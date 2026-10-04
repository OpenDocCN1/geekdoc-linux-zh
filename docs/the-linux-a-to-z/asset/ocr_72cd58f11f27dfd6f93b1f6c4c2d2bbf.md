passed into sigaction(). This is just a pointer to another struct sigaction which will be filled by the sigaction() call with the details from the old sigaction structure. This allows the old values to be restored later if required.

# 19.2.1 Special SIGCHLD Behavior

Sometimes you will want to run a process which generates lots of child processes but which does not wish to wait() for them. By default, child processes in this position will become zombies until some process (probably init) waits for them in the future. If the parent is a very long lived process then the zombies will be hanging around in the system for a long time. The creation of zombies under these circumstances just wastes system resources. There are several ways round the problem under Linux, the simplest being to set the action of the SIGCHLD signal to SIG_IGN, as follows:

```
signal(SIGCHLD, SIG_IGN);
```

As the default action of SIGCHLD is to be ignored anyway, setting this signal to SIG_IGN serves no other useful purpose. This is therefore used as a special feature in Linux to tell the kernel not to generate zombies from the children of the calling process.

# 19.2.2 Signal Masks

Setting and modifying signal masks is performed by a special set of functions, whose prototypes are:

```
#include <signal.h>

int sigemptyset(sigset_t *mask);
int sigfillset(sigset_t *mask);
int sigaddset(sigset_t *mask, int signum);
int sigdelset(sigset_t *mask, int signum);
int sigismember(sigset_t *mask, int signum);
```

The sigemptyset() function takes a pointer (mask) to a signal mask (of type sigset_t) and clears it to ensure that no signals are flagged as blocked. The function sigfillset() fills a signal mask to ensure that all signals are flagged as blocked. The sigaddset() and sigdelset() functions allow signal blocks for individual signals (signum) to be added and deleted respectively. The final function (sigismember()) allows you to determine if a particular signum is flagged as blocked in *mask.

A process can also change and examine the value of its own signal mask using the sigprocmask() system call: