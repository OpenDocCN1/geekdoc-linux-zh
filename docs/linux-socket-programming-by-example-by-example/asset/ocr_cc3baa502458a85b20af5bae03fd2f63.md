# **Listing 2.3:** af_unix.c—Initializing an AF_LOCAL/AF_UNIX Socket Address to /dev/prINTER

```
```
1:	/* af_unix.c:
2:	 * 
3:	 * AF_UNIX Socket Example:
4:	 */
5:	#include <stdio.h>
6:	#include <unistd.h>
7:	#include <stdlib.h>
8:	#include <errno.h>
9:	#include <string.h>
10:	#include <sys/types.h>
11:	#include <sys/stat.h>
12:	#include <sys/socket.h>
13:	#include <sys/un.h>
14:	
15:	/*
16:	 * This function reports the error and
17:	 * exits back to the shell:
18:	 */
19:	static void
20:	bail(const char *on_what) {
21:		perror(on_what);
22:		exit(1);
23:	}
24:	
25:	int
26:	main(int argc,char **argv,char **envp) {
27:		int z;			/* Status return code */
28:		int sock_unix;	/* Socket */
29:		struct sockaddr_un adr_unix;/* AF_UNIX */
30:		int len_unix;		/* length */
31:		const char ptn_unix[]	/* pathname */
32:			= "/tmp/my_sock";
33:	
34:		/*
35:		 * Create a AF_UNIX (aka AF_LOCAL) socket:
36:		 */
37:		sck_unix = socket(AF_UNIX,SOCK_STREAM,0);
38:		
39:		if ( sck_unix == -1 )
40:			bail("socket()");
41:	
42:		/*
43:		 * Here we remove the pathname for the
44:		 * socket, in case it existed from a
45:		 * prior run. Ignore errors (it might
46:		 * not exist).
```
```

*continues*