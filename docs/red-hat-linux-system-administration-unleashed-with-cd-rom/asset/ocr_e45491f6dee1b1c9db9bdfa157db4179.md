# LISTING 7.1 continued

```
```c
fd_set rset;                /* used for select() call */
struct timeval tv;          /* structure used to set the timeout */
int retval = 0;             /* the value returned by select() */
int timeout = 30;           /* the default timeout is 30 seconds */
int count = 0;              /* the number of characters pending */
int val;                    /* FLAGS to set with fcntl */
char *buffer;               /* buffer to hold characters read */
struct termios term;        /* used to set noecho mode */
struct termios termsave;    /* used to restore terminal state */

/* Zero the fd_set and then set a watch on STDIN */
FD_ZERO(&rset);
FD_SET(STDIN_FILENO, &rset);

fprintf(stderr, "argc = %d\n", argc);
switch (argc) {
case 1: {
    break;
}
case 2: {
    if (isdigit(argv[1][0])) {
        timeout = atoi(argv[1]);
    } else {
        fprintf(stderr, "Usage: %s [nnn]\n", argv[0]);
        fprintf(stderr, " where nnn is the number of seconds\n");
        fprintf(stderr, " to wait for input. (default is 30)\n");
        exit(-1);
    }
    break;
}
default: {
    fprintf(stderr, "Usage: %s [-e] [nnn]\n", argv[0]);
    fprintf(stderr, " where nnn is the number of seconds\n");
    fprintf(stderr, " to wait for input. (default is 30)\n");
    exit(-1);
}
}

/* set the timeout for the select call */
tv.tv_sec = timeout;
tv.tv_usec = 0;
```
```