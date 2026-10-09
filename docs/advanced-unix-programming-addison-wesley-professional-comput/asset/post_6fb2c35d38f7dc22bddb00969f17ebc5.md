
The differences between the three variants of _exit are:

- _exit and _Exit behave identically in all respects, although technically _exit is from UNIX and _Exit is from Standard C. From now on, I'll refer only to _exit, and you can assume everything I say about it applies to _Exit as well.
- exit (without the underscore) is also from Standard C. It does everything that _exit does and also some higher-level cleanup, including at least calling functions registered with atexit (Section 1.3.4) and flushing standard I/O buffers, as though fflush or fclose were called. (Whether _exit flushes the buffers is implementation defined, so don't count on it.)

As exit is a superset of _exit, everything I say here about the latter applies also to the former, so I'll mostly just talk about _exit.

Usually, you call _exit in a child process that hasn't done an exec, rather than exit, as I showed in execute2 in the previous section, because whatever cleanup processing the child inherited usually should be done only once. But this isn't always true, so you'll have to examine each case to decide what's appropriate. In the most common case, when the child is overwritten by an exec, a program starts fresh, so whatever cleanup it does when it exits is OK. Any buffers or atexit functions from the parent are long gone.

If you're using the “ec” macros for error checking, as I do in this book, remember that the automatic display of an error message and the function trace-back are done in a function registered with atexit that won't be called if you terminate with _exit (Section 1.4.2). In execute2 in the previous section we took care of this by using the EC_FLUSH macro in both parent and child, although only the child calls _exit.

Here are the synopses for the exit functions. Note that there are two different include files involved:

```
_exit—terminate process without cleanup
#include <unistd.h>
    void _exit(            /* exit status */
    int status
    );
    /* Does not return */
```

```
_Exit—terminate process without cleanup
#include <stdlib.h>

void _Exit(
        int status           /* exit status */
);
/* Does not return */
```

```
exit—terminate process with cleanup
#include <stdlib.h>

void exit(
        int status           /* exit status */
);
/* Does not return */
```

_exit and the other two variants terminate the process that issued it, with a status code equal to the rightmost (least significant) byte of status. There are lots of additional side-effects; the principal ones are listed here, and you can find the complete list in [SUS2002]. Actually, these side-effects apply to process termination in general (except for a crash):

- All open file descriptors are closed.
- As explained in Section 4.3, if the process was the controlling process (the session leader), the session loses its controlling terminal. Also, every process in the session gets a hangup (SIGHUP) signal, which, if not caught or ignored, causes them to terminate as well.
- The parent process is notified of the exit status in a manner explained in the next section.
- Child processes aren’t affected in any way directly, except that their new parent is a special system process, and if they execute the getpid (Section 5.13) system call, they’ll get the process-ID of that system process (usually 1).

The exiting process’s parent receives its status code via one of the wait system calls, which are in the next section. The status code is a number from 0 through 255. By convention, 0 means successful termination, and nonzero means abnormal termination of some sort, as defined by the program doing the exiting. Two standard macros are defined, which I’ve already used in many examples in this book: EXIT_SUCCESS is defined as 0, and EXIT_FAILURE is defined as some nonzero value, typically 1. Using the macros instead of integers like 0 and 1 makes programs a bit more readable, which is why we do it that way.

Once a process terminates with an `exit` variant or via a signal, it stops executing but doesn't go away completely until its exit status is reported to its parent, unless the system has determined (in a manner described in the next section) that its parent isn't interested in the status. A terminated process that hasn't yet reported is called a _zombie_.1

## 5.8 wait, waitpid, and waitid System Calls

wait, waitpid, or waitid waits for a child process to change state (stop, continue, or terminate) and then retrieves that process's status. How a process terminates was explained in the previous section; stopped and continued processes were explained in Section 4.3. I'll start with waitpid and then cover the other two variants.

Several of the features described in this and the next section are only in X/Open-conforming systems and, as of this writing, are not yet in FreeBSD or Linux; they're marked with the notation “[X/Open].” (X/Open was discussed in Sections 1.2 and 1.5.1; although Linux as of this writing claims to be X/Open when we test it with feature-test macros, it doesn't have the X/Open functionality described in this section.)

```
waitpid---wait for child process to change state

#include <sys/wait.h>

pid_t waitpid(
	pid_t pid,      /* process or process-group ID */
	int *statusp,   /* pointer to status or NULL */
	int options,    /* options (see below) */
);
/* Returns process ID or 0 on success or -1 on error (sets errno) */
```

The `pid` argument can be used for one of four things:

- `>0`: wait for the child process with that process ID
- `-1`: wait for any child process
- `0`: wait for any child process in the same process group as the calling process
- `<-1`: wait for any child process in the process group whose process-group ID is -pid

Process groups were explained in Section 4.3. Typically, a shell that runs each pipeline in its own process group will set pid to the negative of that process group's ID when waiting for the pipeline to complete so that any process in the pipeline will cause waitpid to return.

When waitpid returns because a child matching the pid argument changed state, the child's process ID is returned. Zero is returned in one case that will be explained below, under the WNOHANG option.

Only direct children—those created with fork—can be waited for. Grandchildren may not be, even if their parent (the direct child) has already terminated. As explained in the previous section, orphaned processes are inherited by a special system process, not by the grandparent.

Normally, it's important for a process to wait for every child it creates—otherwise terminated children remain in the system as zombies until the parent terminates, at which point the system process that inherits them will do the wait and clean them out for good. As some processes don't terminate for a long time (months, sometimes), keeping zombies around for that long really clogs up the system tables. If waiting is too troublesome, a process can use signals to eliminate zombies, as explained in the next section.

A child that changes state, called waitable, can cause at most one return from waitpid. In other words, a waitable child that's waited for is no longer waitable. This means that if one section of the program gets the status and finds out it wasn't from the process it was expecting, there's no way to stuff the result back into the system so some other waitpid will get the status for that process later. (The call waitid can do this, though—see below.)

If waitpid is executed and there's a waitable child that meets the pid specification, waitpid returns immediately. If there is such a child but it hasn't yet changed state, waitpid blocks until there is a suitable waitable child. If there is no child matching pid at all, waitpid returns -1 and sets errno to ECHILD. There might be no child because the pid is simply wrong or because the child has already been waited for, in which case it's no longer waitable (but, again, see waitid).
