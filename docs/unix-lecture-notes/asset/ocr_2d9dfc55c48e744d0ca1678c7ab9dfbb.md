```
/* pid is the pid of the child that terminated */
if (WIFEXITED(status)) {
    printf("Exit status of child %d was %d.\n", pid, WEXITSTATUS(status));
}
else if ( WIFSIGNALED(status) ) {
    signum = WTERMSIG(status);
    printf("Parent: Child %d exited by signal %d.\n",pid, signum);
}
#ifdef WCOREDUMP
    if ( WCOREDUMP(status) )
        printf("Parent: A core dump took place.\n");
#endif
}
}
return 0;
}
```

# Notes.

+   - The parent is in a busy waiting loop in this example, waiting for the child to terminate. The `WNOAHANG` flag to `waitpid()` allows it to continue polling the `waitpid()` call and do something else in the meanwhile. The body of the loop would be replaced with a task that the parent could do while waiting for the child. The advantage of this is that the parent does not have to block, waiting for the child, but can instead do work. If there is no work to do, then this paradigm is not the one to use.
+   - You can send a signal to the child in the same way as for the program in Listing 7.11 to observe that the parent code detects the error return.

# 7.9.5 Non-blocking waits

Instead of calling wait() or waitpid(), a process can establish a SIGCHLD handler that will run when a child terminates. The SIGCHLD handler can then call wait(). This frees the process from having to poll the wait() function. It only calls wait() when it is guaranteed to succeed. The following example (rabbits2.c in the demos directory) demonstrates how this works.

Listing 7.13: rabbits2.c

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>
#include <limits.h>
#include <sys/wait.h>
#include <termios.h>

#define NUM_CHILDREN 5
#define SLEEPTIME 30

/** child() The code that is executed by each child process
```