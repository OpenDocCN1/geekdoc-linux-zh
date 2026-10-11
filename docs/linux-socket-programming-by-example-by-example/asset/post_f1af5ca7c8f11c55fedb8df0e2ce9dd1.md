
```c
77: 	* Turn on SO_REUSEADDR:
78: 	*/
79: 	z = setsockopt(s, SOL_SOCKET, SO_REUSEADDR,&b,sizeof b);
81: 	if ( z == -1 )
82: 		bail("setsockopt(2)");
83:
84: 	} else {
85: 		* Run in socksrv mode: Request
86: 		* a socket bound to port 80:
87: 		*/
88: 	s = reqport(80);
89: 	if ( s == -1 )
90: 		bail("reqport(80)");
91: 	}
92:
93: 	/*
94: 	 * Now make this a listening socket:
95: 	 */
96: 	z = listen(s,10);
97: 	if ( z == -1 )
98: 		bail("listen(2)");
99:
100: 	/*
101: 	 * Perform a simple, Web server loop for
102: 	 * demonstration purposes. Here we just
103: 	 * accept one line of input text, and
104: 	 * ignore it. We provide one simple
105: 	 * HTML page back in response:
106: 	 */
107: 	for (;;) {
108: 		/*
109: 		 * Wait for a connect from browser:
110: 		 */
111: 		alen = sizeof a_cln;
112: 		c = accept(s,
113: 				(struct sockaddr *)&a_cln,
114: 				&alen);
115: 		if ( c == -1 ) {
116: 			perror("accept(2)");
117: 			continue;
118: 		}
119:
120: 		/*
121: 		 * Create streams for convenience, and
122: 		 */
123: 		/*
124: 		 * just eat any Web command provided:
125: 		 */
126: 		rx = fdopen(c,"r");
127: 		tx = fdopen(dup(c), "w");
128: 		fgets(getbuf,sizeof getbuf,rx);
129: 		/*
130: 		 * Now serve a simple HTML response.
131: 		 * This includes this Web server’s
132: 		 * process ID and the current date
133: 		 * and time:
134: 		 */
135: 		fputs("<HTML>\n" "<HEAD>\n" "<TITLE>Test Page for this little "
136: 		      "web80 server</TITLE>\n" "</HEAD>\n"
137: 		      "<BODY>\n" "<H1>web80 Worked!</H1>\n",tx);
138:
139: 		/*
140: 		 * Report our process ID and the date
141: 		 * and time:
142: 		 */
143: 		time(&td);
144: 		fprintf(tx, "<H2>From PID %ld @ %s</H2>\n",
145: 			(long)getpid(), ctime(&td));
146:
147: 		/*
148: 		 * Now terminate the HTML response:
149: 		 */
150: 		fputs("</BODY>\n" "</HTML>\n", tx);
151:
152: 		fclose(tx);
153: 		fclose(rx);
154: 	}
155: 	return 0;
156: }
```

The very simple Web server in Listing 17.5 uses the following basic procedure:

- 1. If command-line arguments are provided, a socket is created and bound with `bind(2)` if it can (lines 49 to 83). This allows you to prove that you need root access to obtain such a port under Linux.
- 2. If no command-line arguments are provided, the code between lines 89 and 91 is executed instead. Line 89 calls upon a function `report()` to obtain a socket on port 80.
- 3. The function `listen(2)` is called to allow connections to this socket (lines 97 to 99).
- 4. The `for` loop allows for a continuous number of client connections to take place to this Web server (line 108).
- 5. Lines 112 to 154 form the body of the `for` loop, which simply waits for one text line of input and then sends some formatted HTML back to the client in return. The client's socket is closed at lines 152 and 153.

Note in lines 144 to 147 that the process ID of the Web server is reported back to the browser so that you can have confirmation of where this information came from.

## The report() Function

In the `web80.c` program of Listing 17.5, you saw that there was a call to the function `report()`. This function is responsible for contacting the socket server and obtaining a socket on port 80. Listing 17.6 shows the listing of this function.

![](img/961a0296fe36074690a9847b79332eff_468_0.png)

