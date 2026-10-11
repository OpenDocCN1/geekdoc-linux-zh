### Return value
The call returns the parameter *str*.

### Parameters
| Parameter | Description |
| :--- | :--- |
| *domain* | The network type (*AF_INET* or *AF_INET6*) |
| *addr* | The binary address (typically the address field of *struct sockaddr_in*) |
| *str* | The string buffer |
| *len* | The number of bytes available in *str* |

### Possible Errors
(*errno* not set)

### Example

```
```
char str[100];
clientfd = accept(serverfd, &addr, &addr_size);
if ( clientfd > 0 )
  printf("Connected %s:%d\n",
         inet_ntop(AF_INET, &addr.sin_addr, str, sizeof(str)),
         ntohs(addr.sin_port));
```
```

# # Network Addressing Tools

Like the data and addressing tools, the API gives you access to the naming services. These services include domain name services (DNS), the protocols, and so on. This section describes the calls for converting human-readable names.

# ## *getpeername*()

This routine gets the bound address or name of connected peer at the other end of the *sockfd* channel. The call places the results in *buf*. The *buf_len* is the number of bytes available in *buf*. If too small, the information gets truncated. This is the same information you get with the *accept*() call.

### Prototype

```
```
#include <sys/socket.h>
int getpeername(int sockfd, struct sockaddr *addr,
                socklen_t *addr_len);
```
```

### Return Value
Zero if everything goes well. If an error occurs, you can find the cause in *errno*.