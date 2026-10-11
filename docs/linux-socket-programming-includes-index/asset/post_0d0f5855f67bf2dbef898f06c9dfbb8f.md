
In fact, you could convert the socket descriptor into a `FILE*` for higher-level I/O. For example, to use `fscanf()`, you could follow the example below. (The lines in **bold** indicate the changes from the previous listing.)

```c
char Name[NAME], Address[ADDRESS], Phone[PHONE];
FILE *sp;
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0); /* create socket */

/* Connect to host */

if ( (sp = fdopen(sd, "r")) == NULL) /* convert to FILE* */
  perror("FILE* conversion failed");
else if ( fscanf(sp, "%s, %s, %s\n",
  Name, Address, Phone) < 0 )
{
    perror("fscanf");
...
```

Only stream-style sockets can be converted reliably into a `FILE*` stream. The reason is simple: Datagram sockets are typically connectionless—a message is sent and that's it. Also, streaming sockets provide data integrity and message reliability, whereas datagrams are unreliable. Datagrams are similar to putting a message in an addressed and stamped envelope that you send through the postal system: The message may not arrive at all. A `FILE*` connection must be an open channel. If you try to convert a datagram, you may lose critical data. For more information about streams versus datagrams, see Chapter 3, “Different Types of Internet Packs,”

`FILE*` socket connections provide excellent scanning and parsing resources for the network programmer. However, when you use them, you must check *all* return values, including `printf()` and `fscanf()`. Note the preceding example: If the return value of `fscanf()` is less than zero, there was an error.

## Network Security and Reliability

Security and reliability are of the utmost importance when you create network programs. At the time of writing this book, Microsoft operating systems have faced several fundamental security problems, several involving network connections. When you write your programs, make sure that buffers cannot be overflowed and all return values are checked. In a software bazaar setting, you can solicit input from others on your source code. The peer review of the software bazaar is a vast resource of knowledge and experience—use it.

Referring back to the `read()` system call, you may get the following common errors:

- `EAGAIN` Nonblocking I/O is selected, and no data is available. This error instructs the program to try the call again.
- `EBADF` *fd* is not a valid file descriptor or is not open for reading. This can occur if the socket call was unsuccessful or the program closed the input pipe (making it write-only).
- `EINVAL` *fd* is attached to an object that is unsuitable for reading.

The `read()` system call provides no special control over the way it uses the socket. Linux offers another standard system call, `recv()`. You can use `recv()` directly with the socket descriptor for getting information while providing you with more control:

```c
#include <sys/socket.h>
#include <resolv.h>
int recv(int sd, void *buf, int len, unsigned int flags);
```

The `recv()` call is no different from the `read()` call except for the flags. The flags give you more control over what you get or even flow control. These values can be arithmetically ORed together (`FLAG1 | FLAG2 | ...`). Under normal circumstances, the parameter is set to zero. You may wonder why you can’t use the `read()` call if it’s no different than `read()` when the flags are zero. Just as a suggestion, use `recv()` instead of `read()`—it may help you later when the program becomes more complex. Also, generally speaking, it’s better to use one tool set rather than mixing tools. Finally, `read()` checks what kind of I/O descriptor you sent and executes the appropriate system call.

Here are a few useful flags you can use to control the `recv()` system call. You can find a more complete listing in Appendix B, “Networking API.”

- `MSG_OOB` Process out-of-band data. Used for high priority messages. Some protocols allow you to choose between a normal and a high priority when you send a message. Set this flag to have the queue manager look for and return out-of-band messages instead of normal data. See Chapter 10 for more information.
- `MSG_PEEK` Read nondestructively. Used to tell the queue manager to read the message queue without moving the read-index pointer. (In other words, a subsequent read yields at least the same data each time. See the box on the next page.)
- `MSG_WAITALL` Used so that your message doesn’t return until the supplied buffer is filled. Sometimes you get only a partially filled buffer, because the remaining data is in transit. If you know how much information the server is sending and you don’t want to reassemble it yourself, use this flag to fill the buffer (or wait forever).

- `MSG_DONTWAIT` Used so that your message doesn't block if the queue is empty. Similar to setting the nonblocking feature on the socket, only requiring this option on this `recv()` system call exclusively. Normally, if no message data is available, the process waits (blocks) until some data arrives. If you use this flag and the queue has no data available at the time of the call, the system call returns immediately with an `EWOULDBLOCK` error code. (Linux does not currently support this option in the `recv()` call. You can use `O_NONBLOCK` with the `fcntl()` system call. This makes the socket always nonblocking.)

## Getting Fragmented Packets

Your programs are going to execute much faster than the network does. Sometimes a packet arrives at the computer in pieces, because the network routers fragmented it to fit more limited networks. If you call `recv()` when this occurs, you may get an incomplete message. This is one reason why `MSG_PEEK` could give you different results with consecutive calls: The first call may yield 500 bytes, and the second could be 750 bytes. Likewise, this is why there's a `MSG_WAITALL` flag.

The `recv()` system call is more flexible than `read()`, letting you use the different flags to modify behavior. Do a normal read from socket pipe (equivalent to `read()`):

```c
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, 0);
...
```

Read *nondestructively* from socket pipe:

```c
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, MSG_PEEK);
...
```

Read nondestructively out of band data from socket:

```c
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, MSG_OOB | MSG_PEEK);
...
```

The first statement gets the information from the server supplying a buffer, length, and no flags. The next statement displays the information. There is an intentional flaw here: What if the server sends more information than the buffer can accept? This is not a critical defect; nothing is going to crash. The algorithm simply may lose the data it doesn't read.

The `recv()` system call yields similar error codes to `read()` along with the following extensions:

- **ENOTCONN** sd not connected. The supplied socket descriptor is not connected to the peer or server.
- **ENOTSOCK** sd not a socket. The supplied socket descriptor does not have the signatures indicating that it came from a `socket()` system call.

Note that if you use the `read()` system call, you can still get these error codes when using a socket descriptor, because the `read()` call is just a portal to the `recv()` call.

## Closing the Connection

You have the information you need from the server, everything went well, and now you want to close the connection. There are again two ways you can close the connection. Most programs use the standard I/O `close()` system call:

```c
#include <unistd.h>
int close(int fd);
```

Again, the socket descriptor (sd) may substitute for the file descriptor (fd). It works the same. If successful, the return value is zero.

> **Always Close Socket Descriptors**
> Make it a point always to close descriptors manually, particularly sockets. By default, the operating system closes all descriptors and flushes buffers for you. If the descriptor refers to a file, the process works without affecting other systems. Sockets, on the other hand, can linger longer than necessary, tying up resources and making it difficult for other clients to connect.

This call yields only one error:

- **EBADF** fd isn't a valid open file descriptor.

The `shutdown()` system call gives you more control over closing the channels, because you can close either the incoming or outgoing channels. This call is especially helpful when using sockets to replace `stdin` or `stdout`.

> **Confusing Shutdown Commands**
> The `shutdown()` system call is different from the shutdown command (section 8 of online UNIX manuals) for bringing down the operating system.
