
#include <limits.h>
#ifndef PIPE_BUF
#define PIPE_BUF POSIX_PIPE_BUF
#endif

char chunk[PIPE_BUF];

An alternative that may work on your system is to use the fpathconf() system call to determine the value of the atomic write size dynamically. The fpathconf() system call returns the value of various system dependent configuration values associated with an open file descriptor. The fpathconf() function’s synopsis and description is

```
#include <unistd.h>

long fpathconf(int filedes, int name);
long pathconf(char *path, int name);
```

DESCRIPTION
fpathconf() gets a value for the configuration option name
for the open file descriptor filedes.

The second argument to fpathconf() is a mnemonic name defined in the man page. These are names such as _PC_NAME_MAX, _PC_PATH_MAX, and _PC_PIPE_BUF. Each name has a different usage, and its validity depends upon whether the given file descriptor is that of a file, a directory, a pipe, or a terminal. If filedes is a pipe, then the constant _PC_PIPE_BUF is supposed to tell fpathconf() to return the maximum number of bytes that may be written atomically to that pipe. It may not return this value. This will be explained below.

Although it is not necessary to know the value of PIPE_BUF, it is an interesting exercise to learn its value and make sure that it has the magical properties it is supposed to have. The following program is designed to demonstrate (but not prove) that writes of up to PIPE_BUF bytes are atomic, and that larger writes may not be atomic. It also demonstrates how to create multiple writers and a single reader. The program creates two writer processes and one reader. One writer writes 'X's into the pipe, the other 'y's. They each write the same number of characters each time. The command line argument specifies the number of writes that each makes to the pipe. The idea is that if the number is large enough the scheduler will time slice them often enough so that one will write for a while, then the next, and so on. The parent is the reader. It reads the data from the pipe and stores it in a file. The parent reads smaller chunks since it does not matter.

## Listing 8.3: pipedemo2.c

```
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>
#include <signal.h>
#include <sys/wait.h>
```

```
#define READ_FD 0
#define WRITE_FD 1
#define RD_CHUNK 10
#define ATOMIC

#ifndef PIPE_BUF
#define PIPE_BUF POSIX_PIPE_BUF
#endif

void do_nothing( int signo)
{
    return;
}

int main(int argc, char* argv[] )
{
    int i, repeat;
    int bytesread;
    int msgglen;
    pid_t child1, child2;
    int fd[2];
    int outfd;
    char message[RD_CHUNK+1];
    char *Child1_Chunk, *Child2_Chunk;
    long Chunk_Size;

    static struct sigaction sigact;

    sigact.sa_handler = do_nothing;
    sigfillset(&(sigact.sa_mask));
    sigaction(SIGUSR1, &sigact , NULL);

    /* check proper usage */
    if ( argc < 2 ) {
        fprintf(stderr, "Usage: %s size\n", argv[0]);
        exit(1);
    }

    /* try to create pipe */
    if ( -1 == pipe(fd)) {
        perror("pipe call");
        exit(2);
    }

    repeat = atoi(argv[1]);
#if defined ATOMIC
    Chunk_Size = PIPE_BUF;
#else
    Chunk_Size = PIPE_BUF + 200;
#endif
```

```
printf("Chunk size = %ld\n", Chunk_Size);
printf("Value of PIPE_BUF is %d\n", PIPE_BUF);

Child1_Chunk = calloc(Chunk_Size, sizeof(char));
Child2_Chunk = calloc(Chunk_Size, sizeof(char));
if ( ( NULL == Child1_Chunk ) ||
     ( NULL == Child2_Chunk ) ) {
    perror("calloc");
    exit(2);
}

/* create the string that child1 writes */
Child1_Chunk[0] = '\0'; /* just to be safe */
for ( i = 0; i < Chunk_Size-2; i++ )
    strcat(Child1_Chunk, "X");
strcat(Child1_Chunk,"\n");

/* create the string that child2 writes */
Child2_Chunk[0] = '\0'; /* just to be safe */
for ( i = 0; i < Chunk_Size-2; i++ )
    strcat(Child2_Chunk, "Y");
strcat(Child2_Chunk,"\n");

/* create first child process */
switch ( child1 = fork() ) {
case -1: /* fork failed — exit */
    perror("fork()");
    exit(3);

case 0: /* child1 code */
    msgglen = strlen(Child1_Chunk);
    pause();
    for ( i = 0; i < repeat; i++ ) {
        if ( write(fd[WRITE_FD], Child1_Chunk, msgglen )
            != msgglen ) {
            perror("write");
            exit(4);
        }
    }
    close(fd[WRITE_FD]);
    exit(0);
default: /* parent creates second child process */
    switch ( child2 = fork() ) {
    case -1: /* fork failed — exit */
        perror("fork()");
        exit(5);

    case 0: /* child2 code */
        msgglen = strlen(Child2_Chunk);
        pause();
        for ( i = 0; i < repeat; i++ ) {
            if ( write(fd[WRITE_FD], Child2_Chunk, msgglen )
                != msgglen ) {
```
