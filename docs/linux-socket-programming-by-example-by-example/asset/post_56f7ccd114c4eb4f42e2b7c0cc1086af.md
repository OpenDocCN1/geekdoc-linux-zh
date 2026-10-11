
Another way this problem is manifested is after a `fork(2)` function has been called upon. Any sockets that existed prior to a `fork` operation would be duplicated in the child process.

> **TIP**
>
> Use the `shutdown(2)` function instead of the `close(2)` function whenever immediate or partial shutdown action is required. Duplicated file descriptors from `dup(2)`, `dup2(2)`, or `fork(2)` operations can prevent a `close(2)` function from initiating any shutdown action until the last outstanding descriptor is closed.

## Shutting Down Reading from a Socket

Shutting down the read side of the socket causes any pending read data to be silently ignored. If more data is sent from the remote socket, it too is silently ignored. Any attempt by the process to read from that socket, however, will have an error returned to it. This is often done to enforce protocol or to help debug code.

## Knowing When Not to Use `shutdown(2)`

The `shutdown(2)` function is documented to return the errors shown in Table 1.2.

*Table 1.2: Possible errors returned by `shutdown(2)`*

| Error | Description |
| :--- | :--- |
| EBADF | Given socket is not a valid file descriptor. |
| ENOTSOCK | Given file descriptor is not a socket. |
| ENOTCONN | The specified socket is not connected. |

From Table 1.2, you can see that you should only call `shutdown(2)` for connected sockets. Otherwise, the error code `ENOTCONN` is returned.

> **NOTE**
>
> The `shutdown(2)` function does not release the socket's file unit number, even when `SHUT_RDWR` is used. The socket's file descriptor remains valid and in use until the function `close(2)` is called to release it.
>
> Note also that `shutdown(2)` can be called more than once for the same file unit, provided that the socket is still connected.

## Writing a Client/Server Example

You have now looked at enough of the socket API set to start having some fun with it. In this section, you examine, compile, and test a simple client and server process that communicates with a pair of sockets.

To keep the programming code to a bare minimum, one program will start and then fork into a client process and a server process. The child process will assume the role of the client process, whereas the original parent process will perform the role of the server. Figure 1.3 illustrates the relationship of the parent and child processes and the sockets that will be used.

![](img/961a0296fe36074690a9847b79332eff_42_0.png)

**Figure 1.3**: A Client/Server example using fork(2) and socketpair(2).

The parent process is the original starting process. It will immediately ask for a pair of sockets by calling socketpair(2) and then fork itself into two processes by calling fork(2).

The server will accept one request, act on that request, and then exit. The client likewise in this example will issue one request, report the server response, and then exit.

The request will take the form of the third argument to the strftime(3) function. This is a format string, which will be used to format a date and time string. The server will obtain the current date and time at the time that the request is received. The server will use the client's request string to format it into a final string, which is returned to the client. By way of review, the strftime(3) function's synopsis is as follows:

```c
#include <time.h>
```

![](img/961a0296fe36074690a9847b79332eff_42_1.png)

```c
size_t strftime(char *buf,
size_t max,
const char *format,
const struct tm *tm);
```

The arguments `buf` and `max` indicate the output buffer and its maximum length respectively. The argument `format` is an input string that allows you to format a date and time string (Listing 1.3 line 75 shows an example of such a string). Finally, argument `tm` is used to supply all the date and time components necessary to create the output date and time string. Review the man page for strftime(3) if you need to.

Listing 1.3 shows the source listing for the demonstration client/server program.

### Listing 1.3: $ 01lst03.c——Client/Server Example Using socketpair(2) and fork(2)

