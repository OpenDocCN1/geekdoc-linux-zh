
![](img/edd55012c780b4e999320d08ab27959e_414_0.png)

Figure 8.1: A pipe connecting last to grep.

will block, and if grep tries to read from an empty pipe because it is reading faster than last can write, grep will block, and both of these actions are handled behind the scenes by the kernel.

What then is a pipe? Although a pipe may seem like a file, it is not a file, and there is no file pointer associated with it. It is conceptually like a conveyor belt consisting of a fixed number of logical blocks that can be filled and emptied. Each write to the pipe fills as many blocks as are needed to satisfy it, provided that it does not exceed the maximum pipe size, and if the pipe size limit was not reached, a new block is made available for the next write. Filled blocks are conveyed to the read-end of the pipe, where they are emptied when they are read. These types of pipes are called unnamed pipes because they do not exist anywhere in the file system. They have no names.

An unnamed pipe¹ in UNIX is created with the pipe() system call.

```c
#include <unistd.h>
int pipe(int filedes[2]);
```

The system call pipe(fd), given an integer array fd of size 2, creates a pair of file descriptors, fd[0] and fd[1], pointing to the "read-end" and "write-end" of a pipe inode respectively. If it is successful, it returns a 0, otherwise it returns -1. The process can then write to the write-end, fd[1], using the write() system call, and can read from the read-end, fd[0], using the read() system call. The read and write-ends are opened automatically as a result of the pipe() call. Written data are read in first-in-first-out (FIFO) order. The following program (pipedemo0.c in the demos directory) demonstrates this simple case.

Listing 8.1: pipedemo0.c

```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>

#define READ_END 0
#define WRITE_END 1
#define NUM 5
#define BUFSIZE 32

int main(int argc, char* argv[])
{
    int i, nbytes;
    int fd[2];
    char message[BUFSIZE + 1];

    if ( -1 == pipe(fd)) {
        perror("pipe call");
        exit(2);
    }

    for ( i = 1; i <= NUM; i++ ) {
        sprintf(message, "hello #%d\n", i);
        write(fd[WRITE_END], message, strlen(message));
    }
    close(fd[WRITE_END]);

    printf("%d messages sent; sleeping a bit. Please wait...\n", NUM);
    sleep(3);

    while ( ( nbytes = read( fd[READ_END], message, BUFSIZE)) != 0 )
    {
        if ( nbytes > 0 ) {
            message[nbytes] = '\0';
            printf("%s", message);
        }
        else
            exit(1);
    }
    fflush(stdout);
    exit(0);
}
```

## Notes

- In this program, the write calls are not error-checked, which they should be. The read() in the while loop condition is error-checked: if it returns something strictly less than zero, exit(1) is executed.
- The read() call is a blocking read by default; you have to explicitly make it non-blocking if you want it to be so. By design, a blocking read on a pipe will block waiting for data as long as the write-end of the pipe is held open. If the program does not close the write-end of the pipe before the read-loop starts, it will hang forever, because read() will continue to wait for data. This could be avoided if the read-loop knew in advance exactly how many bytes to expect, because in that case it could just read exactly that many bytes and then exit the loop, but it is rarely the case that one knows how much data to expect. Naturally, the process has to write the data into the pipe before the read loop begins, otherwise there will be nothing to read!
- Notice that the read() calls always read the same amount of data. This example demonstrates that the reader can read fixed-size chunks and assemble them into larger chunks, because the data arrives in the order it was sent (unlike data sent across a network). Pipes have no concept of message boundaries – they are simply byte streams.
- Finally, observe that before calling printf() to print the string on the standard output, the string has to be null-terminated.
