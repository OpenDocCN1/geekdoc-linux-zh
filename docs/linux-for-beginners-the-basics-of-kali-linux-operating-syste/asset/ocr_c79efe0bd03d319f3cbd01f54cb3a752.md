For descendant fork () returns zero and for ancestor the id ( pid ) of the created descendant process. When for some reason the descendant was not created, fork () will return -1. Therefore, the normal code for and fork () looks like this:

```
pid_t pid;
if ((pid = fork ()) == -1)
{ /* error, crash */}
if (pid == 0)
{
    // is a descendant
}
else
{
    // this is the ancestor
    printf (" Descendant started with code % d \ n ", pid);
}
```

Once the process is created, it can access the identifying information by a system call to getpid () which returns the current process ID, and getppid (), which returns the process ID of the ancestor.

```
#include <unistd. h>
pid_t mypid, parent_pid;
mypid = getpid ();
parent_pid = getppid ();
```

# Completing The Process

To end the process, UNIX systems use the _ exit () system call. Consider implementing this system call in Linux. The following actions occur during its execution.

+   1. The status of the process shines through TASK _ ZOMBIE

+   2.