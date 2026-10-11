```
Listing 17.4: continued
8:	* Receive Data & Credentials:
9:	*
10:	* ARGUMENTS:
11:	* s 		 Socket to read from
12:	* credp 	Ptr to receiving area for cred.
13:	* buf 	Ptr to receiving buffer for data
14:	* bufsize 	Maximum # of bytes for buffer
15:	* addr 	Ptr to buffer to receive peer
16:	*		 address (or NULL)
17:	* alen 	Ptr to Maximum byte length
18:	*		 (updated with actual length
19:	*		 upon return.)
20:	*
21:	* RETURNS:
22:	* >=0 		 Data bytes read
23:	* -1 		 Failed: check errno
24:	*
25:	* NOTES:
26:	* The value -1 is returned with errno set
27:	* to ENOENT, if data is returned without
28:	* any credentials.
29:	*/
30:	int
31:	recv_cred(
32:	int s, /* Socket */
33:	struct ucred *credp, /* Credential buffer */
34:	void *buf, /* Receiving Data buffer */
35:	unsigned bufsize, /* Recv. Data buf size */
36:	void *addr, /* Received Peer address */
37:	socklen_t *alen) { /* Ptr to addr length */
38:
39:	int z;
40:	struct msghdr msgh; /* Message header */
41:	struct iovec iov[1]; /* I/O vector */
42:	struct cmsghdr *cmsgp = NULL;
43:	char mbuf[CMSG_SPACE(sizeof *credp)];
44:
45:	/*
46:	* Zero out message areas:
47:	*/
48:	mmemset(&msgh, 0, sizeof msgh);
49:	mmemset(mbuf, 0, sizeof mbuf);
50:
51:	/*
52:	* Establish datagram address (if any):
53:	*/
```