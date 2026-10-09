
will fit; if the O_NONBLOCK flag is set and it won't fit, none of it is sent, −1 is returned, and errno is set to EAGAIN or EWOULDBLOCK.

You can use sendto with a connected socket, but in that case the destination socket address is ignored and the output goes to the socket_fd socket, just as for write. The only advantage over write is that you can specify flags, but, if that's all you want, it would be more straightforward to use send (Section 8.9.1).

Now we can show an example that does what Figure 8.4 shows, with the addition that each peer reads incoming data. Peer 2 gets a message, makes a little change to it, and sends it to Peer 1. Peer 1 puts together four messages to send to Peer 2 and displays the responses. Note that, unlike the connected-socket examples, here both peers do a bind, and neither calls listen, accept, or connect.

```c
#define SOCKETNAME1 "SktOne"
#define SOCKETNAME2 "SktTwo"
#define MSG_SIZE 100

int main(void)
{
    struct sockaddr_un sa1, sa2;
    strcpy(sa1.sun_path, SOCKETNAME1);
    sa1.sun_family = AF_UNIX;
    strcpy(sa2.sun_path, SOCKETNAME2);
    sa2.sun_family = AF_UNIX;
    (void)unlink(SOCKETNAME1);
    (void)unlink(SOCKETNAME2);
    if (fork() == 0) { /* Peer 1 */
    int fd_skt;
    size_t nread;
    char msg[MSG_SIZE];
    int i;
    sleep(1); /* let peer 2 startup first */
    ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
    ec_neg1( bind(fd_skt, (struct sockaddr *)&sa1, sizeof(sa1)) )
    for (i = 1; i <= 4; i++) {
        snprintf(msg, sizeof(msg), "Message #%d", i);
        ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
        (struct sockaddr *)&sa2, sizeof(sa2)) )
        ec_neg1( nread = read(fd_skt, msg, sizeof(msg)) )
        if (nread != sizeof(msg)) {
            printf("Peer 1 got short message\n");
            break;
        }
    }
    printf("Got \"%s\" back\n", msg);
        }
        ec_neg1( close(fd_skt) )
        exit(EXIT_SUCCESS);
    }
    else { /* Peer 2 */
        int fd_skt;
        size_t nread;
        char msg[MSG_SIZE];

        ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
        ec_neg1( bind(fd_skt, (struct sockaddr *)&sa2, sizeof(sa2) ) )
        ec_neg1( nread = read(fd_skt, msg, sizeof(msg)) )
        while (true) {
            if (nread != sizeof(msg)) {
                printf("Peer 2 got short message\n");
                break;
            }
            msg[0] = 'm';
            ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
                     (struct sockaddr *)&sa1, sizeof(sa1)) )
            ec_neg1( close(fd_skt) )
            exit(EXIT_SUCCESS);
        }
    }

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

Putting both processes in the same program isn’t normal; we did it just to make the example simpler. However, we had to stick in the call to `sleep` at the start of the child process (Peer 1) to let Peer 2 go first. Not the best way to sequence things but OK for our present purposes. In a real application getting the server started before the clients isn’t usually a problem. If it is, a correct way to synchronize the two is in Section 9.2.

This is the output:

```
Got "message #1" back
Got "message #2" back
Got "message #3" back
Got "message #4" back
```

For datagrams `read` isn’t really a good choice because it doesn’t tell us who sent the data. This wasn’t a problem for connected sockets because each return from `accept` gave us a separate file descriptor for each client that we could both `read` and write. In the example just given, Peer 2 merely assumed it was supposed to sendto Peer 1, but, in general, applications are more complicated than that.

Sure enough, there’s the opposite of sendto called recvfrom:

```c
recvfrom—receive message from socket

#include <sys/socket.h>

ssize_t recvfrom(
  int socket_fd,                /* socket file descriptor */
  void *buffer,                 /* buffer for received message */
  size_t length,                /* length of buffer */
  int flags,                    /* flags */
  struct sockaddr *sa,          /* address of sender */
  socklen_t *sa_len            /* address length */
);
/* Returns number of bytes received, 0, or -1 on error (sets errno) */
```

recvfrom’s first three arguments are like those of read. In addition, it has a flags argument and two arguments that receive the sender’s socket address.

Prior to the call, you must set sa to something big enough to hold the sender’s socket address, and then sa_len to the size of that storage. On return sa_len is set to the actual size of the address. Then, if you want, you can pass sa and sa_len directly to sendto for a response.

Like sendto, recvfrom always returns a complete message for a connection-less socket. It waits for one if O_NONBLOCK is clear, or, if set, returns −1 with errno to EAGAIN or EWOULDBLOCK.

You could use recvfrom for a connected socket if you want to know the source address, but there’s not a whole lot you can do with that address since it would be ignored in a call to sendto anyway, as previously explained. Another way to get the address of a socket whose file descriptor you have would be to call get-sockname (Section 8.9.2).

There are three portable flags that you can use with recvfrom:

| Flag | Description |
| :--- | :--- |
| MSG_OOB | Receives out-of-band data, if any; see Section 8.7. |
| MSG_PEEK | Returns the message, but leaves it unread for the next read, recvfrom, or other input operation. |
| MSG_WAITALL | For connected sockets only, causes recvfrom to block until the entire requested length is available, unless MSG_PEEK is also set or the call is interrupted by a signal, termination of the connection, or an error. Has no effect on connectionless sockets because the message is always indivisible. |

Here’s my example reworked to use recvfrom and to have several peers sending to the same socket, so it’s a client/server arrangement:

```c
#define SOCKETNAME_SERVER "SktOne"
#define SOCKETNAME_CLIENT "SktTwo"
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

EC_CLEANUP_BGN
  exit(EXIT_FAILURE);
EC_CLEANUP_END
}

static void run_server(void)
{
  int fd_skt;
  ssize_t nrecv;
  char msg[MSG_SIZE];
  struct sockaddr_storage sa;
  socklen_t sa_len;

  ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
  ec_neg1( bind(fd_skt, (struct sockaddr *)&sa_server, sizeof(sa_server)) )
  while (true) {
    sa_len = sizeof(sa);
    ec_neg1( nrecv = recvfrom(fd_skt, msg, sizeof(msg), 0,
                              (struct sockaddr *)(&sa, &sa_len) )
    if (nrecv != sizeof(msg)) {
      printf("server got short message\n");
      break;
    }
    msg[0] = 'm';
    ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
                    (struct sockaddr *)(&sa, sa_len) )
  }
  ec_neg1( close(fd_skt) )
  exit(EXIT_SUCCESS);

EC_CLEANUP_BGN
  exit(EXIT_FAILURE);
EC_CLEANUP_END
}

int main(void)
{
  int nclient;

  strcpy(sa_server.sun_path, SOCKETNAME_SERVER);
  sa_server.sun_family = AF_UNIX;
  (void)unlink(SOCKETNAME_SERVER);
  for (nclient = 1; nclient <= 3; nclient++)
    run_client(nclient);
  run_server();
  exit(EXIT_SUCCESS);
}
```
