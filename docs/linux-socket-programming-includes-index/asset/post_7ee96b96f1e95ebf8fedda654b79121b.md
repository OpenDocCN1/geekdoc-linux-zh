
## LISTING 7.10 Continued

```c
close(FDs[0]); /* not needed now */
close(FDs[1]); /* no writing to parent */

read(0, buffer, sizeof(buffer));/* get message from parent */
/*
 */---do processing---*/
printf("My report...");
exit(0);
close(FDs[1]);
```

## LISTING 7.11 Creating Pipes in a Child Thread

```c
/************************************/
/***          Child Thread         ***/
int FDs[2];    /* create the place holder for the new pipe */
pipe(FDs); /* create the pipe: FDs[0]=input, FDs[1]=output */
char buffer[1024];

/*---Create the child process---*/

read(FDs[0], buffer, sizeof(buffer));/* get msg from parent */
/*---do processing---*/
printf("My report...");
/*
 */
close(FDs[0]); /* close input pipe */
close(FDs[1]); /* close output pipe */

pthread_exit(arg);
```

You can create a pipe between two tasks using Figure 7.2 as a guide; use the following steps to further understand what is happening.

1. The parent declares a file descriptor array. When you call the pipe() system call, the call places the descriptors in this array.
2. The parent creates the pipe. The kernel creates a queue and places the reading descriptor in fd[0] and the writing descriptor in fd[1].

![](img/2591af4bdf00a0f382331fc9481f785e_173_0.png)

### FIGURE 7.2

When you create a pipe between tasks, you have to follow a particular sequence of redirecting and closing channels.

## Using Pipes Requires Closing One End

When the system creates a pipe, it connects the input channel to the output channel: The pipe effectively loops in on itself—whatever the program writes can be read by the same task (as if it were talking to itself). The same message still goes to the child, but the parent sees its own message in the input. Most communication paths are in one direction: the parent telling the child what it should process, so your process closes the unneeded channels. However, if you want true bi-directional communication, you need to call `pipe()` twice—one pipe for each direction (see Figure 7.3).

3. The parent spawns the new task. The process gets an exact copy of everything (including the pipe). The pipe between the parent and child is inherited.
4. The parent communicates with the child using the file descriptor array.
5. The child process redirects its own standard input (this is optional) and communicates with the parent using the open pipe. It also closes the output channel.
6. The parent needs only the output channel of the pipe to communicate with the child, so it closes the input channel.

You cannot redirect the I/O channels in threads because they share the file descriptor tables. This means that if you close the file in one thread, you essentially close it in all other threads of your program. Processes, on the other hand, make a copy of the file descriptor tables, so closing one channel does not affect the other processes in the program.

Figure 7.2 showed you how to create a unidirectional connection between a parent and the child. To create a bi-directional connection, you need to follow Figure 7.3.

Refer to this diagram to help you create pipes and redirection for your programming.

## Signaling a Course Change: Folding

The poker game has few direct, asynchronous controls. A player can fold (step out of the current game) at any time. If the game were held in the Old West, a cheater might meet a sudden, asynchronous termination. In any case, the dealer picks up the dropped cards. Likewise, after you have started a process, you can change its course or your parent task can get notified of termination with signals.

Every task you program should handle all useful signals. There are approximately 30 different kinds of signals (two signals are user-defined). Most signals you can ignore or not capture because the likelihood that they occur is slim or to capture them is not meaningful. Many uncaught signals usually terminate your program, and some of these are important to multi-tasking programs. For example, the system notifies the parent when a child terminates with a `SIGCHLD` signal.

![](img/2591af4bdf00a0f382331fc9481f785e_175_0.png)

### FIGURE 7.3

*Your program can create an additional connection back if you want bi-directional communication between the parent and the child.*

A signal is similar to an interrupt; the only information is that the signal occurred. When the signal arrives, the task stops what it is doing and jumps to a specified routine (called a *signal handler*). For **SIGHUP**, you can call *wait()* to clean up the child's termination. You also can support other signals, such as math errors or Ctrl+C breaks.

Linux supports two styles of signals: System V (a one-shot signal that reverts back to its default handler when the system calls your custom handler) and BSD (that keeps its handler until told otherwise). If you use the *signal()* system call, the single-shot is the default. You may not be interested in this feature—you should expect to capture the signal repeatedly.

## Resetting the Signal Handler

To reset the handler, some programs used to fix the one-shot System-V behavior by placing a call to the signal system call directly in the signal handler. *Unfortunately*, this can create a race condition; a signal could come in before the call to reset it. As a result, the signal may be lost.

Instead of using *signal()*, the preferred system call is *sigaction()*. The *sigaction()* system call provides you more control over the behavior of the signal subsystem. The following is its prototype:

```c
#include <signal.h>
int sigaction(int sig_num, const struct sigaction *action,
    const struct sigaction *old);
```

You use the first parameter to define which signal to capture. The second parameter defines how you want to handle the signal. If you set the last parameter to a *non-NULL* value, the call stores the last action definition. The structure definition for the second and third parameters is as follows:

```c
struct sigaction
{
    /* Function pointer to handler */
    void (*sa_handler)(int signum);
    /* Specialized sigaction callback */
    void (*sa_sigaction)(int, siginfo_t *, void *);
    /* Bit array of signals to block while in handler */
    sigset_t sa_mask;
    /* behavior to perform */
    int sa_flags;
    /* (deprecated--set to zero) */
    void (*sa_restorer)(void);
};
```

## The Server Perspective and Load Control

To use this structure, you set the first field (sa_handler) to different values than a function pointer. If you place SIG_IGN in this field, the program ignores the specific incoming signal. Also, the program returns the behavior to the default if you use SIG_DFL.

To permit or deny cascading signals (one signal interrupting another), use the second field, sa_mask. Each bit (there are 1,024 possible bits) represents a signal to permit (1) or block (0). By default, a specific signal blocks like signals while servicing the first. For example, if you are servicing a SIGCHLD signal and another process terminates, your handler ignores that signal by default. You can change that behavior with SA_NOMASK.

The sa_flags determine the behavior of the handler. Most of the time, you can set it to zero:

- **SA_ONESHOT** Use the System V behavior of resetting the handler once a signal is caught.
- **SA_RESHAND** Same as SA_ONESHOT.
- **SA_RESTART** Restart some system calls if a signal interrupts it. Use this flag to restart system calls such as accept().
- **SA_NOMASK** Allow the same signal to interrupt while handling an earlier signal.
- **SA_NODEFER** Same as SA_NOMASK.
- **SA_NOCLDSTOP** Does not notify parent if a child process just stops (SIGSTOP, SIGSTP, SIGTTIN, or SIGTTTOU). This flag is important for this chapter.

Listing 7.12 shows an example of how to capture the SIGFPE (float-point exception) and ignore the SIGINT (keyboard interrupt).

## LISTING 7.12 SIGFPE and SIGINT Handler Example

```c
/***/
/** Capturing SIGFPE and ignoring SIGINT example */
/***/

#include <signal.h>

/* Define the signal catcher */
void sig_catcher(int sig)
{ printf("I caught signal #%d\n", sig); }

int main(void)
{ struct sigaction act;

bzero(&act, sizeof(act));
act.sa_handler = sig_catcher;

sigaction (SIGFPE, &act, 0); /* Capture a float error */
```
