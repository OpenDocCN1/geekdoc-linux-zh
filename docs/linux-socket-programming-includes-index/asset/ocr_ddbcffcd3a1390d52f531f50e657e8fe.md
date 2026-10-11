second line. If you want to connect to a different server, place the appropriate IP address in this string. The program proceeds with other initializations, including the `socket()` system call. When you start working with the structure, zero it out with `bzero()`. The program sets the family to `AF_INET`. Next, the program sets the port and the IP address. The `htons()` and `inet_aton()` conversion tools used here are covered in Chapter 2.

The next call is the connection to the server. Please note that the code fragment checks the return values for every procedure call. That policy is one of many keys to making your net-work programs robust.

After the program establishes the connection, the socket descriptor, sd, becomes a read/write channel between the two programs. Most servers we are accustomed to offer single transac-tions and then hang up (for example, an HTTP 1.0 server sends the requested file, then closes the connection). To interface with these types of server, your program has to send the request, get the reply, and close the connection.

# ## Getting the Server's Reply

The socket is open and the channel is established. Now, you can get the first "hello." Some servers initiate the conversation like the person answering the phone. This message may include the server's name and some instructions for connection. Once your connection is open, you can use the standard library low-level I/O calls for communication. Here is the `read()` system call:

```
```
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t count);
```
```

You're probably familiar with this call. Other than its special capability to use the socket descriptor (sd) instead of the file descriptor (fd), everything else is almost the same as reading from a file. You can even use the `read()` system call as in the following code fragment:

```
```
...
int sd, bytes_read;
sd = socket(PF_INET, SOCK_STREAM, 0);    /* create socket */

/**** Connect to host ****/

bytes_read = read(sd, buffer, MAXBUF);  /* read the message */
if ( bytes_read < 0 )
    /* report connection error; exit routine */
...
```
```