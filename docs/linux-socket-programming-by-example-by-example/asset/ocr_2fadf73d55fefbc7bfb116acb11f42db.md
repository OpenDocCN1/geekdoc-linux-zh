```
100:     * Report the Date & Time:
101:  */
102:       dtbuf[z] = 0;  /* null terminate string */
103:
104:       printf("Date & Time is: %s\n", dtbuf);
105:
106:       /*
107:        * Close the socket and exit:
108:        */
109:       close(s);
110:       putchar('\n');
111:
112:       return 0;
113:  }
```

The program can be described in more detail, as follows:

+   1. The program will use an IP number on the command line if provided (line 48), but otherwise defaults to your local host (also known as localhost) by using the local loopback address 127.0.0.1 (line 51). The IP number on the command line allows the user to test the daytime service on another remote host. This is particularly useful if it is turned off on the local host and the service is available somewhere else.

+   2. Line 57 looks up the daytime Internet service for use over TCP/IP. If this service is not found, the problem is reported in lines 59 to 61.

+   3. The server's address and the length of the address are established in lines 67 to 76. Note especially line 69 where the service port number is established for the daytime service.

+   4. The socket is created in line 81. Note especially the argument SOCK\_STREAM that specifies that we want a TCP/IP socket (when used with PF\_INET).

+   5. The program connects to the server in line 88. If this fails, the error is handled in line 90.

+   6. Line 95 shows a read(2) call that retrieves the output from the server. The return value indicates the number of bytes read. Otherwise, the error is dealt with in line 97.

+   7. Line 102 makes certain that we have a terminating null byte, so that the buffer dtbuf[] can be treated like a C string.

+   8. Line 104 reports the value returned by the server.

+   9. The socket is closed in line 109.