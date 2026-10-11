Listing 1.3: continued

```
```
88:				sterror(errno));
89:			exit(1);
90:		}
91:
92:		/*
93:		 * Now indicate that we will not be writing
94:		 * anything further to our socket, by shutting
95:		 * down the write side of the socket:
96:		 */
97:		if ( shutdown(s[1],SHUT_WR) == -1 ) {
98:			fprintf(stderr,"%s: shutdown(2)\n",
99:				sterror(errno));
100:			exit(1);
101:		}
102:
103:		/*
104:		 * Receive the reply from the server:
105:		 */
106:		z = read(s[1],rxbuf,sizeof rxbuf);
107:		if ( z < 0 ) {
108:			fprintf(stderr,"%s: read(2)\n",
109:				sterror(errno));
110:			exit(1);
111:		}
112:
113:		/*
114:		 * Put a null byte at the end of what we
115:		 * received from the server:
116:		 */
117:		rxbuf[z] = 0;
118:
119:		/*
120:		 * Report the results:
121:		 */
122:		printf("Server returned '%s'\n",rxbuf);
123:		fflush(stdout);
124:
125:		close(s[1]);	/* Close our end now */
126:
127:	} else {
128:
129:		/*
130:		 * This is the parent process (server):
131:		 */
132:		int status; /* Child termination status */
133:		char txbuf[80];		/* Reply buffer */
```
```