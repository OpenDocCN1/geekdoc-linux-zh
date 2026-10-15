

group leaders can do this. Since the server is now a child of the original process, it is neither, so it can call setsid(), which makes it a session leader of a new session and a group leader of a new process group.

- 3. Registering its intent to ignore SIGHUP.
- 4. Forking another child process, terminating in the parent again, and letting the new child, which is the grandchild of the original process, execute the server code. In some versions of UNIX, when a session leader opens a terminal device (which it may want to do sometimes), that terminal is automatically made the control terminal for the process. By running as the child of a session leader, the server is now immune from this eventuality. In Linux, a process can set the O_NOCTTY flag on open() to prevent this. The reason for ignoring SIGHUP is that when a session leader terminates, all of its children are sent a SIGHUP, which would otherwise kill them. Since the parent is a session leader, the child must ignore SIGHUP.
- 5. Changing the working directory to "/".
- 6. Clearing the umask.
- 7. Closing any open file descriptors.

A procedure for doing all of these steps, based on one from [Stevens], is below.

## Listing 8.17: daemon_init.c

```
void daemon_init(const char *pname, int facility)
{
    int     i;
    pid_t   pid;

    if ( (pid = fork()) == -1) {
        perror("fork");
        exit(1);
    }
    else if (pid != 0)
        exit(0);            /* parent terminates */

    /* Child continues from here */
    /* Detach itself and make itself a session leader */
    setsid();

    /* Ignore SIGHUP */
    signal(SIGHUP, SIG_IGN);

    if ( (pid = fork()) == -1) {
        perror("fork");
        exit(1);
    }
    else if ( pid != 0 )
        exit(0);    /* First child terminates */

    /* Grandchild continues from here */
    chdir("/");         /* change working directory */
```

```
umask(0); /* clear our file mode creation mask */

/* Close all open file descriptors */
for (i = 0; i < MAXFD; i++)
    close(i);

/* Start logging with syslog() */
openlog(pname, LOG_PID, facility);
}
```

The final version of the upcase server incorporates this function and turns itself into a daemon. The only changes required are to include this function into the code and insert the line

```
daemon_init(argv[0], 0);
```

before the first executable statement.

## 8.6 Multiplexed I/O With select

Imagine the situation in which a process has multiple sources of input open for reading, such as a set of pipes as well as the terminal. Suppose the process has to respond to commands typed at the terminal as well as display messages that are available in the pipes. This is what is meant by multiplexed input: when a process has to obtain input available from multiple sources simultaneously. One solution would be to make all of the reads non-blocking and to continually poll each descriptor to see if there is data ready for reading on it. Polling, though, has many drawbacks, as we have seen, the most important of which is that it is wasteful of the CPU resource.

Another alternative would be to use asynchronous reads on each descriptor. This is also possible, but quite messy to code, and has the drawback that it relies on signals which may not be handled properly or reliably.

It is for these reasons that the select() system call was developed. Basically, the select() call allows a process to listen to multiple descriptors at once and to be notified when any one of them have pending input or output. Roughly put, select() is given a set of masks of file descriptors, representing I/O devices or files in which the process is interested. When input or output is ready on any of them, the appropriate bits in these masks are set. The process can check the masks to see which I/O is ready and can then read or write the ready descriptors. The select() call works with any file descriptor, so that it can be used with files, pipes, FIFOs, devices, and sockets.

select() is fairly complex:

```
/* According to POSIX.1-2001 */
#include <sys/select.h>

/* According to earlier standards */
```

> There is a similar call named poll().

