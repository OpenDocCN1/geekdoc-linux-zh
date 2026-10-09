
In this new example, only the server’s socket address is known to the server and the clients. A client socket address is known only to that client; the server gets it from its call to *recvfrom*. I left the *read* calls in the clients alone, but those could have been calls to *recvfrom* as well. There’s more output since there are now three clients:

```
Got "message #1" back
Got "message #2" back
Got "message #3" back
Got "message #4" back
Got "message #1" back
Got "message #2" back
Got "message #3" back
Got "message #4" back
Got "message #1" back
Got "message #2" back
Got "message #3" back
Got "message #4" back
```

## 8.6.3 sendmsg and recvmsg

There are variants of *sendto* and *recvfrom* that use the same flags and have the same return value but which use a single argument that points to a *msghdr* structure that contains both the socket address and the message. They’re capable of scatter reading and gather writing, just like *readv* and *writev*, which we saw way back in Section 2.15.

```
sendmsg—send message to socket using msghdr structure

#include <sys/socket.h>

ssize_t sendmsg(
int socket_fd,         /* socket file descriptor */
const struct msghdr *message, /* message */
int flags              /* flags */
);
/* Returns number of bytes sent or -1 on error (sets errno) */
```

```
recvmsg—receive message from socket using msghdr structure

#include <sys/socket.h>

ssize_t recvmsg(
int socket_fd,         /* socket file descriptor */
struct msghdr *message, /* message */
int flags              /* flags */
);
/* Returns number of bytes received, 0, or -1 on error (sets errno) */
```

### struct msghdr—structure for sendmsg and recvmsg

```
struct msghdr {       /* optional address */
    void *msg_name;
    socklen_t msg_namelen; /* size of address */
    struct iovec *msg_iov; /* scatter/gather array */
    int msg_iovlen; /* number of elements in msg_iov */
    void *msg_control; /* ancillary data */
    socklen_t msg_controllen; /* ancillary data buffer len */
    int msg_flags; /* flags on received message */
};
```

For **sendmsg**, the socket address is pointed to by the misnamed **msg_name** member, and the socket-address length goes in **msg_namelen**. The data to be sent is pointed to via the **msg_iov** member, which points to an **iovec** structure and is used just as with **writev**. Member **msg_iovlen** is the number of elements in the **msg_iov** array. I explained setting up these members in Section 2.15. Member **msg_flags** is ignored.

For **recvmsg**, you can set **msg_name** to **NULL** or to a buffer of length **msg_namelen** to receive the sender’s socket address, similar to the way **recvfrom** works. When **recvmsg** returns, **msg_namelen** is changed to the actual socket-address length. Members **msg_iov** and **msg_iovlen** are used as with **readv**. There’s one portable flag that can be set in the returned **msg_flags** member: **MSG_TRUNC**, which means that the message was too long to fit in the supplied buffers.

The socket-address members, **msg_name** and **msg_namelen**, are used as with connectionless sockets; for connected sockets they’re ignored.

The two other members I didn’t explain, **msg_control** and **msg_controllen**, are used for ancillary data that has to do with access rights. I won’t go into it here, but you can read about it in [SUS2002] or in your system’s documentation.

Here’s just the **run_server** function from the previous section redone to use **recvmsg** and **sendmsg**:

