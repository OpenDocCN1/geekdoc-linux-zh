
```
write(1, &s, s_len);
write(1, &x, n+1);
printf("\n");
}
}
} // while
return 0;
}

void interrupt_handler (int signo, siginfo_t *info, void *context)
{
    int     localid;      /* stores a number to uniquely identify signal */
    time_t  timenow;      /* current time -- used to generate id */
    static  int ticker = 0; /* used for id also */
    struct tm *tp;

    time(&timenow);
    tp = localtime(&timenow);
    localid = 36000*tp->tm_hour + 600*tp->tm_min + 10*tp->tm_sec +
              ticker++ % 10;
    printf("Entered handler: sig = %d \tid = %d\n",
           info->si_signo, localid);
    sleep(3);
    printf("Leaving handler: sig = %d \tid = %d\n",
           info->si_signo, localid);
}
```

The while loop in the main program exists just to demonstrate that the system calls to perform I/O are restarted when the interrupts occur. You can run this program with any combination of SA_RESTART, SA_RESETHAND, and SA_NODEFER to see the combined effect of the flags. You can add any signal to the blocked set, but you will only be able to send SIGINT and SIGQUIT unless you open a separate window and use the kill command to send arbitrary signals to the process. You can try this – put signal 4 in the blocked set and issue kill -4 with the process id from a second window while the process is handling a Ctrl-C. You will see that signal 4 is blocked until interrupt_handler() finishes.

The while loop is designed so that you do not have to kill this program to terminate it. If you type "quit" it will terminate.

## 5.3.13 Creating Signal Mask Sets

There are four functions that modify signal mask sets:

```
sigemptyset(sigset_t *set);
sigfillset(sigset_t *set);
sigaddset(sigset_t *set, int signum);
sigdelset(sigset_t *set, int signum);
```

The first two create empty and full mask sets respectively. The next two add or delete specific signals from the specified sets. You can either create an empty mask and add to it, or create a full mask and delete from it. If you plan on having more than half of the signals in it, then do the latter, otherwise do the former.

## 5.3.14 Blocking Signals Temporarily around Critical Sections

The sigprocmask() system call can be used to block or unblock signals sent to a process. This is useful if you need to temporarily turn off all signals in a small section of code. This is one way to create something like a critical section, in the sense that the process will not be interrupted in the middle of the code fragment. It does not prevent the kernel from preempting the process and letting another process run on the CPU, so it does not provide a means of protecting shared variables that might be accessed while the process is removed from the CPU, but it does allow the process to complete some critical sequence of statements without any signal handlers running in the interim, and without being terminated in the midst of it. The prototype is

```
int sigprocmask( int how, const sigset_t *sigs, sigset_t *prev);
```

where how is one of SIG_BLOCK, SIG_UNBLOCK, or SIG_SETMASK. SIG_BLOCK will block the specified signal set, i.e., prevent those signals from reaching until the proc mask is changed. SIG_UNBLOCK allows the signals in the set to be unblocked, and SIG_SETMASK is used to change the mask completely, i.e., assign a new mask to the proc mask. The following program can be run to demonstrate how the blocking works. If you type Ctrl-C during the first loop, the process will continue to loop and it will exit before the second loop is executed. If you change the SIG_BLOCK to SIG_UNBLOCK then the Ctrl-C will kill the process when you type it.

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
