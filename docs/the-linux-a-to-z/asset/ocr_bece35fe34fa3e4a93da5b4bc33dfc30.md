```
#include <unistd.h>
```

```
int select(int nfds, fd_set *rdfds, fd_set *wrfds,
    fd_set *exfds, struct timeval *timeout);
```

where rdfds, wrfds and exfds are the set of read, write and exception handling file descriptors, respectively, that are to be monitored by select(), nfds is the highest numbered file descriptor that needs to be checked and the timeout parameter can cause select() to return early even if no file descriptors are ready.

The fd_sets pointed to by rdfds, wrfds and exfds are modified by the call to show which file descriptors are ready and the select() call returns a total of the number of ready file descriptors.

In order to simplify the setting, resetting and testing of appropriate file descriptor bits within an fd_set a set of macros is defined as follows:

| Macro | Description |
|---|---|
| FD_SET(fd, setptr) | set fd bit pointed to by setptr; |
| FD_CLR(fd, setptr) | clear fd bit pointed to by setptr; |
| FD_ZERO(setptr) | clear all bits pointed to by setptr; |
| FD_ISSET(fd, setptr) | test fd bit pointed to by setptr. |

These macro definitions are made available by including the header file <types.h> in your code.

# Exercises

+   1. Modify the chat program you wrote in the exercises at the end of the socket library case study to use the select() system call to work out when there is something for it to do, rather than repeatedly polling around all of the open socket descriptors to find out if any of them is ready to be read().
2. Implement your own version of the standard date command which displays the current wall clock date and time in a suitable format.
3. Implement your own version of the standard time command which takes another command and parameters as its own command line arguments, executes the given command, and then displays the kernel and user times used by the controlled command during its execution.
4. Write a pair of simple commands which can be set up as setuid root and which will allow ordinary users to mount and unmount a floppy disk at a fixed point in the directory hierachy (say /floppy).

# Answers

+   1. In order to do this, you will need to use the select() system call at the top of the infinite loop in main(). In order to be fully effective the socket