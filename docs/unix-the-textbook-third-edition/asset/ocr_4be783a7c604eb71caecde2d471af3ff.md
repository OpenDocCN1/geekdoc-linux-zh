# TABLE 20.23 Reasons for the select() Call to Fail

| Reason for Failure | Value of errno |
|---|---|
| One of the descriptor sets contains an invalid descriptor | EBADF |
| One (or more) of the following arguments points to an illegal address: readfds, writefds, exceptfds, or timeout | EFAULT |
| A signal occurred before the time limit expired and before any of the descriptors became ready | EINTR |
| timeout is invalid (i.e., one of the fields of this argument is too big or negative) | EINVAL |
| nfds is invalid | EINVAL |

# Server process

+   1. Create a socket for SOCK_STREAM style of communication.
+   2. Bind an address to the socket using the bind() system call.
+   3. Put the socket in passive mode using the listen() system call.
+   4. Add the socket descriptor to the set of those sockets on which I/O or exception is possible—to keep the discussion simple, we will not deal with sockets meant to monitor exception conditions.
+   5. Use the select() system call to monitor and select those descriptors that are ready for I/O.
+   6. See which of the sockets are ready by checking the descriptors in the descriptor sets. If the passive socket is ready, use the accept() system call to accept the connection request from a client and add the newly created socket to the set of those on which I/O is possible.
+   7. If a socket other than the passive socket is ready, receive the next request from an already connected client using the read() system call, form a response, and send it to the client using the write() system call.
+   8. If the client request is to close a connection, close the connection gracefully, set the corresponding descriptor value to 0 in the original descriptor set on which I/O was possible.
+   9. Set the 'readfds', 'writefds', and 'exceptfds' descriptor sets to the original set of descriptors on which I/O is possible (after accommodating any changes outlined in Step 8).
+   10. Go to Step 5.

# FIGURE 20.29 Algorithm for the single-process connection-oriented concurrent server process using the select() system call.

for the server, its compilation, execution, and testing using the TIME and ECHO client discussed in Section 20.8.2.

```
% more select_server.c
#include <time.h>
#include <netdb.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <sys/select.h>

#define UNIXEPOCH 2208988800
#define TIME "8001"
#define ECHO "8002"
#define BUFF 256
#define QLEN 5
```