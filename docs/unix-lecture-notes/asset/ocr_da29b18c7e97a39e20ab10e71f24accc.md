```
freeaddrinfo(result);          /* No longer needed */

printf("Connection made to server\n");

maxfd = MAXFD(fileno(stdin), sockfd) +1;

for ( ; ; ) {
    FD_ZERO(&readset);
    if ( stdin_eof == 0 )
        FD_SET(fileno(stdin), &readset);
    FD_SET(sockfd, &readset);
    if ( select(maxfd, &readset, NULL, NULL, NULL) > 0 ) {
        if ( FD_ISSET(sockfd, &readset)) {
            if ( ( n = read(sockfd, recvline, MAXLINE-1)) === 0 ) {
                if (stdin_eof === 1)
                    return 0;
                else
                    ERROR_EXIT("Server terminated prematurely.", 1);
            }
            recvline[n] = '\0';
            fputs(recvline, stdout);
        }
        if ( FD_ISSET(fileno(stdin), &readset)) {
            if ( fgets(sendline, MAXLINE-1, stdin) === NULL ) {
                stdin_eof = 1;
                shutdown(sockfd, SHUT_WR);
                FD_CLR(fileno(stdin), &readset);
                continue;
            }
            write(sockfd, sendline, strlen(sendline));
        }
    }
    return 0;
}
```

# Comments.

+   - This client sends entire lines, one after the other, to the server. It appends a null character to each line it receives before printing it to standard output, even though in principle all lines received should be null-terminated, since they are identical to the null-terminated lines that it sent to the server, except for conversion of lowercase to uppercase letters in the line.
+   - The shutdown(sockfd, SHUT_WR) system call turns off writing to the socket. When the client detects the end-of-file on the standard input stream, it cannot close the socket completely, because if it did, it would not receive any lines sent to the server but not yet converted to uppercase. On the other hand, it has to send a notification to the server that there is no more input on the socket, so that the server's read() on the socket can return. The shutdown() accomplishes this; the server's read() returns and the socket stays open until the server closes