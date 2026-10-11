# Understanding the Signal SIGURG

The receiving process needs to be notified when out-of-band data has arrived. This is particularly true if it must be read separately from the normal data stream. One such method for doing this is to have the Linux kernel send your process the SIGURG signal when out-of-band data has arrived.

There are two requirements for using SIGURG signal notification:

+   - You must establish ownership of the socket.
+   - You must establish a signal handler for SIGURG.

To receive the SIGURG signal, you must establish your process (or process group) as the owner of the socket. To establish this ownership, you use the `fcntl(2)` function. Its function prototype as it applies to us here is as follows:

```
```
#include <unistd.h>
#include <fcntl.h>

int fcntl(int fd, int cmd, long arg);
```
```

The arguments for this function are as follows:

+   1. The file descriptor `fd` (or socket) to apply a control function to.
+   2. The control function `cmd` to apply.
+   3. The value `arg` to set (if any).

The return value depends upon the control function being exercised by `fcntl(2)`. The Linux man page for `fcntl(2)` describes the `cmd` operation `F_SETOWN` in some detail, for those who are interested in additional reading.

To establish your process (or process group) as the owner of a socket, the receiving program could use the following code:

![](bbox=[0.08, 0.7, 0.16, 0.82])

```
```
int z;  /* Status */
int s;  /* Socket */

z = fcntl(s,F_SETOWN,getpid());

if ( z == -1 ) {
    perror(*fcntl(2)*);
    exit(1);
}
```
```

The `F_SETOWN` operation causes the `fcntl(2)` function to return zero if successful, or −1 if it fails (*errno indicates the cause of the failure* ).