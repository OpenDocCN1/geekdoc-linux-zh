+   The process informs the ancestors and descendants that it has ended (with the help of special signals)
+   3.
+   The resources allocated during the fork () call are released
+   4.
+   The scheduler is informed that the context can be switched

You can use either the _exit() system call or its exit() library function to complete the process in applications. This function closes all process threads, correctly releases all resources, and calls _exit() to actually complete it:

```
#include <unistd.h>
void _exit(int status); // status specifies the return code
#include <stdlib.h>
void exit(int status); // status specifies the return code
exit(128);
```

Note that it is better not to call exit() when a process can use resources in conjunction with other processes (for example, it is a descendant process with an ancestor, and a descendant inherited resource descriptors from the ancestor). The reason is that in this case, trying to release the resources in the offspring will result in them being released from the ancestors as well. You must use _exit() to complete these processes.

# Waiting For Process To Complete

When the process is completed, its control block is not immediately removed from the process list and hash and remains there until another process (ancestor) removes it from there. If the process is actually missing in the system (it is finished), but only its control unit, then the process is called a zombie process.

# Waitpid() system call