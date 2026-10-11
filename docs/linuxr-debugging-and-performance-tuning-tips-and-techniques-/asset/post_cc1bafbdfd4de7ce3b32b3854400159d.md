
```c
2226 (
2227 unsigned i;
2228 for (i = 0; i < nsigs; i++)
2229 {
2230 int sig = sigs[i];
2231 #ifndef SA_NOCLDSTOP
2232 sigaction(sig, NULL, &oldact); //Retire old handler
2233 if (oldact.sa_handler != SIG_IGN) //If not ignoring this signal
2234 sigaction(sig, &newact, NULL); //Install our handler
2235 #else
2236 if (signal(sig, SIG_IGN) != SIG_IGN)
2237 signal(sig, sighandler); //Same logic with old API
2238 #endif
2239 }
2240 )
```

We note that lines 2216–2219 and 2221 could be replaced with the single call:

`sigfillset(&newact.sa_mask);`

We don’t know why the code is written the way it is.

Also of interest are lines 2233–2234 and 2236–2237, which show the correct way to check whether a signal is being ignored and to install a handler only if it’s not.

> NOTE The sigaction() API and the signal() API should not be used together for the same signal. Although POSIX goes to great lengths to make it possible to use signal() initially, retrieve a struct sigaction representing the disposition from signal(), and restore it, it’s still a bad idea. Code will be easier to read, write, and understand if you use one API or the other, exclusively.

### 10.6.5 Retrieving Pending Signals: sigpending()

The sigpending() system call, described earlier, lets you retrieve the set of signals that are pending, that is, those that have come in, but are not yet delivered because they were blocked:

```c
#include <signal.h>  POSIX
int sigpending(sigset_t *set);
```

Besides unblocking the pending signals so that they get delivered, you may choose to ignore them. Setting the action for a pending signal to SIG_IGN causes the pending signal to be discarded (even if it was blocked). Similarly, for those signals for which the default action is to ignore the signal, setting the action to SIG_DFL causes such a pending signal to also be discarded.

### 10.6.6 Making Functions Interruptible: siginterrupt()

As a convenience, the `siginterrupt()` function can be used to make functions interruptible for a particular signal or to make them restartable, depending on the value of the second argument. The declaration is:

```c
#include <signal.h> XSI
int siginterrupt(int sig, int flag);
```

According to the POSIX standard, the behavior of `siginterrupt()` is equivalent to the following code:

```c
int siginterrupt(int sig, int flag)
{
    int ret;
    struct sigaction act;

    (void) sigaction(sig, NULL, &act);  // Retrieve old setting

    if (flag)
        act.sa_flags &= ~SA_RESTART;    // If flag is true ... Disable restarting
    else
        act.sa_flags |= SA_RESTART;     // Otherwise ... Enable restarting

    ret = sigaction(sig, &act, NULL);    // Put new setting in place
    return ret;                          // Return result
}
```

The return value is 0 on success or -1 on error.

### 10.6.7 Sending Signals: kill() and killpg()

The traditional Unix function for sending a signal is named `kill()`. The name is something of a misnomer; all it does is send a signal. (Often, the result is that the signal’s recipient dies, but that need not be true. However, it’s way too late now to change the name.) The `killpg()` function sends a signal to a specific process group. The declarations are:

```c
#include <sys/types.h> POSIX
#include <signal.h>

int kill(pid_t pid, int sig);

int killpg(int pgrp, int sig); XSI
```

The sig argument is either a signal name or 0. In the latter case, no signal is sent, but the kernel still performs error checking. In particular, this is the correct way to verify that a given process or process group exists, as well as to verify that you have permission to send signals to the process or process group. `kill()` returns 0 on success and -1 on error; `errno` then indicates the problem.

The rules for the `pid` value are a bit complicated:

- `pid > 0`: The `pid` is a process number, and the signal is sent to that process.
- `pid = 0`: The signal is sent to every process in the sending process's process group.
- `pid = -1`: The signal is sent to every process on the system except for any special system processes. Permission checking still applies. On GNU/Linux systems, only the `init` process (PID 1) is excluded, but other systems may have other special processes.
- `pid < -1`: The signal is sent to the process group represented by the absolute value of `pid`. Thus, you can send a signal to an entire process group, duplicating `killpg()`'s functionality. This nonorthogonality provides historical compatibility.

