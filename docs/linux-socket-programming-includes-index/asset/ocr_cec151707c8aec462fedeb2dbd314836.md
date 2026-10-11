Referring back to the `read()` system call, you may get the following common errors:

+   * `EAGAIN` Nonblocking I/O is selected, and no data is available. This error instructs the program to try the call again.
+   * `EBADF` *fd* is not a valid file descriptor or is not open for reading. This can occur if the socket call was unsuccessful or the program closed the input pipe (making it write-only).
+   * `EINVAL` *fd* is attached to an object that is unsuitable for reading.

The `read()` system call provides no special control over the way it uses the socket. Linux offers another standard system call, `recv()`. You can use `recv()` directly with the socket descriptor for getting information while providing you with more control:

```
```c
#include <sys/socket.h>
#include <resolv.h>
int recv(int sd, void *buf, int len, unsigned int flags);
```
```

The `recv()` call is no different from the `read()` call except for the flags. The flags give you more control over what you get or even flow control. These values can be arithmetically ORed together (`FLAG1 | FLAG2 | ...`). Under normal circumstances, the parameter is set to zero. You may wonder why you can’t use the `read()` call if it’s no different than `read()` when the flags are zero. Just as a suggestion, use `recv()` instead of `read()`—it may help you later when the program becomes more complex. Also, generally speaking, it’s better to use one tool set rather than mixing tools. Finally, `read()` checks what kind of I/O descriptor you sent and executes the appropriate system call.

Here are a few useful flags you can use to control the `recv()` system call. You can find a more complete listing in Appendix B, “Networking API.”

+   * `MSG_OOB` Process out-of-band data. Used for high priority messages. Some protocols allow you to choose between a normal and a high priority when you send a message. Set this flag to have the queue manager look for and return out-of-band messages instead of normal data. See Chapter 10 for more information.
+   * `MSG_PEEK` Read nondestructively. Used to tell the queue manager to read the message queue without moving the read-index pointer. (In other words, a subsequent read yields at least the same data each time. See the box on the next page.)
+   * `MSG_WAITALL` Used so that your message doesn’t return until the supplied buffer is filled. Sometimes you get only a partially filled buffer, because the remaining data is in transit. If you know how much information the server is sending and you don’t want to reassemble it yourself, use this flag to fill the buffer (or wait forever).