# Listing 17.6: continued

```
26: 		* Create a Unix Socket:
27: 		*/
28: 	s = socket(PF_LOCAL, SOCK_STREAM, 0);
29: 	if ( s == -1 )
30: 		return -1; 	/* Failed: check errno */
31:
32: 		/*
33: 		* Create the abstract address of
34: 		* the socket server:
35: 		*/
36: 	memset(&a_srvr, 0, sizeof a_srvr);
37: 	a_srvr.sun_family = AF_LOCAL;
38: 	strncpy(a_srvr.sun_path,
39: 		"$SOCKET-SERVER",
40: 			sizeof a_srvr.sun_path-1);
41: 	a_srvr.sun_path[0] = 0;
42:
43: 		/*
44: 		* Connect to the sock server:
45: 		*/
46: 	z = connect(s,&a_srvr,sizeof a_srvr);
47: 	if ( z == -1 )
48: 		return -1; 	/* Failed: check errno */
49:
50: 		/*
51: 		* Now issue our request:
52: 		*/
53: 	do {
54: 		z = write(s,&port,sizeof port);
55: 	} while ( z == -1 && errno == EINTR );
56:
57: 	if ( z == -1 )
58: 		return -1; 		/* Failed: see errno */
59:
60: 		/*
61: 		* Now wait for a reply:
62: 		*/
63: 	z = recv_fd(s);
64: 	close(s);
65:
66: 	return z; 			/* z = fd or -1 */
67: 	}
```