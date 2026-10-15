
The cmd argument is the operation to be performed on the open file with descriptor fd. The data type, value, and use of the last argument depend on the value of the cmd argument. In this section, we are only interested in discussing commands that are used for file locking. There are two commands that may be used for this purpose: F_SETLK and F_SETLKW. Each command sets or clears a file segment lock according to the description of the lock given in the third argument via a pointer to a variable of type struct flock. The lock may be shared (read) or exclusive (write).

With F_SETLK as the third argument, the fcntl() call returns immediately with a value of −1 if a lock cannot be set. The F_SETLKW command is similar to the F_SETLK command, except that in the case of F_SETLKW the calling process waits (i.e., blocks) if other locks have blocked a shared or mutually exclusive lock. The process stays blocked until the request is satisfied. During this wait, if fcntl() is interrupted, it returns −1 and errno is set to EINTR.

The flock structure has at least the following fields:

```
struct flock {
    short   l_type;    /* lock operation type                 */
    short   l_whence;  /* lock base indicator                 */
    off_t   l_start;   /* starting offset from base           */
    off_t   l_len;     /* lock length in consecutive bytes;   */
                     /* l_len == 0 means until end of file  */
    int     l_sysid;   /* system ID running process holding lock */
    pid_t   l_pid;     /* process ID of process holding lock  */
    ...
}
```

The value of l_whence may be SEEK_SET, SEEK_CUR, or SEEK_END, to indicate that the relative offset l_start bytes is from the start of the file, the current position of the file pointer, or the EOF, respectively. The file will be locked if l_len and l_start are set to 0 each and l_whence is set to SEEK_SET. The l_type field is set to F_RDLCK for shared (read) lock and F_WRLCK for exclusive (write) lock.

In order for our code to be portable to Solaris, we have made a few changes to it. These changes are as follows. After these changes have been made, the code will run on both PC-BSD and Solaris systems.

- 1. Include the following header files in the already existing list of header files.
  #include <fcntl.h>
  #include <unistd.h>
  #include <sys/file.h>
  #include <sys/stat.h>
- 2. Create the ~/Servers directory on your system.
- 3. The preprocessor directive to define LOCKFILE on Solaris and PC-BSD systems should be as follows:

```
#ifdef __sun
#define LOCKFILE "/export/home/sarwar/Servers/testd.lock"
#else
#define LOCKFILE "/usr/home/sarwar/Servers/testd.lock"
#endif
```

- 4. Use a variable of the struct flock type.

```
struct flock lock;
```

- 5. The conditional compilation of file-locking code for Solaris and PC-BSD replaces the code for file locking on PC-BSD.

```
#ifdef __sun
    /* Set lock */
    lock.l_start = 0;
    lock.l_len = 0;
    lock.l_type = F_WRLCK;
    lock.l_whence = SEEK_SET;

    /* Lock LOCKFILE for mutually exclusive access */
    if (fcntl(lockfd, F_SETLK, &lock)) {
        perror("Daemon already running");
        close(lockfd);
        exit(1);
    }
#else
    /* Lock LOCKFILE for mutually exclusive access */
    if (flock(lock, LOCK_EX | LOCK_NB)) {
        perror("Daemon already running");
        close(lockfd);
        exit(1);
    }
#endif
```

We enhance the daemon.c program discussed in Section 21.6 with the code fragments discussed in this section, according to steps a) to e), for compilation and execution on both PC-BSD and Solaris machines. The following session shows the new version of the daemon.c program, its compilation, and the running of the executable code on a PC-BSD machine. The program works correctly on our Solaris machine too. Because of the lock, only one instance of the daemon may run at any given time.

```
% cat lock_daemon.c
#include <fcntl.h>
#include <unistd.h>
#include <sys/file.h>
#include <sys/signal.h>
#include <sys/stat.h>
```
