# close()

Closes all descriptors (file or socket). If the socket is connected to a server or client, it requests a close(). The channel actually remains active after the close until the channel empties or times out. Every process has a limit to the number of open descriptors it can have.

getdtablesize() returns 1024 in Linux 2.2.14, and the /usr/include/linux/limits.h file defines this limit with NR_OPEN. Also, the first three descriptors default to stdin (0), stdout (1), and stderr (2).

# Prototype

```
#include <unistd.h>
int close(int fd);
```

# Return Value

Zero if everything goes well. If an error occurs, you can find the cause in errno.

# Parameter

+   - fd: The file or socket descriptor

# Possible Error

+   - EBADF: fd isn't a valid open file descriptor.

# Example

```
int sockfd;
sockfd = socket(PF_INET, SOCK_RAW, htons(99));
if ( sockfd < 0 )
PANIC("Raw socket create failed");
...
if ( close(sockfd) != 0 )
PANIC("Raw socket close failed");
```