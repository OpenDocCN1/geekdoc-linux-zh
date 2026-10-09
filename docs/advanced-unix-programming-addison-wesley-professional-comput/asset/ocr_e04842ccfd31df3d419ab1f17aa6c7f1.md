# 572 Chapter 8: Networking and Sockets

or the call is interrupted by a signal, termination of the con-nec-
tion, or an error. Has no effect on connectionless sockets because
the message is always indivisible.

Here’s my example reworked to use recvfrom and to have several peers sending
to the same socket, so it’s a client/server arrangement:

```
#define SOCKETNAME_SERVER "Sktoner"
#define SOCKETNAME_CLIENT "SkTwo"
static struct sockaddr_un sa_server;
#define MSG_SIZE 100
static void run_client(int nclient)
{
    struct sockaddr_un sa_client;
    int fd_skt;
    ssize_t nrecv;
    char msg[MSG_SIZE];
    int i;

    if (fork() == 0) {  /* client */
    sleep(1);  /* let server startup first */
    ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
    snprintf(sa_client.sun_path, sizeof(sa_client.sun_path),
        "%s-%d", SOCKETNAME_CLIENT, nclient);
    (void)unlink(sa_client.sun_path);
    sa_client.sun_family = AF_UNIX;
    ec_neg1( bind(fd_skt, (struct sockaddr *)sa_client,
        sizeof(sa_client)) )
    for (i = 1; i <= 4; i++) {
    snprintf(msg, sizeof(msg), "Message #%d", i);
    ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
        (struct sockaddr *)sa_server, sizeof(sa_server)) )
    ec_neg1( nrecv = read(fd_skt, msg, sizeof(msg)) )
    if (nrecv != sizeof(msg)) {
        printf("Client got short message\n");
        break;
    }
    printf("Got \"%s\" back\n", msg);
    }
    ec_neg1( close(fd_skt) )
    exit(EXIT_SUCCESS);
    }
return;
```