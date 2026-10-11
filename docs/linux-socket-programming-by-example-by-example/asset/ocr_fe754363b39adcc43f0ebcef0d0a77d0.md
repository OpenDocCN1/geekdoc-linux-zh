# DISCOVERING SOCKET TYPES

Knowing about the protocol families is part of the battle when attempting to create an exotic socket. You now need to know about the socket types that are supported by the protocol family that you have selected. This can usually be done using the following simple procedure:

+   1. Change to the Linux kernel source directory (you might need to install it first). For example, this might require you to do `cd /usr/linux/src`.
+   2. Change to the Linux network source code subdirectory. For example, you would do `cd ../net` in order to change to that subdirectory.
+   3. List the directory with the command `ls -F`. This will cause the subdirectories to be shown with a trailing `/` (slash) after them.
+   4. Usually, the subdirectory name is indicative of the protocol in which you might be interested. Change to that subdirectory (for example, `cd ipx`).
+   5. Perform a grep command for anything starting with `SOCK_`.

Usually, this is sufficient to list the socket types that you want to know about. Listing 4.2 shows an example session, following these steps.

```
**Listing 4.2: Listing the Supported Socket Types for a Protocol Family**
```
$ cd /usr/src/linux
$ cd ../net
$ ls -F
802/
Changes
Config.in
Makefile
README
TUNABLE
appletalk/
a25/
bridge/
core/

decnet/
eternet/
ip/
ipx/
irda/
lppb/
netlink/
netrom/

netsyms.c
netsyms.o
network.a
packet/
protocols.o
protocols.c
rose/
sched/
sock_n_syms.o
socket.c

socket.o
sunrpc/
sysctl_net.c
sysctl_net.o
unix/
wancuter/
x25/
```
$ cd ipx
$ ls -F
Config.in af_ipx.c sysctl_net_ipx.c
Makefile af_spx.c
$ grep SOCK _ .c
af_ipx.c: s->state, SOCK_INODE(s)->socket)->_i_uid);
af_ipx.c: case SOCK_DGRAM:
af_ipx.c: case SOCK_SEQPACKET:
af_spx.c: case SOCK_STREAM: /* Allow higher levels to piggyback */
af_spx.c: if(sock->type == SOCK_DGRAM)
af_spx.c: SOCK_DEBUG(sk,)
```