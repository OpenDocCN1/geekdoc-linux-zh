# **CAUTION**

Always use the macro names, such as `MSG_DONTWAIT` for example, when specifying constants and flag bits. While Table 6.1 shows the hexadecimal values for each C macro constant, only use the macro name. In this manner, if a change to the constant should be made in a later release of Linux, your program can simply be recompiled and still function correctly without any source code modification.

# **TIP**

The man page for `sendto(2)` for Red Hat Linux 6.0 lists the value of C macro constant `MSG_NOSIGNAL` as `0x2000`. However, the `include/linux/socket.h` file within the kernel sources for 2.2.10 lists the value as `0x4000`. A comment in this include file also indicates that not all of the flags listed there are supported yet.

Many of the flag values listed in Table 6.1 are for advanced use and won't be covered at this time. They have been listed here for your convenience as a reference. Normally, you will simply supply the value zero.

Later in this chapter, you will put the `sendto(2)` function to work. Before you do this, however, you should learn about the `recvfrom(2)` function.

# ## Introducing the `recvfrom(2)` Function

The companion to the `sendto(2)` function is the `recvfrom(2)` function. This function differs from the `read(2)` function in that it allows you to receive the sender's address at the same time you receive your datagram. The function synopsis is as follows:

```
`#include <sys/types.h>
#include <sys/socket.h>`
```

```
`int recvfrom(int s, 
            void *buf, 
            int len, 
            unsigned flags, 
            struct sockaddr *from, 
            int *fromlen);`
```

The list of arguments is very similar to those used in the `sendto(2)` function. The `recvfrom(2)` arguments are

+   1. The socket `s` to receive the datagram from.
+   2. The buffer pointer `buf` to start receiving the datagram into.
+   3. The maximum length (`len`) in bytes of the receiving buffer `buf`.
+   4. Option flag bits `flags`.
+   5. The pointer to the receiving socket address buffer, which will receive the sender's address (pointer argument `from`).