
```
{
    int pid;

    pid = fork();
    if (pid == -1) {
        perror("Fork failed");
        exit(1);
    }
    /* Child process */
    if (pid == 0) {
        printf("Child's PID = %d\n", getpid());
        exit(0);
    }
    /* Parent process */
    printf("Parent's PID = %d\n", getpid());
    sleep(10);
    /* Parent process does not wait for the child */
    /* process and child becomes a zombie process */
    exit(0);
}
```

```
% gcc48 -w create_zombie.c -o create_zombie
% ./create_zombie
Parent's PID = 14978
Child's PID = 14979
<Ctrl+Z>
Suspended
% ps
  PID TT  STAT      TIME COMMAND
14522 1  Ss       0:00.42 -csh (csh)
14978 1  T        0:00.00 ./create_zombie
14979 1  Z        0:00.00 <defunct>
14986 1  R+       0:00.01 ps
% fg
zombie
%
```

A sample run under Solaris is shown in the following session. Note that you need to use the ps -al command to display the status of the zombie processes.

```
% ./create_zombie
Parent's PID = 12295
Child's PID = 12296
<Ctrl+Z>
Stopped (user)
```

```
% ps -al
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
0 Z 1007 12296 12295 0 0 - - 0 - ? 0:00 <defunct>
0 T 1007 12295 12294 0 40 20 ? 432 pts/1 0:00 ./create_zombie
0 O 1007 12297 12294 0 40 20 ? 2318 pts/1 0:00 ps
0 S 1007 12294 12166 0 40 20 ? 2179 ? pts/1 0:00 csh
% fg
zombie
%
```

When a child of the init process terminates, init calls one of the wait() system calls to collect the exit status of the child. Thus, none of the children of init ever becomes a zombie. The child may be a process that was directly created by init or was inherited by init because the parent of the process had died (or was not waiting) when the process terminated.

## EXERCISE 19.11

Replicate the preceding session on your system. Does the create_zombie.c program work as expected?

## 19.3.7 Terminating a Process

A process can use the kill() system call to terminate a process for which it has such permission. A process owned by the superuser may terminate any process. We discuss this system call in detail in Section 19.5.4.

## 19.4 PROCESSES AND THE FILE DESCRIPTOR TABLE

We now discuss the importance of PPFDT in relation to file sharing between processes, I/O redirection, and communication between processes using different channels including pipes, FIFOs, and sockets. We discuss the concept of file sharing in Section 19.4.1 and I/O redirection in Section 19.4.2. Chapter 20 describes UNIX interprocess communication in detail.

### 19.4.1 File Sharing between Processes

As discussed earlier, a child process gets a copy of the PPFDT of its parent. It means that if a process opens a file before creating a child process, the parent and child processes have access to the file descriptor of the open file. Consequently, the I/O performed on the open file by either process is visible to the other process.

The program file_sharing.c illustrates how parent and child processes share files that are open before the child process is created. We demonstrate the concept with only one file, but it extends to multiple files. The program takes filename and nbytes (the I/O size in bytes) as command line arguments and opens for reading and writing the file specified as the command line argument. It then creates a child process that inherits the PPFDT and,

therefore, the file descriptor of the opened file. Both the parent and child processes do I/O with the same file. The program displays the data read by both processes and the position of the file pointer after I/O in both processes, verifying that both processes do I/O with the same file. The nbytes argument may vary from 0 to 512 because the size of the read/write buffer has been set to 512 bytes. We use the sleep(1) call in the parent process to make sure that the child process performs I/O before the parent process. It is done to make sure that the values of the file pointer are displayed correctly in both processes. A few sample runs follow the listing of the program to verify that the file-sharing concept works as discussed. Note that foo is the name of an existing file.

```
% cat file_sharing.c
/* file_sharing.c: fileshare filename nbytes */
#include <fcntl.h>
#include <unistd.h>
#include <sys/wait.h>

#define SIZE 512

int main(int argc, char *argv[])
{
    int fd, n, nr, nbytes, pid, status;
    char buf[SIZE];

    /* Open file */
    if (argc != 3) {
        printf("$s filename nbytes\n", argv[1]);
        exit(1);
    }
    nbytes = atoi(argv[2]);
    if ((fd = open(argv[1], O_RDWR)) == -1) {
        perror("File opening");
        exit(1);
    }
    /* Create a child */
    pid = fork();
    /* Child process */
    if (pid == 0) {
        /* Read and display on stdout */
        if ((nr = read(fd, buf, nbytes)) == -1) {
            perror("Read failed");
            exit(1);
        }
        write(1, buf, nr); /* Throw on standard output */
        n = lseek(fd, 0L, SEEK_CUR);
        printf("\n\nChild: position of the file pointer after I/O is %d\n\n", n);
        close(fd);
```
