+   3. The function `listen(2)` is called to allow connections to this socket (lines 97 to 99).

+   4. The `for` loop allows for a continuous number of client connections to take place to this Web server (line 108).

+   5. Lines 112 to 154 form the body of the `for` loop, which simply waits for one text line of input and then sends some formatted HTML back to the client in return. The client's socket is closed at lines 152 and 153.

Note in lines 144 to 147 that the process ID of the Web server is reported back to the browser so that you can have confirmation of where this information came from.

# The report() Function

In the `web80.c` program of Listing 17.5, you saw that there was a call to the function `report()`. This function is responsible for contacting the socket server and obtaining a socket on port 80. Listing 17.6 shows the listing of this function.

![](bbox=[0.05, 0.48, 0.18, 0.58])

```
Listing 17.6: report.c—The report() Function

1: /* report.c
2: *
3: * Request a port from the sockserv:
4: */
5: #include "common.h"
6:
7: /*
8: * Request a INADDR_ANY socket on the
9: * port number requested:
10: *
11: * ARGUMENTS:
12: * s Socket to send request on
13: * port Port (host order) being requested
14: *
15: * RETURNS:
16: * >= 0 Socket to use
17: * -1 Failed: check errno
18: */
19: int
20: report(int port) {
21: int z;
22: int s; /* socket */
23: struct sockaddr_un a_svr; /* serv. adr */
24:
25: /*
```