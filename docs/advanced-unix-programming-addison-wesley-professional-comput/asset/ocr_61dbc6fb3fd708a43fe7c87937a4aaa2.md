# **struct msghdr**—structure for sendmsg and recvmsg

```
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
```

For **sendmsg**, the socket address is pointed to by the misnamed **msg_name** member, and the socket-address length goes in **msg_namelen**. The data to be sent is pointed to via the **msg_iov** member, which points to an **iovec** structure and is used just as with **writev**. Member **msg_iovlen** is the number of elements in the **msg_iov** array. I explained setting up these members in Section 2.15. Member **msg_flags** is ignored.

For **recvmsg**, you can set **msg_name** to **NULL** or to a buffer of length **msg_namelen** to receive the sender’s socket address, similar to the way **recvfrom** works. When **recvmsg** returns, **msg_namelen** is changed to the actual socket-address length. Members **msg_iov** and **msg_iovlen** are used as with **readv**. There’s one portable flag that can be set in the returned **msg_flags** member: **MSG_TRUNC**, which means that the message was too long to fit in the supplied buffers.

The socket-address members, **msg_name** and **msg_namelen**, are used as with connectionless sockets; for connected sockets they’re ignored.

The two other members I didn’t explain, **msg_control** and **msg_controllen**, are used for ancillary data that has to do with access rights. I won’t go into it here, but you can read about it in [SUS2002] or in your system’s documentation.

Here’s just the **run_server** function from the previous section redone to use **recvmsg** and **sendmsg**:

```
```c
static void run_server(void)
{
    int fd_skt;
    ssize_t nrecv;
    char msg[MSG_SIZE];
    struct sockaddr_storage sa;
```
```