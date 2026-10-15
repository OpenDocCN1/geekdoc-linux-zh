
```c
int check_file_status ( int fd )
{
    int flags = fcntl ( fd, F_GETFL );
    if ( -1 === flags ) {
        perror ( "Could not get flags." );
        return ( -1 );
    }

    switch ( flags & O_ACCMODE ) {
    case O_WRONLY:
        printf("write-only\n");
        break;
    case O_RDONLY:
        printf("read-only\n");
        break;
    case O_RDWR:
        printf("read-write\n");
        break;
    }

    if ( flags & O_CREAT )      printf("O_CREAT flag is set\n");
    if ( flags & O_EXCL )       printf("O_EXCL flag is set\n");
    if ( flags & O_NOCTTY )     printf("O_NOCTTY flag is set\n");
    if ( flags & O_TRUNC )      printf("O_TRUNC flag is set\n");
    if ( flags & O_APPEND )     printf("O_APPEND flag is set\n");
    if ( flags & O_NONBLOCK )   printf("O_NONBLOCK flag is set\n");
    if ( flags & O_NDELAY )     printf("O_NDELAY flag is set\n");
#if defined(O_SYNC)
    if ( flags & O_SYNC )       printf("O_SYNC flag is set\n");
#endif
#if defined(O_FSYNC)
    if ( flags & O_FSYNC )      printf("O_FSYNC flag is set\n");
#endif
    if ( flags & O_ASYNC )      printf("O_ASYNC flag is set\n");
    printf("\n");
    return 0;
}
```

As O_SYNC and O_FSYNC are not necessarily defined on all UNIX systems, the tests for these flags are conditionally compiled. You can embed this function into a main program such as

```c
int main(int argc, char *argv[])
{
    int flags, fd;

    if ( argc != 2 ) {
        printf("usage: %s <descriptor#>\n", argv[0]);
        exit(1);
    }
    if ( ( fd = atoi(argv[1])) < 0 ) {
        printf("usage: %s <descriptor#>\n", argv[0]);
        exit(1);
    }
    check_file_status(fd);
    return 0;
}
```

and run the program redirecting standard input, output and error. In the process you will discover some surprising results. For example, if the above program is named checkstatus, try to predict the output of

```
$ ./checkstatus 1 > out1
$ cat out1
```

and of

```
$ ./checkstatus 0
$ ./checkstatus 2 2>errs
```

The point is to determine, when input or output is redirected, how the status flags for the three standard devices, standard input, output, and error, are changed.

## 4.2.2 Appending and Race Conditions

The O_APPEND flag controls append mode. Consider the following problem. A shared log file is used to record various system activities. Each of several different processes adds its own entry to the end of the log file to record its activity.

Let us make this concrete. Recall that UNIX uses the **utmp** file to record each and every login and logout. Each login must be recorded at the end of this file when it occurs. When UNIX starts up, `init()` creates a `getty()` process for each terminal, or some other comparable process in the case of network logins, and when a user logs in at a terminal, the `getty()` or other similar process spawns a `login()` process for that terminal. As a consequence, multiple `login()` processes might exist at any time. Imagine that two users login on different terminals at the exact same time. The two `login()` processes each have to add an entry to the end of the table. To add an entry to the end of a file, the file must be opened for writing, using `O_WRONLY`, or reading and writing, using `O_RDWR`. Thus, a process that needs to add a record to the end of the file must perform the following steps:

- 1. Open the file in read/write mode.
- 2. Seek to the end of the file.
- 3. Write a login record at the position obtained by the seek.

In terms of system calls, this would look something like the following:

```c
fd = open(_PATH_WTMP, O_RDWR);
// error check the open() and if successful then
// create the wtmp record to write ... and then
lseek(fd, 0, SEEK_END);
write(fd, &record, len);
```

The lseek() call obtains the file pointer for the file and sets it to the end of the file at the time the call is made. This pointer is stored in the file structure for the this process's connection to the file. When the process calls write(), the data will be written at the position of this file pointer.

Imagine now that two different processes, identified here as login1 and login2, execute this same sequence of instructions independently and simultaneously. For simplicity, suppose that they run on a one-processor machine and they are time-sliced onto the processor. In particular, suppose the processor executes the following sequence of instructions. The leftmost integer represents the current time in some fixed time unit. login1 executes instructions in the left column; login2, in the right.

| time | login1 | login2 |
|------|--------|--------|
| 0 | fd = open(_PATH_WTMP, O_WRONLY); | |
| 1 | ... | |
| 5 | lseek(fd, 0 SEEK_END); | |
| 6 | | fd = open(_PATH_WTMP, O_WRONLY); |
| 7 | | ... |
| 10 | | lseek(fd, 0 SEEK_END); |
| 11 | | write(fd, &record, len); |
| 12 | write(fd, &record, len); | |

login1 sets the file pointer at time 5. It is removed from the CPU and login2 sets the file pointer to the same position as login1 did, at time 10. It writes to the file at time 11. Then login1 writes to the same position, overwriting the data just written by login2; the record written by login1 replaces the one just written by login2. This is a classic example of a race condition.

Race conditions are removed by using some type of mechanism that will allow a sequence of instructions to be executed as an atomic operation, which simply means that once the first instruction is started, no other process can execute any instruction that accesses any of the shared data until the last instruction is completed. UNIX solves this particular problem by providing write connections with an optional auto-append mode. When auto-append mode (O_APPEND) is enabled, every write operation is preceded immediately and atomically by a seek to the end of the file. This guarantees that each write occurs at the end of the file, regardless of how many other processes are trying to do the same thing simultaneously. Therefore the login and logout processes simply have to open the file in auto-append mode, or enable it after the file is opened with fcntl(). The preceding code would be reduced to the following:

```c
fd = open(_PATH_WTMP, O_WRONLY | O_APPEND);
// create the record to write ...
write(fd, &record, len);
```
