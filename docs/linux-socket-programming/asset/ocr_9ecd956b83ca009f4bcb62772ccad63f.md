Likewise in the write() call, you can substitute the file descriptor (fd) with the socket descriptor (sd). As an example, here is a snippet showing a typical socket output with write() :

```
```
int sd, bytes_written = 0, retval;

sd = socket(AF_INET, SOCK_STREAM, 0);
... /*** Connect to host ***/

while ( bytes_written < len )      /* repeat sending until all */
{                                  /*...bytes of message are sent */
    ret_val = write(sd, buffer+bytes_written, len);

    if ( ret_val >= 0 )
        bytes_written += ret_val;
    else
        /*--report connection error--*/
}
```
```

On the other hand, here is a snippet showing a typical socket output with fprintf() by converting the socket descriptor into a FILE* :

```
```
FILE *sp;
int sd;

sd = socket(AF_INET, SOCK_STREAM, 0);
... /*** Connect to host ***/

sp = fdopen(sd, "w");             /* create FILE* from socket */
if ( sp == NULL )
    perror("FILE* conversion failed");

fprintf(sp, "%s, %s, %s\ n",Name, Address, Phone);
```
```

Note that in the first example, the program has to loop on the write() to get all the bytes out. Even though this is a socket stream, you cannot guarantee that the program sends all the bytes at once. The second instance does not have that limitation, because FILE* has its own data-buffering subsystem. When you write to a FILE* buffer, the subsystem forces you to wait until it sends all the bytes.

There is, of course, a dedicated socket write call: send(). Like the recv() call, send() gives the programmer more control over the execution of the transmission. The prototype declaration is

```
```
#include <sys/socket.h>
#include <resolv.h>
int send(int sd, const void *msg, int len, unsigned int flags);
```
```

All the parameters are the same as write() except for the last—flags. The send() system call has several options that help revise the call’s behavior:

+   * **MSG_OOB** Send "Out Of Band" data. As used above, it allows you to send one byte to the peer, client, or server indicating an urgent condition. The receiver has only one byte dedicated for OOB data; subsequent OOB messages overwrite the last message. When an OOB message arrives, the operating system issues a SIGURG (urgent signal) to the responsible program.