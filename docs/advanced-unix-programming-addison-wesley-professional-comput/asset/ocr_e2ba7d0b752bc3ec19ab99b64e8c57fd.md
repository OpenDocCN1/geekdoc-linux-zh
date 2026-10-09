# 8.7 Out-of-Band Data

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