```
```
68:	bail("fcntl(2)");
69:
70:	/*
71:	 * Catch SIGURG:
72:	 */
73:	signal(SIGURG,sigurg);
74:
75:	/*
76:	 * Receive the OOB data inline:
77:	 */
78:	z = setsockopt(s,
79:			SOL_SOCKET,
80:			SO_OOBINLINE,
81:			&oobinline,
82:			sizeof oobinline);
83:	if ( z == -1 )
84:	bail("setsockopt(2)");
85:
86:	for (;;) {
87:		printf("[\n%s]\n",
88:			Socketmark(s)
89:			? "AT MARK"
90:			: "No Mark");
91:
92:		z = recv(s,buf,sizeof buf,0);
93:		if ( z == -1 )
94:		bail("recv(2)");
95:		if ( z == 0 )
96:		break;
97:		buf[z] = 0;
98:
99:		printf("rcv `%s' (%d)\n",
				buf, z);
101:	}
102:
103:	close(s);
104:	return 0;
105:	}
```
```

This program is very similar to the oobrecv.c module, so only the differences will be highlighted here. They are

+   1. The include file for sys/ioctl.h is added in line 12 for the benefit of ioctl(2) call later in the program.
+   2. The signal handler for SIGURG is modified to report only that the signal was raised (lines 22 to 27).
+   3. A new function Socketmark() is defined in lines 33 to 42 to emulate the new socketmark(3) function.