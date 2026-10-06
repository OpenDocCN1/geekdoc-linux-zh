# 25.2 Data Structures 515

(except for the actual payload that initially remains in the user address space). Otherwise, the structure is passed, as is, to the udp_sendmsg() function for sending UDP packets.

```
struct msgghdr {
    void *msg_name;
    int *msg_namelen;
    struct iovec *msg_iov;
    unsigned __kernel_size_t *msg_iovlen;
    void *msg_control;
    unsigned __kernel_size_t msg_controln;
    unsigned msg_flags;
};
include/linux/socket.h
```

For sending UDP packets, msg_name is not really a name, but a pointer to a sockaddr_in (see Section 27.1.1), which contains an IP address and a port number; msg_namelen describes the length of this structure. msg_iov pointer refers to an array of iovec structures, which reference the payload. This means that this payload can be present in a series of individual blocks, where each block denoted in an iovec structure by its initial address (iov_base) and its length (iov_len):

```
struct iovec {
    void *iov_base;
    unsigned __kernel_size_t iov_len;
};
```

The buffer specified by msg_control and msg_controln can be used to pass protocol-specific control messages. We will not discuss the format of these messages; see detailed in the recv() system call manpage.
The msg_flags element can be used to pass different flags from both the process to the kernel and in the opposite direction. The kernel evaluates the following flags:

+   - MSG_ROUTE specifies that the destination must be in the local area network and that, for this reason, the datagram should not be sent over a router to it
- MSG_DONTWAIT prevents the system call from blocking if, for example, there are no data to be received.
- MSG_ERRQUEUE means that no packet should be fetched, but instead a detailed error message, which might be available at the socket.

The following flag is an example of flags returned by the kernel to the process:

+   - MSG_TRUNC indicates that the buffer space provided for receiving was insufficient, so that some of the packet data were lost.