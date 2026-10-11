```
struct sockaddr_in dest;
char buffer[MAXBUF];

/*--- Create socket and assign a port number ---*/
sockfd = socket(AF_INET, SOCK_STREAM, 0);
bzero(&dest, sizeof(dest));
dest.sin_family = AF_INET;
dest.sin_port = htons(atoi(strings[2]));
inet_addr(strings[1], &dest.addr.s_addr);

/*--- Connect to server & send request ---*/
if ( connect(sockfd, &dest, sizeof(dest)) != 0 )
    PANIC("connect() failed");
printf(buffer, "%s\n", strings[3]);
send(sockfd, buffer, strlen(buffer), 0);
/*--- Clear buffer and read SHORT reply ---*/
bzero(buffer, MAXBUF);
recv(sockfd, buffer, MAXBUF-1, 0);
printf("%s", buffer);
close(sockfd);
return 0;
}
```

If you want to use this algorithm to get a long reply, you need to change the last section to the following:

```
/****************************************/
/*--- Revising the code to get lengthy replies  ---*/
/****************************************/
/*--- Clear buffer and read SHORT reply ---*/
do
{
     bzero(buffer, MAXBUF);
     bytes = recv(sockfd, buffer, MAXBUF, 0);
     printf("%s", buffer);
}
while ( bytes > 0 );
close(sockfd);
```

This addition works correctly if the server closes the connection after sending you the data. Otherwise, your program waits indefinitely for data.

Waiting for information is a particular problem with socket programming. Sometimes you can trust the server to close the connection when it is done sending. However, some servers expect to leave the channel open until the client closes it. Be aware that if your program waits for a long time, you may be facing that type of problem.