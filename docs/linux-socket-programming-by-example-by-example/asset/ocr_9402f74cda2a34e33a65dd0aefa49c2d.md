contains the value of AF_INET, each pointer in this array of pointers points to a 4-byte IP address. The end of the list is marked by a NULL pointer.

# Applying the gethostbyname(3) Function

A short demonstration program for the function gethostbyname(3) has been provided in Listing 9.4. This program accepts multiple hostnames on the command line and then queries the name server for each. All available information is reported to standard output, or an error is reported if the name cannot be resolved.

Listing 9.4: Lookup.c—Demonstration Program for gethostbyname(3)

![](bbox=[0.09, 0.33, 0.18, 0.45])

```
1: /* lookup.c:
2:  *
3:  * Example of gethostbyname(3):
4:  */
5: #include <stdio.h>
6: #include <unistd.h>
7: #include <stdlib.h>
8: #include <string.h>
9: #include <errno.h>
10: #include <sys/socket.h>
11: #include <netinet/in.h>
12: #include <arpa/inet.h>
13: #include <netdb.h>
14: 
15: extern int h_errno;
16: 
17: int
18: main(int argc,char **argv) {
19: 	int x, x2;
20: 	struct hostent *hp;
21: 
22: 	for (x=1; x<argc; ++x ) {
23: /*
24: 	* Look up the hostname:
25: 	*/
26: 	hp = gethostbyname(argv[x]);
27: 	if ( !hp ) {
28: 	/* Report lookup failure */
29: 	fprintf(stderr,
30: 		"%s: host '%s'\n",
31: 		hstrerror(h_errno),
32: 		argv[x]);
33: 		continue;
34: 	}
35: 
```