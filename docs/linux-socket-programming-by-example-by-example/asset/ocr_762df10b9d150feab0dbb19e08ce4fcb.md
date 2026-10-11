# **DISCOVERING PROTOCOL FAMILIES**

Most of the time, the undocumented features will require that you look at some kernel source code and include files. Do not be daunted by this prospect. Many useful bits of information can be determined by looking at this code, without getting too into the details.

The protocol family macros are defined by including the file:

```
#include <sys/socket.h>
```

However, this include file actually includes another file, which then defines the protocol macro constants. The file of interest is the pathname:

```
/usr/include/bits/socket.h
```

A simple way to list all of the protocols that might have support in the kernel is to perform a simple grep command. Listing 4.1 shows how to perform this, and what the results might look like.

![](bbox=[0.04, 0.38, 0.6, 0.41])

```
$ grep PF_ /usr/include/bits/socket.h
#define PF_UNIX         0      /* Unspecified. */
#define PF_LOCAL        1      /* Local to host (pipes and file-domain). */
#define PF_UNIX         PF_LOCAL   /* Old BSD name for PF_LOCAL. */
#define PF_FILE         PF_LOCAL   /* Another non-standard name for PF_LOCAL. */
#define PF_INET         2      /* IP protocol family. */
#define PF_AX25         3      /* Amateur radio AX.25. */
#define PF_IPX          4      /* Novel11 Internet Protocol. */
#define PF_APPLETALK    5      /* AppleTalk DDP. */
#define PF_NETROM       6      /* Amateur radio NetROM. */
#define PF_BRIDGE       7      /* Multi-protocol bridge. */
#define PF_ATMPVC       8      /* ATM PVCs. */
#define PF_X25          9      /* Reserved for X.25 project. */
#define PF_INET6        10     /* IP version 6. */
#define PF_ROSE         11     /* Amateur radio X.25 PLP. */
#define PF_DECnet       12     /* Reserved for DECnet project. */
#define PF_NETBEUI      13     /* Reserved for 802.2LLC project. */
#define PF_SECURITY     14     /* Security callback pseudo AF. */
#define PF_KEY          15     /* PF_KEY key management API. */
#define PF_NETLINK      16
#define PF_ROUTE        PF_NETLINK /* Alias to emulate 4.4BSD. */
#define PF_PACKET       17     /* Packet family. */
#define PF_ASH          18     /* Ash. */
#define PF_ECONET       19     /* Acorn Econet. */
#define PF_ATMSVC       20     /* ATM SVCs. */
#define PF_SNA          22     /* Linux SNA project. */
#define PF_IRDA         23     /* IRDA sockets. */
#define PF_MAX          32     /* For now... */
#define AF_UNSPEC       PF_UNSPEC
#define AF_LOCAL        PF_LOCAL
```

![](bbox=[0.12, 0.45, 0.21, 0.5])