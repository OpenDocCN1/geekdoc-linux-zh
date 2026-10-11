program is brought into memory to replace it. For this reason, the wrapper and the server programs keep the same process ID (this is important to inetd, the parent process).

If all goes well, the server begins to execute. If for some reason the server does not execute, then the execve(2) function will return control. The following error recovery steps are then carried out:

+   1. The log file is reopened (line 103) because it was closed prior to calling execve(2) in line 95.
+   2. The error is reported to the log file (line 104).

# **Introducing the Client Program**

A modified version of an earlier client program is presented here. This client program requires two command-line arguments: the server address and the client address to use. The specification of the additional client IP address permits you to perform more experimentation with your TCP wrapper program. Listing 16.5 shows the modified datagram client program.

**Listing 16.5:** dgramcln2.c - The Modified Datagram Client Program

![](bbox=[0.1, 0.54, 0.19, 0.63])

```
```
1: /* dgramcln2.c:
2:  *
3:  * Modified datagram client:
4:  */

5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <errno.h>
9: #include <string.h>
10: #include <time.h>
11: #include <sys/types.h>
12: #include <sys/socket.h>
13: #include <netinet/in.h>
14: #include <arpa/inet.h>

16: /*
17:  * This function reports the error and
18:  * exits back to the shell:
19:  */
20: static void
21: bail(const char *on_what) {

23:     if ( errno ) {
24:         fputs(strerror(errno),stderr);
25:         fputs(": ", stderr);
```