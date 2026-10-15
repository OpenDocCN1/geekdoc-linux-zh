
```
perror("Fork failed");
    exit(1);
}
/* Parent process */
if (pid > 0) {
    exit(0);
}
/* Child process: Continues and becomes the server */
/* process running forever as a daemon          */
/* Ignore signals */
signal(SIGHUP, SIG_IGN);
signal(SIGINT, SIG_IGN);

/* Set umask */
(void) umask(027);

/* Display Daemon's PID */
(void) sprintf(buf, "Daemon PID: %d\n", getpid());
(void) write(1, buf, strlen(buf));

/* Code for the server */
while (1) {
    /* Wait for a client request */
    /* Serve the client request  */
    sleep(10);      /* Dummy code */
}
```

```
% gcc46 -w daemon.c -o daemon
% ./daemon
Daemon PID: 16624
% kill -0 16624
% ps
  PID TT  STAT      TIME COMMAND
12930 2  Ss     0:00.55 -csh (csh)
16624 2  S      0:00.00 daemon
16639 2  R+     0:00.01 ps
% kill -2 16624
% ps
  PID TT  STAT      TIME COMMAND
12930 2  Ss     0:00.56 -csh (csh)
16624 2  S      0:00.00 daemon
16658 2  R+     0:00.01 ps
% kill -9 16624
% ps
  PID TT  STAT      TIME COMMAND
12930 2  Ss     0:00.58 -csh (csh)
16671 2  R+     0:00.01 ps
%
```

## EXERCISE 21.3

Repeat the preceding shell session to make sure that the daemon.c program works correctly on both PC-BSD and Solaris systems.

## EXERCISE 21.4

What services does inetd, the UNIX superserver, offer on your system? List all the connection-oriented and connectionless services that the configuration file for inetd contains.

## 21.7 RUNNING A SINGLE COPY OF A PROGRAM

In this section, we discuss how we can make sure that only a single copy of a process runs. Some daemons are designed so that only a single copy of the daemon runs. One of the reasons for this may be that the daemon needs exclusive access to an object such as a file or device. There may be other reasons—for example, if multiple instances of cron start running, each would run a scheduled operation. This would not only result in duplicate operations but possibly an error too. Similarly, if a server goes down and two system administrators restart it, then the end result would be unpredictable.

You can ensure that a single instance of a daemon runs by including a code snippet at the beginning of the server program that accesses a lock of some sort. The lock may be a spin lock (i.e., a binary semaphore), a lock for exclusive access of a record, or a lock for exclusive access of a file. The actual code for the service offered by the server is executed only after this lock has been acquired, ensuring that only one copy of the program executes. In UNIX, daemons are usually designed to use a lock file for this purpose. The lock files for UNIX daemons are located in the /var/spool directory in PC-BSD and in the /var/run directory in Solaris.

Files may be locked for mutually exclusive access by using the flock() system call. Here is a brief description of the flock() system call.

```
#include <sys/file.h>
int flock(int fd, int operation);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

Here, fd is the descriptor of an open file and operation specifies the type of access requested. The possible values of the operation argument are shown in Table 21.2. The flock() system call may fail for the reasons listed in Table 21.3.

### TABLE 21.2 Possible Values of the operation Parameter and Their Effect on the File Referred to by the Descriptor fd

| Value of operation | Effect on the File Referred to by fd |
|---|---|
| LOCK_SH | Lock the file for shared access |
| LOCK_EX | Lock the file for mutually exclusive access |
| LOCK_NB | Do not block while locking the file (i.e., nonblocking locking) |
| LOCK_UN | Unlock the file |

### TABLE 21.3 Reasons for flock() to Fail

| Reason for Failure | Value of errno |
|---|---|
| The LOCK_NB option was specified and the file was already locked | EWOULDBLOCK |
| The fd argument is not a valid descriptor | EBADF |
| The fd argument does not refer to a file | EINVAL |
| The fd argument refers to an object that does not support file locking | EOPNOTSUPP |
| No locks are available | ENOLCK |

You can use the following piece of code to lock a file for mutual exclusion. You open or create the LOCKFILE and lock it for exclusive access using the flock() system call. We use the nonblocking call so that if the given file is already locked, the program terminates. Since we do not have write permission to the /var/spool and /var/run directories, we place the lock file in the /usr/home/sarwar/Servers directory—that is, a user's home directory in PC-BSD.

```
#include <sys/file.h>
#include <sys/stat.h>
#define LOCKFILE "/usr/home/sarwar/Servers/testd.lock"
#define LOCKMODE (S_IRUSR|S_IWUSR|S_IWGRP|S_IROTH)
...
/* Open (or create) LOCKFILE */
lock = open(LOCKFILE, O_RDWR | O_CREAT, LOCKMODE);
if (lock < 0) {
    perror("open failed to create LOCKFILE");
    exit(1);
}
/* Lock LOCKFILE for mutually exclusive access */
if (flock(lock, LOCK_EX | LOCK_NB) {
    perror("flock failed to obtain exclusive lock for file");
    exit(1);
}
```

The flock() system call is simple and portable across fork(). However, it is not available on all UNIX platforms, including Solaris. The fcntl() system call may be used for performing such operations on open files that may not be performed with other system calls, including locking files for shared or exclusive access. The fcntl() system call is a little harder to use—it does not hold locks across fork(), the lock on a file is released when a close() system call is used on its descriptor—but it works on most UNIX systems, including Solaris. Here is a brief description of the fcntl() system call.

```
#include <sys/types.h>
#include <unistd.h>
#include <fcntl.h>
int fcntl(int fd, int cmd, /* arg */ ...);
Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```