The meanings of `pid` for `kill()` are similar to those of `waitpid()` (see Section 9.1.6.1, “Using POSIX Functions: wait() and waitpid(),” page 306).

The Standard C function `raise()` is essentially equivalent to

```c
int raise(int sig) {
    return kill(getpid(), sig);
}
```

The C standards committee chose the name `raise()` because C also has to work in non-Unix environments, and `kill()` was considered specific to Unix. It was also a good opportunity to use a more descriptive name for the function.

`killpg()` sends a signal to a process group. As long as the `pgrep` value is greater than 1, it’s equivalent to `kill(-pgrep, sig)`. The GNU/Linux `killpg(2)` manpage states that if `pgrep` is 0, the signal is sent to the sending process’s process group. (This is the same as `kill()`.)

As you might imagine, you cannot send signals to arbitrary processes (unless you are the superuser, `root`). For ordinary users, the real or effective UID of the sending process must match the real or saved set-user-ID of the receiving process. (The different UIDs are described in Section 11.1.1, “Real and Effective IDs,” page 405.)

However, `SIGCONT` is a special case: As long as the receiving process is a member of the same session as the sender, the signal will go through. (Sessions were described briefly in Section 9.2.1, “Job Control Overview,” page 312.) This special rule allows a job control shell to continue a stopped descendant process, even if that stopped process is running with a different user ID.

### 10.6.8 Our Story So Far, Episode II

The System V Release 3 API was intended to remedy the various problems presented by the original V7 signal APIs. The notion of signal blocking, in particular, is an important additional concept.

However, those APIs didn’t go far enough, since they worked on only one signal at a time, leaving wide open plenty of windows through which undesired signals could arrive. The POSIX APIs, by working atomically on multiple signals (the process signal mask, represented programmatically by the sigset\_t type), solves this problem, closing the windows.

The first set of functions we examined manipulate sigset\_t values: sigfillset(), sigemptysigset(), sigaddset(), sigdelset(), and sigismember().

The next set works with the process signal mask: sigprocmask() sets and retrieves the process signal mask, sigpending() retrieves the set of pending signals, and sigsusp pend() puts a process to sleep, temporarily replacing the process signal mask with the one in its parameter.

The POSIX sigaction() API is (severely) complicated by the need to supply

- Backward-compatible behavior: SA\_RESETHAND and SA\_RESTART in the sa\_flags field.
- A choice as to whether or not the received signal is also blocked: SA\_NODEFER for sa\_flags.
- The ability to have two different kinds of signal handlers: one-argument or three-argument.
- A choice of behaviors for managing SIGCHLD: SA\_NOCLODSP and SA\_NODWAIT for sa\_flags.

The siginterrupt() function is a convenience API for enabling or disabling restartable system calls for a given signal.

Finally, kill() and killpg() can be used to send signals, not just to the current process but to other processes as well (permissions permitting, of course).

## 10.7 Signals for Interprocess Communication

> “THIS IS A TERRIBLE IDEA! SIGNALS ARE NOT MEANT FOR THIS! Just say NO.”
> —Geoff Collyer—

One of the primary mechanisms for interprocess communication (IPC) is the pipe, which is described in Section 9.3, “Basic Interprocess Communication: Pipes and FIFOs,” page 315. It is possible to use signals for very simple IPC as well. Doing so is rather clumsy; the recipient can only tell that a particular signal came in. While the sigaction() API does allow the recipient to learn the PID and owner of the process that sent the signal, such information usually isn’t terribly helpful.

> NOTE As the opening quote indicates, using signals for IPC is almost always a bad idea. We recommend avoiding it if possible. But our goal is to teach you how to use the Linux/Unix facilities, including their negative points, leaving it to you to make an informed decision about what to use.

Signals as IPC may sometimes be the only choice for many programs. In particular, pipes are not an option if two communicating programs were not started by a common parent, and FIFO files may not be an option if one of the communicating programs only works with standard input and output. (One instance in which signals are commonly used is with certain system daemon programs, such as xinetd, which accepts several signals advising that it should reread its control file, do a consistency check, and so on. See xinetd(8) on a GNU/Linux system, and inetd(8) on a Unix system.)

The typical high-level structure of a signal-based application looks like this:

```c
for ( ; ; ) {
    Wait for signal
    Process signal
}
```

The original V7 interface to wait for a signal is pause():

5 Our thanks to Ulrich Drepper for helping us understand the issues involved.
