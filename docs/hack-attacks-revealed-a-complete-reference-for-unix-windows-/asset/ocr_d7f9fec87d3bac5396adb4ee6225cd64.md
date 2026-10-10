```
sock = socket(AF_INET, SOCK_STREAM, 0);
#elseif
#endif UDP
sock = socket(AF_INET, SOCK_DGRAM, 0);
#endif
if (sock == -1) {
perror("socket");
exit(0);
}
printf("Opening network socket.\n");
if (!daemon) {

if (connect (sock, &destaddr, sizeof(struct sockaddr_in)) ==
-1) {
perror("connect");
exit(0);
}
netfd = sock;
} else {
struct sockaddr_in listenaddr;
#endif UDP
struct sockaddr_in remote;
#endif
int socklen;
listenaddr.sin_port = htons(destport);
listenaddr.sin_family = AF_INET;
listenaddr.sin_addr.s_addr = inet_addr ("0.0.0.0");
if (bind(sock, &listenaddr, sizeof(struct sockaddr_in)) ==
-1) {
perror("bind");
exit(0);
}
socklen = sizeof(struct sockaddr_in);
#ifife TCCP
if (listen (sock, 1) == -1) {
perror("listen");
exit(0);
}
printf("Waiting for TCP connection... \n");
if ((netfd = accept (sock, &listenaddr, &socklen)) == -1) {
perror("accept");
exit(0);
}
} #else /* TCP */
netfd = sock;
recvfrom (netfd, buffer, BUFSIZE, MSG_PEEK, &remote,
&socklen);
connect (netfd, &remote, socklen);
#endif
}
printf ("Opening /dev/tap0\n");
tapfd = open ("/dev/tap0", O_RDWR);
if (tapfd == -1) {
```

613