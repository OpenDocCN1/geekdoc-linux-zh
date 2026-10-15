# 8.2.3 Pipe Capacity

The capacity of a pipe may be larger than PIPE_BUF. There is no exposed system constant that indicates the total capacity of a pipe; however, the following program, based on one from [Haviland et al], can be run on any system to test the maximum capacity of a pipe, and also to prove that a process cannot write to a pipe unless it has at least PIPE_BUF bytes available.

# Listing 8.4: pipesizetest.c

```
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>
#include <signal.h>
#include <limits.h>

int count = 0;
sig_atomic_t full = 0;

/**
 * The SIGALRM handler. This sets the full flag to indicate that the
 * write call blocked, and it prints the number of characters written
 * to the pipe so far.
 */
void on_alarm(int signo)
{
    printf("\nwrite() blocked with %d chars in the pipe.\n", count);
    full = 1;
}

int main(int argc, char* argv[])
{
    int fd[2];
    int pipe_size;
    int bytesread;
    int amount_to_remove;

    char buffer[PIPE_BUF];
    char c = 'x';
    static struct sigaction sigact;

    sigact.sa_handler = on_alarm;
    sigfillset(&(sigact.sa_mask));
    sigaction(SIGALRM, &sigact, NULL);

    if ( -1 === pipe(fd) ) {
        perror("pipe failed");
        exit(1);
    }

    /* Check whether the _PC_PIPE_BUF constant returns the pipe capacity
     * or the atomic write size
     */
    pipe_size = fpathconf(fd[0], _PC_PIPE_BUF);
```