
exit(1);
case 0:
    dup2(fd[0], fileno(stdin));    /* now stdin points to fd[0] */
    close(fd[0]);                  /* close input end of pipe */
    close(fd[1]);                  /* close output end of pipe */
    execlp(argv[2], argv[2], NULL); /* run the first command */
    perror("execlp");
    exit(2);
default:
    close(fd[0]);   /* parent must close its ends of the first pipe */
    close(fd[1]);
    for ( i = 1; i <= 2; i++ )
        if ( wait(NULL) == -1 ) {
            perror("wait failed");
            exit(3);
        }
    return 0;
}
}
return 0;
}

There are a couple of things you can try to do at this point to test your understanding of pipes.

+   1. There is a UNIX utility called tee that copies its input stream to standard output as well as to its file argument:
+   
+       $ ls -l | tee listing
+   
+       will copy the output of "ls -l" into the file named listing as well as to standard output. Try to write your own version of tee.
+   2. Extend shpipe2 to work with any number of commands so that
+   
+       $ shpipe3 cmmd cmmd ... cmmd
+   
+       will act like
+   
+       $ cmmd | cmmd | ... | cmmd

## 8.3.3 The popen() Library Function

The sequence

+   1. generate a pipe,
+   2. fork a child process,
+   3. duplicate file descriptors, and
+   4. execute a new program in order to redirect the input or output of that program to the parent,

is so common that the developers of the C library added a pair of functions, popen() and pclose() to streamline this procedure:

```
#include <stdio.h>
FILE *popen(const char *command, const char *type);
int pclose(FILE *stream);
```

The popen() function creates a pipe, forks a new process to execute the shell /bin/sh (which is system dependent), and passes the command to that shell to be executed by it (using the -c flag to the shell, which tells it to expect the command as an argument.)

popen() expects the second argument to be either "r" or "w". If it is "r" then the process invoking it will be returned a FILE pointer to the read-end of the pipe and the write-end will be attached to the standard output of the command. If it is "w", then the process invoking it will be returned a FILE pointer to the write-end of the pipe, and the read-end will be attached to the standard input of the command. The output stream is fully buffered.

File streams created with popen() must be closed with pclose(), which will wait for the invoked process to terminate and returns its exit status or -1 if wait4() failed.

An example will illustrate. We will write a third version of the shpipe program, called shpipe3, using popen() and pclose() instead of the pipe(), fork(), dup() sequence. See Listing 8.8 below.

### Listing 8.8: shpipe3.c

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <limits.h>

int main(int argc, char* argv[])
{
    int     nbytes;
    FILE    *fin;           /* read-end of pipe */
    FILE    *fout;          /* write-end of pipe */
    char    buffer[PIPE_BUF];   /* buffer for transferring data */

    if ( argc < 3 ) {
        fprintf(stderr, "Usage: %s  command1 command2\n", argv[0]);
        exit(1);
    }

    if ( (fin = popen(argv[1], "r")) == NULL ) {
        fprintf(stderr, "popen() failed\n");
        exit(1);
    }

    if ( (fout = popen(argv[2], "w")) == NULL ) {
        fprintf(stderr, "popen() failed\n");
        exit(1);
    }

    while ( (nbytes = read(fileno(fin), buffer, PIPE_BUF)) > 0 )
```

```
write(fileno(fout), buffer, nbytes);

pclose(fin);
pclose(fout);
return 0;
}
```

## 8.4 Named Pipes

Unnamed pipes are an elegant mechanism, however, they have several drawbacks. They can only be shared by processes with a common ancestor, such as a parent and child, or multiple children or descendants of a parent that created the pipe. Also, they cease to exist as soon as the processes that are using them terminate, so they must be recreated every time they are needed. If you are trying to write a server program with which clients can communicate, the clients will need to know the name of the pipe through which to communicate, but an unnamed pipe has no such name.

*Named pipes* make up for these shortcomings. A named pipe, or *FIFO*, is very much like an unnamed pipe in how you use it. You read from it and write to it in the same way. It behaves the same way with respect to the consequences of opening and closing it when various processes are either reading or writing or doing neither. In other words, the semantics of opening, closing, reading, and writing named and unnamed pipes are the same.

What distinguishes named pipes from unnamed pipes is that

- They exist as directory entries in the file system and therefore have associated permissions and ownership²
- They can be used by processes that are not related to each other.
- They can be created and deleted at the shell level or at the programming level.

### 8.4.1 Named Pipes at the Command Level

Before we look at how they are created within a program, let us look at how they are created at the user level. There are two commands to create a FIFO. The older command is mknod. mknod is a general purpose utility for creating device special files. There is also a mkfifo command, which can only be used for creating a FIFO file. We will look at how to use mknod. You can read about the mkfifo command in the man pages.

```
$ mknod PIPE p
```

creates a FIFO named "PIPE". The lowercase p, which must follow the file name, indicates to mknod that PIPE should be a FIFO (p for pipe.) After typing this command, look at the working directory:

²Although they have directory entries, they do not exist in the file system. They have no disk blocks and their data is not on disk when they are in use.
