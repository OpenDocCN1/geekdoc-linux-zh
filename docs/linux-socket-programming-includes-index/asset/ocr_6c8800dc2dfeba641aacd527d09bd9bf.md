msg_len
The number of bytes to send.

options
A set of flags to enable special message handling:
* `MSG_CCB` Send message out-of-band (urgent).
* `MSG_DONTROUTE` Send the message bypassing all routers. If unsuccessful, the network sends an error back.
* `MSG_DONTWAIT` Don't allow blocking. Similar to the `fcntl()` option call, but only applies to this call. If the call would block, the call returns with `EWOULDBLOCK` in `errno`.
* `MSG_NOSIGNAL` If the peer severs the connection, don't raise a `SIGPIPE` signal locally.

# Possible Errors

+   * `EBADF` An invalid descriptor was specified.
+   * `ENOTSOCK` The argument `sockfd` is not a socket.
+   * `EFAULT` An invalid user space address was specified for `buffer`.
+   * `EMSGSIZE` The call can't complete because the socket requires that the message be sent atomically, and the size of the message to be sent has made this impossible.
+   * `EAGAIN` The socket is marked non-blocking and the requested operation would block.
+   * `ENOBUFS` The system was unable to allocate an internal memory block. The operation may succeed when buffers become available.
+   * `EINTR` A signal occurred.
+   * `ENOMEM` No memory available.
+   * `EINVAL` Invalid argument passed.
+   * `EPIPE` The local end has been shut down on a connected socket. In this case, the process will also receive a `SIGPIPE` unless `MSG_NOSIGNAL` is set.

# Example

```
```c
/* ** Send a message (TCP, UDP) to a connected destination ** */
int sockfd;
int bytes, bytes_wrote=0;
/* -- Create socket, connect to server/peer -- */
while ( (bytes = send(sockfd, buffer, msg_len, 0)) > 0 )
if ( (bytes_wrote += bytes) >= msg_len )
    break;
if ( bytes < 0 )
    perror( "send" );
```
```