```c
  1:  /*  Listing 1.3
  2:    *
  3:    * Client/Server Example Using socketpair(2)
  4:    * and fork(2):
  5:    */
  6:
  7:  #include <stdio.h>
  8:  #include <stdlib.h>
  9:  #include <unistd.h>
 10:  #include <errno.h>
 11:  #include <string.h>
 12:  #include <time.h>
 13:  #include <sys/types.h>
 14:  #include <sys/socket.h>
 15:  #include <sys/wait.h>
 16:
 17:  /*
 18:    *
 19:    * As of RedHat-6.0, these are still not defined:
 20:    */
 21:  #ifndef SHUT_RD
 22:  #define SHUT_RD      0
 23:  #define SHUT_WR      1
 24:  #define SHUT_RDWR    2
 25:  #endif
 26:
 27:  /*
 28:    * Main program:
 29:    */
 30:  int
 31:  main(int argc,char **argv) {
 32:      int z;            /*  Status return code */
 33:      int s[2];        /*  Pair of sockets   */
 34:      char *msgp;     /*  A message pointer */
 35:      int mlen;        /*  Message length    */
 36:      char buf[80];    /*  Work buffer       */
 37:      pid_t child;     /*  Child PID */
 38:
 39:      /*
 40:        * Create a pair of local sockets:
 41:        */
 42:      z = socketpair(AF_LOCAL,SOCK_STREAM,0,s);
 43:      if (z == -1) {
 44:          fprintf(stderr,"$s: socketpair(2)\n",
 45:                  strerror(errno));
 46:          exit(1);
 47:      }
 48:      /*
 49:       * Now fork() into two processes:
 50:       */
 51:      if ((child = fork()) == pid_t -1) {
 52:          /*
 53:           * Failed to fork into two processes:
 54:           */
 55:          fprintf(stderr,"%s: fork(2)\n",
 56:                  strerror(errno));
 57:          exit(1);
 58:      } else if (child == 0) {
 59:          /*
 60:           * This is the child process (client):
 61:           */
 62:          char rxbuf[80]; /* Receive buffer */
 63:          printf("Parent PID is %ld\n",(long)getppid());
 64:          close(s[0]);      /* Server uses s[1] */
 65:          s[0] = -1;        /* Forget this unit */
 66:          /*
 67:           * Form the message and its length:
 68:           */
 69:          msgp = "%A %d-%b-%Y %l:%M %p";
 70:          mlen = strlen(msgp);
 71:          printf("Child sending request '%s'\n",msgp);
 72:          fflush(stdout);
 73:          /*
 74:           * Write a request to the server:
 75:           */
 76:          z = write(s[1],msgp,mlen);
 77:          if (z < 0 ) {
 78:              fprintf(stderr,"%s: write(2)\n",
 79:                  strerror(errno));
 80:              exit(1);
 81:          }
 82:          /*
 83:           * Now indicate that we will not be writing
 84:           * anything further to our socket, by shutting
 85:           * down the write side of the socket:
 86:           */
 87:          if ( shutdown(s[1],SHUT_WR) == -1 ) {
 88:              fprintf(stderr,"%s: shutdown(2)\n",
 89:                  strerror(errno));
 90:              exit(1);
 91:          }
 92:
 93:          /*
 94:           * Receive the reply from the server:
 95:           */
 96:          z = read(s[1],rxbuf,sizeof rxbuf);
 97:          if ( z < 0 ) {
 98:              fprintf(stderr,"%s: read(2)\n",
 99:                  strerror(errno));
100:              exit(1);
101:          }
102:
103:          /*
104:           * Put a null byte at the end of what we
105:           * received from the server:
106:           */
107:          rxbuf[z] = 0;
108:
109:          /*
110:           * Report the results:
111:           */
112:          printf("Server returned '%s'\n",rxbuf);
113:          fflush(stdout);
114:
115:          close(s[1]);	/* Close our end now */
116:
117:      } else {
118:
119:          /*
120:           * This is the parent process (server):
121:           */
122:          int status; /* Child termination status */
123:          char txbuf[80];		/* Reply buffer */
124:          time_t td;    /* Current date & time */
125:
126:          printf("Child PID is %ld\n", (long)child);
127:          fflush(stdout);
128:
129:          close(s[1]);   /* Client uses s[1] */
130:          s[1] = -1;     /* Forget this descriptor */
131:
132:          /*
133:             * Wait for a request from the client:
134:             */
135:          z = read(s[0], buf, sizeof buf);
136:
137:          if ( z < 0 ) {
138:                fprintf(stderr, "%s: read(2)\n",
139:                        strerror(errno));
140:                exit(1);
141:          }
142:
143:          /*
144:             * Put a null byte at the end of the
145:             * message we received from the client:
146:             */
147:          buf[z] = 0;
148:
149:          /*
150:             * Now perform the server function on the
151:             * received message:
152:             */
153:          time(&td);      /* Get current time */
154:
155:          strftime(txbuf, sizeof txbuf,  /* Buffer */
156:                   buf,               /* Input format */
157:                   localtime(&td));   /* Input time */
158:
159:          /*
160:             * Send back the response to client:
161:             */
162:          z = write(s[0], txbuf, strlen(txbuf));
163:
164:          if ( z < 0 ) {
165:                fprintf(stderr, "%s: write(2)\n",
166:                        strerror(errno));
167:                exit(1);
168:          }
169:
170:          /*
```
