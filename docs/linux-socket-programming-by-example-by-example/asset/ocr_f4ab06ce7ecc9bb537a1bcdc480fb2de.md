```
```c
41:
42:     if (z == -1) {
43:         fprintf(stderr,"$s: socketpair(2)\n",
44:                 strerror(errno));
45:         exit(1);
46:     }
47:     /
48:     * Now fork() into two processes:
49:     */
50:     if ((chpid = fork()) == pid_t -1) {
51:         /*
52:          * Failed to fork into two processes:
53:          */
54:         fprintf(stderr,"%s: fork(2)\n",
55:                 strerror(errno));
56:         exit(1);
57:     } else if (chpid == 0) {
58:         /*
59:          * This is the child process (client):
60:          */
61:         char rxbuf[80]; /* Receive buffer */
62:         printf("Parent PID is %ld\n",(long)getppid());
63:         close(s[0]);      /* Server uses s[1] */
64:         s[0] = -1;        /* Forget this unit */
65:         /*
66:          * Form the message and its length:
67:          */
68:         msgp = "%A %d-%b-%Y %l:%M %p";
69:         mlen = strlen(msgp);
70:         printf("Child sending request '$s'\n",msgp);
71:         fflush(stdout);
72:         /*
73:          * Write a request to the server:
74:          */
75:         z = write(s[1],msgp,mlen);
76:         if (z < 0 ) {
77:             fprintf(stderr,"$s: write(2)\n",
```
```