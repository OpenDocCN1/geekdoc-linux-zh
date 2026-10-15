```
/* Now fork the child processes. Check return values and exit if we have a problem. Note that the exit() may be executed only for some children and not others. */
for ( i = 0; i < N; i++ )
    if ( -1 == fork() )
        exit(1);

/* Create the output string that the process wil/ write, and write using system call. */
sprintf(str, "Process id = %d\n", getpid());
write(1, str, strlen(str));
fflush(stdout);        /* to force output before shell prompt */
sleep(1);              /* to give time to the shell to display prompt */
return 0;
}
```

# 7.7.1 Other Versions of fork()

The vfork() system call is a different version of the fork() call that is designed to be more efficient. Rather than making a complete copy of the address space of the old process, the vfork() call creates a new process without copying the data and stack segments of the parent and instead allows the child process to share these. This saves time and memory but also raises the possibility that the child will inadvertently corrupt the state of the parent process. It is not intended to be used to allow the child and parent to share data; on the contrary, its purpose is to avoid the extensive memory copying in the case that the child will replace its code anyway using exec() (to be discussed soon.)

There is also a clone() system call in Linux systems. The clone() function, which is technically a library routine wrapping a system call, allows the child to share the address space with its parent, and also lets the programmer pass a function and arguments for the child to execute. We will look at it in detail later.

# 7.7.2 Synchronizing Processes with Signals

The next program, synchdemo1.c, demonstrates how to use fork() and signals to synchronize a child and its parent.

# Listing 7.5: synchdemo1.c

```
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <sys/types.h>
#include <sys/wait.h>

void c_action(int signum)
{
    /* nothing to do here */
}
/**************************************************************/
```