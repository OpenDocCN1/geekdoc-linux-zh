The return value from this function is the number of bytes sent. Otherwise, -1 indicates an error occurred and **errno** indicates the reason for it.

# The **recvmsg(2)** Function

The **recvmsg(2)** function is the natural counterpart to the **sendmsg(2)** function. The function prototype for it is as follows:

![](bbox=[0.08, 0.22, 0.17, 0.33])

```
#include <sys/types.h>
#include <sys/socket.h>

int recvmsg(int s, struct msghdr *msg, unsigned int flags);
```

The function arguments are as follows:

+   • The socket *s* to receive a message from.
+   
+   • The message header structure pointer *msg*, which will control the operation of this function call.
+   
+   • The optional *flag bits* argument *flags*. These are the same flags that are valid for **recv(2)** or **recvfrom(2)** function calls.

The return value from this function is the number of bytes received. Otherwise, -1 indicates an error occurred and **errno** indicates the reason for it.

# Understanding **struct msgdr**

This appears to be a formidable structure to establish when seeing it for the first time. But don’t fear the penguins! Examine the following structure definition:

![](bbox=[0.08, 0.63, 0.17, 0.74])

```
struct msghdr {
    void      *msg_name;
    socklen_t  msg_namelen;
    struct iovec *msg_iov;
    size_t     msg_iovlen;
    void      *msg_control;
    size_t     msg_controllen;
    int        msg_flags;
};
```

# NOTE

Prior to the **Posix.1g** standard, the **msg_name** and **msg_control** members were typically defined as C data type **(char \*)**. Additionally, members **msg_namelen** and **msg_controllen** were previously declared as **int** types.