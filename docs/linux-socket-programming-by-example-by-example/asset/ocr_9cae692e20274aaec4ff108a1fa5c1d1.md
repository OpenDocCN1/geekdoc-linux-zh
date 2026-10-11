# Applying the setsockopt(2) Function

Listing 12.2 shows a short program that changes the send and receive buffer sizes for a socket. After setting these options, the program obtains the actual sizes of these buffers and reports them.

```
Listing 12.2: setsndrcv.c—Setting SOCKET Options SO_SNDBUF and SO_RCVBUF

```c
/* setsndrcv.c:
 *
 * Set SO_SNDBUF & SO_RCVBUF Options:
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <assert.h>

/*
 * This function reports the error and
 * exits back to the shell:
 */
static void
bail(const char *on_what) {
    if ( errno != 0 ) {
        fputs(strerror(errno),stderr);
        fputs(": ",stderr);
    }
    fputs(on_what,stderr);
    fputc('\n',stderr);
    exit(1);
}

int
main(int argc,char **argv) {
    int z;
    int s = -1;                     /* Socket */
    int sndbuf=0;      /* Send buffer size */
    int rcvbuf=0;/* Receive buffer size */
    socklen_t option;  /* Option length */

/*
 * Create a TCP/IP socket to use:
 */
```
continues
```