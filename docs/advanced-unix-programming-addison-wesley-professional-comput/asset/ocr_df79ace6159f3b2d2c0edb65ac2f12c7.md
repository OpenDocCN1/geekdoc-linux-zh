`tcgetsid` is only on SUS systems, so it isn't available on FreeBSD. You can get the session ID from a file descriptor open to the controlling terminal, however, first by calling `tcgetpgrp` to get the foreground process group ID, and then, since that must be the process ID of a process in the session, you can call `getsid` to get the session ID.

# **4.3.5 Using the Session-Related System Calls**

Here's a function that prints lots of session- and process-group-related information using the previous system calls:

```
```c
#include <termios.h>

static void showpginfo(const char *msg)
{
    int fd;

    printf("%s\n", msg);
    printf("\tprocess ID = %ld; parent = %ld\n",
           (long)getpid(), (long)getppid());
    printf("\tsession ID = %ld; process-group ID = %ld\n",
           (long)getsid(0), (long)getpgid(0));
    ec_negl( fd = open("/dev/tty", O_RDWR) )
    printf("\tcontrolling terminal's foreground process-group ID = %ld\n",
           (long)tcgetpgrp(fd));
#if _XOPEN_VERSION >= 4
    printf("\tcontrolling-terminal's session ID = %ld\n",
           (long)tcgetsid(fd));
#else
    printf("\tcontrolling-terminal's session ID = %ld\n",
           (long)getsid(tcgetpgrp(fd)));
#endif
    ec_negl( close(fd) )
    return;

    EC_CLEANUP_BGN
        EC_FLUSH("showpginfo")
    EC_CLEANUP_END
}
```

```

We want to call `showpginfo` when the process starts up and when it gets a `SIGCONT` signal so we can see what's going on when it's running in the background. I'm not going to tell much about signal catching until Chapter 9, and all you need to know for now is that the initializing of the structure and the call of `sigaction` arranges for the function `catchsig` to be executed when a