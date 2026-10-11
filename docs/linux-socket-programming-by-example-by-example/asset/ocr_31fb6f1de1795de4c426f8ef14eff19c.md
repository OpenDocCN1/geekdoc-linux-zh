```
int len,
unsigned flags,
const struct sockaddr *to,
int tolen);
```

Don't let the number of arguments intimidate you about this function. They are quite easy to understand, after they are described:

+   1.  The first argument s is the socket number. You received this value from the socket(2) function.
+   2.  Argument msg is a pointer to the buffer holding the datagram message that you wish to send.
+   3.  Argument len is the length, in bytes, of the datagram that starts at the pointer given by msg.
+   4.  The flags argument allows you to specify some option bits. In many cases, you will simply supply a value of zero.
+   5.  The argument to is a pointer to a generic socket address that you have established. This is the address of the recipient of the datagram.
+   6.  Argument tolen is the length of the address argument to.

The value returned by the function sendto(2), when successful, is the number of bytes sent (note that this is no guarantee that they were received at the remote end.) When an error occurs, the function returns a value of -1 and the value errno can be consulted to find out why.

The second-to-last function argument allows you to identify where the datagram must be sent. The argument to must point to a valid socket address, and the argument tolen should contain the correct length of the address. You have become an expert at forming addresses in the preceding chapters, so you should feel right at home here.

Table 6.1 lists the values that the flags argument can have, though most of the time you will simply supply the value zero instead.

# Table 6.1: The flags Values for the sendto(2) Function

| Flag | Hexadecimal | Meaning |
| :--- | :--- | :--- |
| 0 | 0x0000 | Normal—no special options |
| MSG_OOB | 0x0001 | Processes out-of-band data |
| MSG_DONTROUTE | 0x0004 | Bypasses routing; uses direct interface |
| MSG_DONTWAIT | 0x0040 | Does not block; waiting to write |
| MSG_NOSIGNAL | 0x4000 | Does not raise SIGPIPE when the other end has disconnected |