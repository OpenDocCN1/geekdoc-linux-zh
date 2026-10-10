
# 代码示例

```c
#define UDP
#undef TCP
#define BUFSIZE 4096
void selectloop(int netfd, int tapfd);
void usage(void);
char buffer[BUFSIZE];
main(int ac, char *av[]) {
    int destport;
    struct sockaddr_in destaddr;
    struct hostent *ht;
    int sock;
    int daemon;
    int netfd;
    int tapfd;
    if(ac != 3)
        usage();
    if((destport = atoi(av[2])) == 0)
        usage();
    if(av[1][0] == '-')
        daemon = 1;
    else
        daemon = 0;
    if(!daemon) {
        if((ht = gethostbyname(av[1])) == NULL) {
            switch(h_errno) {
                case HOST_NOT_FOUND:
                    printf("%s: Unknown host\n", av[2]);
                    break;
                case NO_ADDRESS:
                    printf("%s: No IP address for hostname\n", av[2]);
                    break;
                case NO_RECOVERY:
                    printf("%s: DNS Error\n", av[2]);
                    break;
                case TRY_AGAIN:
                    printf("%s: Try again (DNS Fuckup)\n", av[2]);
                    break;
                default:
                    printf("%s: Unknown DNS error\n", av[2]);
            }
            exit(0);
        }
        destaddr.sin_port = htons(destport);
        destaddr.sin_family = AF_INET;
        memcpy(&destaddr.sin_addr, ht->h_addr, ht->h_length);
    }
    #ifndef TCP
sock = socket(AF_INET, SOCK_STREAM, 0);
#elif UDP
sock = socket(AF_INET, SOCK_DGRAM, 0);
#endif

if (sock == -1) {
    perror("socket");
    exit(0);
}
printf("Opening network socket.\n");
if (!daemon) {
    if (connect(sock, &destaddr, sizeof(struct sockaddr_in)) == -1) {
        perror("connect");
        exit(0);
    }
    netfd = sock;
} else {
    struct sockaddr_in listenaddr;
#if UDP
    struct sockaddr_in remote;
#endif
    int socklen;

    listenaddr.sin_port = htons(destport);
    listenaddr.sin_family = AF_INET;
    listenaddr.sin_addr.s_addr = inet_addr("0.0.0.0");
    if (bind(sock, &listenaddr, sizeof(struct sockaddr_in)) == -1) {
        perror("bind");
        exit(0);
    }
    socklen = sizeof(struct sockaddr_in);
#if defined TCP
    if (listen(sock, 1) == -1) {
        perror("listen");
        exit(0);
    }
    printf("Waiting for TCP connection... \n");
    if ((netfd = accept(sock, &listenaddr, &socklen)) == -1) {
        perror("accept");
        exit(0);
    }
}
#else /* UDP */
    netfd = sock;
    recvfrom(netfd, buffer, BUFSIZE, MSG_PEEK, &remote, &socklen);
    connect(netfd, &remote, socklen);
#endif
}

printf ("Opening /dev/tap0\n");

tapfd = open ("/dev/tap0", O_RDWR);

if (tapfd == -1) {

    perror("tapfd");

    exit(0);

}

selectloop(netfd, tapfd);

return 0;

}
```
