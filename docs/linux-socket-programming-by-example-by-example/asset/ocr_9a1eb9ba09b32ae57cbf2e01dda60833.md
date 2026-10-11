Some programmers prefer, however, to explicitly describe the protocol argument value. This might be important for certain applications in which a specific protocol is required, and no substitution is permitted. This allows you to choose the final protocol used rather than rely on today's “kernel of the month.” The downside of this is that when networks and protocols evolve, someone might have to go back and revisit your source code to make it work.

In this book, you'll learn about the only four combinations you'll need to use.

# ## Using PF_LOCAL and SOCK_STREAM

You will use a zero for the protocol argument in the socket(2) or socketpair(2) functions for PF_LOCAL sockets. This is the only supported value for that argument. A valid socket(2) call using PF_LOCAL and SOCK_STREAM is shown as follows:

```
```
int s;

s = socket(PF_LOCAL, SOCK_STREAM, 0);

if (s == -1)
	perror("socket()");
```
```

This creates a stream socket to allow one process to communicate with another process within the same host. The steps are

+   1. Integer **s** is declared to receive the socket number (it is treated the same as a file descriptor).

+   2. The **socket(2)** function is called. The domain argument is set to PF_LOCAL, and the socket type argument is set to SOCK_STREAM to request a stream socket. The protocol argument is set to zero, which is the only valid value for PF_LOCAL sockets.

+   3. The value s is tested to see whether it is the value -1. If it is, then an error has occurred, and errno has the reason for it. Function perror(3) is used in this example to report what the errno code indicates.

+   4. If s is not -1, then it represents a valid socket. It can be used in most places in which a file descriptor is valid (in read(2) and write(2) function calls, for example).

> **NOTE**
> At the present time, zero is the only valid value for the protocol argument of the socket(2) or socketpair(2) function calls, when the domain argument is PF_LOCAL (or PF_UNIX).