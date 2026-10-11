The procedure that function `report()` implements is as follows:

+   1. The function accepts as input the port number being requested (line 20). The `web80.c` program calls this function with the argument `80`.
+   2. A `PF_LOCAL (PF_UNIX)` socket is created in lines 28 to 30. This socket must be a `PF_LOCAL` socket in order that credentials be available to the receiving server.
+   3. An abstract server address is formed in lines 36 to 41. This will be used to contact the socket server.
+   4. A call to `connect(2)` is made to contact the socket server (lines 46 to 48).
+   5. A `write(2)` call is used to send the port number that is being requested.
+   6. The function `recv_fd()` is called to obtain the server response (line 63). The return value will be `>= 0` if a socket was received, or `-1` if an error was received instead.
+   7. The socket or the value `-1` is returned in line 66.

Now you must investigate the workings of `recv_fd()` to see how the file descriptor was received.

# The `recv_fd()` Function

Listing 17.7 shows the code for the function `recv_fd()`.

```
Listing 17.7: `recvfd.c`—The `recv_fd()` Function

```
1: /* recvfd.c
2:  *
3:  * Receive a file descriptor:
4:  */
5: #include "common.h"
6: 
7: /*
8:  * Receive a file descriptor from the
9:  * socket.
10:  *
11:  * ARGUMENTS:
12:  * s Socket to receive file
13:  * descriptor on.
14:  *
15:  * RETURNS:
16:  * >= 0  Received file descriptor
```
```