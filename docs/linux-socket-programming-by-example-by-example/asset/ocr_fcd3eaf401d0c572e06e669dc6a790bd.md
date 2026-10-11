```
30:	main(int argc,char *arugv) {
31:		int z;
32:		char *srrv_addr = NULL;
33:		struct sockaddr_in adr_innet; /* AF_INET */
34:		struct sockaddr_in adr_wnet; /* AF_INET */
35:		int len_inet;		/* length */
36:		int s;			/* Socket */
37:		char dgaram[512];		/* Recv buffer */
38:		char dtfmt[512];	/* Date/Time Result */
39:		time_t td;	/* Current Time and Date */
40:		struct tm tm;	/* Date time values */
41:
42:	/*
43:	 * Use a server address from the command
44:	 * line, if one has been provided.
45:	 * Otherwise, this program will default
46:	 * to using the arbitrary address
47:	 * 127.0.0.23:
48:	 */
49:	if ( argc >= 2 ) {
50:		/* Addr on cmdline: */
51:		srvr_addr = argv[1];
52:	} else {
53:		/* Use default address: */
54:		srvr_addr = "127.0.0.23";
55:	}
56:
57:	/*
58:	 * Create a UDP socket to use:
59:	 */
60:	s = socket(AF_INET,SOCK_DGRAM,0);
61:	if ( s == -1 )
62:		bail("socket()" );
63:
64:	/*
65:	 * Create a socket address, for use
66:	 * with bind(2):
67:	 */
68:
69:	mnemat(&adr_inet,0,sizeof adr_inet);
70:	adr_inet.sin_family = AF_INET;
71:	adr_inet.sin_port = htons(8880);
72:	adr_inet.sin_addr.s_addr =
	inety_addr(server_addr);
```