```c
/* report.c
 *
 * Request a port from the sockserv:
 */
#include "common.h"

/*
 * Request a INADDR_ANY socket on the
 * port number requested:
 *
 * ARGUMENTS:
 * s Socket to send request on
 * port Port (host order) being requested
 *
 * RETURNS:
 * >= 0 Socket to use
 * -1 Failed: check errno
 */
int
report(int port) {
	int z;
	int s; /* socket */
	struct sockaddr_un a_svr; /* serv. adr */

	/*
	 * Create a Unix Socket:
	 */
	s = socket(PF_LOCAL, SOCK_STREAM, 0);
	if ( s == -1 )
		return -1; 	/* Failed: check errno */

	/*
	 * Create the abstract address of
	 * the socket server:
	 */
	memset(&a_srvr, 0, sizeof a_srvr);
	a_srvr.sun_family = AF_LOCAL;
	strncpy(a_srvr.sun_path,
		"$SOCKET-SERVER",
		sizeof a_srvr.sun_path-1);
	a_srvr.sun_path[0] = 0;

	/*
	 * Connect to the sock server:
	 */
	z = connect(s,&a_srvr,sizeof a_srvr);
	if ( z == -1 )
		return -1; 	/* Failed: check errno */

	/*
	 * Now issue our request:
	 */
	do {
		z = write(s,&port,sizeof port);
	} while ( z == -1 && errno == EINTR );

	if ( z == -1 )
		return -1; 		/* Failed: see errno */

	/*
	 * Now wait for a reply:
	 */
	z = recv_fd(s);
	close(s);

	return z; 			/* z = fd or -1 */
}
```

The procedure that function `report()` implements is as follows:

- 1. The function accepts as input the port number being requested (line 20). The `web80.c` program calls this function with the argument `80`.
- 2. A `PF_LOCAL (PF_UNIX)` socket is created in lines 28 to 30. This socket must be a `PF_LOCAL` socket in order that credentials be available to the receiving server.
- 3. An abstract server address is formed in lines 36 to 41. This will be used to contact the socket server.
- 4. A call to `connect(2)` is made to contact the socket server (lines 46 to 48).
- 5. A `write(2)` call is used to send the port number that is being requested.
- 6. The function `recv_fd()` is called to obtain the server response (line 63). The return value will be `>= 0` if a socket was received, or `-1` if an error was received instead.
- 7. The socket or the value `-1` is returned in line 66.

Now you must investigate the workings of `recv_fd()` to see how the file descriptor was received.

## The `recv_fd()` Function

Listing 17.7 shows the code for the function `recv_fd()`.

```c
/* recvfd.c
 *
 * Receive a file descriptor:
 */
#include "common.h"

/*
 * Receive a file descriptor from the
 * socket.
 *
 * ARGUMENTS:
 * s Socket to receive file
 * descriptor on.
 *
 * RETURNS:
 * >= 0  Received file descriptor
 * -1    Failed: See errno
 */
int
recv_fd(int s) {
	int z;
	struct msghdr msg;    /* Message header */
	struct iovec iov[1];   /* I/O vector */
	struct cmsghdr *cmsp = NULL;
	char buf[CMSG_SPACE(sizeof(int))];
	char dbuf[80];        /* Small data buffer */

	/*
	 * Initialize structures to zero bytes:
	 */
	memset(&msg,sizeof msg);
	memset(buf,0,sizeof buf);

	/*
	 * No socket addresses are used here:
	 */
	msg.msg_name = NULL;
	msg.msg_namelen = 0;

	/*
	 * Install our I/O vector:
	 */
	msg.msg_iov = iov;
	msg.msg_iovlen = 1;

	/*
	 * Initialize I/O vector to read data
	 * into our dbuf[] array:
	 */
	iov[0].iov_base = dbuf;
	iov[0].iov_len = sizeof dbuf;

	/*
	 * Load control data into buf[]:
	 */
	msg.msg_control = buf;
	msg.msg_controllen = sizeof buf;

	/*
	 * Receive a message:
	 */
	do {
		z = recvmsg(s,&msg,0);
	} while ( z == -1 && errno == EINTR );

	if ( z == -1 )
		return -1;	/* Failed: see errno */

	/*
	 * Walk the control structure looking for
	 * a file descriptor:
	 */
	for ( cmsgh = CMSG_FIRSTHDR(&msg);
		cmsgh != NULL;
		cmsgh = CMSG_NXTHDR(&msg,cmsgh) ) {

		if ( cmsgh->cmsgh_level == SOL_SOCKET
		    && cmsgh->cmsgh_type == SCM_RIGHTS ) {
			/*
			 * File descriptor found:
			 */
			return *(int *) CMSG_DATA(cmsgh);
		}
	}

	/*
	 * No file descriptor was received:
	 * If we received 4 bytes, assume we
	 * received an errno value... then
	 * set errno from our received data.
	 */
	if ( z == sizeof(int) )
		errno = *(int *)buf;	/* Rcvd errno */
	else
		errno = ENOENT;	/* Default errno */

	return -1; /* Return failure indication */
}
```

The function `recv_fd()` implements the following procedure:

- 1. The input argument `s` is the socket that the server response is to come from (line 20).
- 2. This function expects to receive only one ancillary data object containing a file descriptor. This allows the buffer size to be simply stated as shown in line 25. Note that if multiple ancillary objects might be received, you will need to declare a larger buffer than the one shown on line 25.