```c
static void run_server(void)
{
    int fd_skt;
    ssize_t nrecv;
    char msg[MSG_SIZE];
    struct sockaddr_storage sa;
    struct msghdr m;
    struct iovec v;

    ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
    ec_neg1( bind(fd_skt, (struct sockaddr *)&sa_server, sizeof(sa_server)) )
    while (true) {
        memest(&m, 0, sizeof(m));
        m.msg_name = &sa;
        m.msg_namelen = sizeof(sa);
        v.iov_base = msg;
        v.iov_len = sizeof(msg);
        m.msg_iov = &v;
        m.msg_iovlen = 1;
        ec_neg1( nrecv = recvmsg(fd_skt, &m, 0) )
        if (nrecv != sizeof(msg)) {
            printf("server got short message\n");
            break;
        }
        ((char *)m.msg_iov->iov_base)[0] = 'm';
        ec_neg1( sendmsg(fd_skt, &m, 0) )
    }

    c_neg1( close(fd_skt) )
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

There’s additional work to set up the msghdr structure, but the recvmsg and sendmsg calls are then very simple. Imagine an application where there are a lot of different messages being sent to different addresses, and you can begin to see the benefits of keeping the addresses in the same structure as the message data.

## 8.6.4 Using connect with Connectionless Sockets

Normally a client uses connect (Section 8.1.2) to connect with a server’s socket, but it also works with connectionless sockets to establish a default address for subsequent sends and recvs, which don’t take a socket-address argument. The specifics of those two system calls are in Section 8.9.1.

Calling connect with a NULL socket address removes the default address.

## 8.7 Out-of-Band Data

Occasionally it's necessary to send an urgent message on a socket connection. If it's sent inline, it won't be read until everything ahead of it is read first, so there's a way to send it out-of-band. The receiver also must be receiving out-of-band messages.

To send an out-of-band message, set the MSG_OOB flag with sendto, sendmsg, or send.

A receiver using select (Section 8.1.3) finds out about an out-of-band message through the so-called "error" set of file descriptors passed as the fourth argument to select. Then it gets the message by setting the MSG_OOB flag in a call to recvfrom, recvmsg, or recv. Or, it can just check for an out-of-band message every time it's about to receive ordinary data by calling one of the receiving functions with the O_NONBLOCK flag set on the socket file descriptor (via fcntl, Section 3.8.3) and MSG_OOB set for the receiving call.

If the SO_OOBINLINE option is set (Section 8.3), out-of-band data may be placed inline, along with the other data. The protocol may precede the out-of-band data with an out-of-band mark, ignored when data is read, but whose presence can be detected with a call just for that purpose:

```
sockatmark—test presence of out-of-band mark
#include <sys/socket.h>
int sockatmark(
    int socket_fd    /* socket file descriptor */
);
/* Returns 1 if at mark, 0 if not, or -1 on error (sets errno) */
```

The problem with sockatmark is that, if it returns 0 because the socket is empty, out-of-band data may arrive after the call to sockatmark but before the next receive operation. Since the out-of-band mark is ignored when data is received, the mark will be lost. The way to avoid this is ensure that data is ready to be received before calling sockatmark, with, for example, a call to select. That way a 0 return from sockatmark means unambiguously that there is data, but it is not preceded by the out-of-band mark.

You can also arrange to get a SIGURG signal when out-of-band data has arrived. To do this, call fcntl with the F_SETOWN operation to set the process or process-group that should get the signal. For more details, see [SUS2002] or your system's documentation.

## 8.8 Network Database Functions

These *network database* functions provide information about hosts, networks, protocols, and services. I already introduced the most important of these functions, getaddrinfo, in Section 8.2.6. Another handy function, gethostname, was in Section 8.2.7. Here I’ll describe the rest, grouped according to the kind of information they deal with.

### 8.8.1 Host Functions

The three functions for scanning the host database are:

- **sethostent**—start host-database scan

```
#include <netdb.h>

void sethostent( int stayopen /* leave connection open? */
      );
```

- **gethostent**—get next host-database entry

```
#include <netdb.h>

struct hostent *gethostent(void);
/* Returns next entry or NULL on end of database (errno not defined) */
```

- **endhostent**—end host-database scan

```
#include <netdb.h>

void endhostent(void);
```

**struct hostent**—structure for host-database functions

```
struct hostent {
  char  *h_name;             /* official host name */
  char  **h_aliases;         /* array of alternative host names */
  int     h_addrtype;        /* address family (not type) */
  int     h_length;          /* length of each address */
  char  **h_addr_list;       /* array of pointers to network addresses */
};
```

You can call *gethostent* in a loop to scan through all the known host names. You start the scan with *sethostent*, using the argument to indicate whether the connection to the host database should stay open, or whether *gethostent* should open and close it each time it’s called. You call *endhostent* at the end. Thus, it sounds like a lot could be happening, but in practice all these functions are likely to do is scan the /etc/hosts file on the local machine.
