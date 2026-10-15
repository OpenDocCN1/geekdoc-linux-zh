# 5.3.14  Blocking Signals Temporarily around Critical Sections

The sigprocmask() system call can be used to block or unblock signals sent to a process. This is useful if you need to temporarily turn off all signals in a small section of code. This is one way to create something like a critical section, in the sense that the process will not be interrupted in the middle of the code fragment. It does not prevent the kernel from preempting the process and letting another process run on the CPU, so it does not provide a means of protecting shared variables that might be accessed while the process is removed from the CPU, but it does allow the process to complete some critical sequence of statements without any signal handlers running in the interim, and without being terminated in the midst of it. The prototype is

```
int sigprocmask( int how, const sigset_t *sigs, sigset_t *prev);
```

where how is one of SIG_BLOCK, SIG_UNBLOCK, or SIG_SETMASK. SIG_BLOCK will block the specified signal set, i.e., prevent those signals from reaching until the proc mask is changed. SIG_UNBLOCK allows the signals in the set to be unblocked, and SIG_SETMASK is used to change the mask completely, i.e., assign a new mask to the proc mask. The following program can be run to demonstrate how the blocking works. If you type Ctrl-C during the first loop, the process will continue to loop and it will exit before the second loop is executed. If you change the SIG_BLOCK to SIG_UNBLOCK then the Ctrl-C will kill the process when you type it.

```
```c
#include <signal.h>
#include <stdio.h>

int main()
{
    int i;
    sigset_t sigs, prevsigs;

    sigemptyset(&sigs);
    sigaddset(&sigs, SIGINT);
    sigprocmask(SIG_BLOCK, &sigs, &prevsigs);

    for (i = 0; i < 5; i++) {
        printf("Waiting %d\n", i);
        sleep(1);
    }
    sigprocmask(SIG_SETMASK, &prevsigs, NULL);
    for (i = 0; i < 5; i++) {
        printf("After %d\n", i);
        sleep(1);
    }
}
```
```