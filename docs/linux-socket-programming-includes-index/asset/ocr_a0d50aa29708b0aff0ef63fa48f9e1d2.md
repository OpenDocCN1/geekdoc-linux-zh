With the shutdown() system call, you can close different directions of data flow in the communication path, making the path read-only or write-only:

```
#include <sys/socket.h>
int shutdown(int s, int how);
```

The how parameter can have three values:

| Value | Function |
| :--- | :--- |
| 0 (zero) | Write only (think of "O" in "output") |
| 1 (one) | Read only (think of "I" in "input") |
| 2 | Close both input and output |

# # Summary: What's Going On Behind the Scenes?

Several things occur behind the scenes when the program opens a socket and connects to a TCP server. All the socket call does is create a message queue. Things really happen when the program connects. (You can get the complete program listing on the companion CD.) Table 1.2 shows what happens on the client and server sides.

# **TABLE 1.2** Steps of Creating a Socket and Connecting

| Client's Actions | Server's Actions |
| :--- | :--- |
| 1. Calls socket(): Creates a queue; sets flags for communciation protocols. | (Waiting for connection) |
| 2. Calls connect(): The operating system assigns a temporary port number if the socket doesn't have an assigned port number through bind(). | (Waiting) |
| 3. Sends a message to the server requesting a connection, telling the server which port the client is using. | 4. Places the connection request on the listening queue. |
| (Waiting for server) | 5. Reads the connection queue, accepts a connection, and creates a unique socket channel. |
| (Waiting) | |