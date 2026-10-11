Listing 11.2: continued

```
10: #include <time.h>
11: #include <sys/types.h>
12: #include <sys/socket.h>
13: #include <netinet/in.h>
14: #include <arpa/inet.h>
15: #include <netdb.h>
16: #include <sys/wait.h>
17: #include <signal.h>
18:
19: #ifndef SHUT_RDWR
20: #define SHUT_RDWR 3
21: #endif
22:
23: extern int mkaddr(void *addr,
24: int *addr_len,
25: char *input_address,
26: char *protocol);
27:
28: extern void rpn_process(FILE *tx,
29: char *buf);
30:
31: /*
32: * Process Terminated Child processes:
33: */
34: static void
sigchld_handler(int signo) {
36: pid_t PID;
37: int status;
38:
39: do {
40: PID = waitpid(-1,&status,WNOHANG);
41: } while ( PID != -1 );
42:
43: /* Re-instate handler */
44: signal(SIGCHLD,sigchld_handler);
45: }
46:
47: /*
48: * This function reports the error and
49: * exits back to the shell:
50: */
51: static void
52: bail(const char *on_what) {
53: if ( errno != 0 ) {
54: fputs(strerror(errno),stderr);
55: fputs(": ",stderr);
```