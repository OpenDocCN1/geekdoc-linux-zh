```
8:  #include <errno.h>
9:  #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12: #include <netinet/in.h>
13: #include <arpa/inet.h>
14: #include <netdb.h>
15: 
16: /*
17:  * This function reports the error and
18:  * exits back to the shell:
19: */
20: static void
21: bail(const char *on_what) {
22:     fputs(strerror(errno),stderr);
23:     fputs(": ",stderr);
24:     fputs(on_what,stderr);
25:     fputc('\n',stderr);
26:     exit(1);
27: }
28: 
29: int
30: main(int argc,char **argv) {
31:     int z;
32:     char *srvr_addr = NULL;
33:     struct sockaddr_in addr_srvr;/* AF_INET */
34:     int len_inet;                 /* Length  */
35:     int s;                       /* Socket  */
36:     struct servent *sp;         /* Service entry */
37:     char dtbuf[128];            /* Date/Time info */
38: 
39: /*
40:  * Use a server address from the command
41:  * line, if one has been provided.
42:  * Otherwise, this program will default
43:  * to using the arbitrary address
44:  * 127.0.0.1:
45: */
46: if ( argc >= 2 ) {
47:     /* Addr on cmdline: */
48:     srvr_addr = argv[1];
49: } else {
50:     /* Use default address: */
51:     srvr_addr = "127.0.0.1";
52: }
53:
```