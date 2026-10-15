```
#define BUFF      256

int main(int argc, char *argv[])
{
    int csock; /* Descriptor for connected socket */
    if (argc != 4) {
        printf("Usage: %s hostname port protocol\n", argv[0]);
        exit(0);
    }

    csock = CreateConnectedSock(argv[1], argv[2], argv[3]);

    /* Perform client-side of the DAYTIME service using csock,  */
    /* the client socket connected the server-side active socket */
    DaytimeClientTCP(csock);

    /* Deallocate socket and return */
    close(csock);
    return 0;
}

int CreateConnectedSock(char *ip, char *portstr, char *protocol)
{
    /* Insert code for the function */
}

/* Client side of the DAYTIME service. 'sock' is the  */
/* client socket connected to serve's active socket.  */
void DaytimeClientTCP(int sock)
{
    int n;
    char buf[BUFF];

    /* Read time string from server and display on screen */
    while ((n = read(sock, buf, BUFF)) > 0)
        write(1, buf, n);
}
```

Here is the compilation and a sample run of the DAYTIME client-server software. As explained previously, on a Solaris machine you would use the gcc -w -lsocket daytime_server_TCP.c -o udpdaytimes command to generate the executable code for the server program and the gcc -w -lsocket -lnsl daytime_client_TCP.c -o udpdaytimec command to generate the executable code for the client program.

```
% gcc46 daytime_server_TCP.c -w -o tcpdaytimes
% gcc46 daytime_client_TCP.c -w -o tcpdaytimec
```