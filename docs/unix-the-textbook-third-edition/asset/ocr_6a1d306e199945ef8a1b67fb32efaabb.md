# TABLE 20.15 Meaning of Each Field of the servent Structure

| Field | Purpose |
|---|---|
| h_name | Official name of host |
| h_aliases | NULL-terminated array of other names of host |
| h_addrtype | Address type (family) of host, usually AF_INET (currently defined as PF_INET) |
| h_length | Length (in bytes) of address: 4 bytes for IPv4 and 16 bytes for IPv6 |
| h_addr_list | NULL-terminated array of network addresses for host |
| h_addr | Used for backward compatibility; first address in h_addr_list |

A brief description of the inet_aton() call is given next. Note that it works for address domains PF_INET and PF_INET6.

```
#include <netinet/in.h>
#include <arpa/inet.h>
int inet_aton(const char *cp, struct in_addr *pin);
Success: 1
Failure: 0 if address string is invalid
```

This function call converts the IP address in DDN specified as string cp to the IP address in network byte order and stores it in the structure specified as pin. The following code snippet shows sample use of this function.

```
#include <netinet/in.h>
#include <arpa/inet.h>
...
int n;
struct in_addr address;
...
memset(&address, '\0', sizeof(address));
n = inet_aton("39.59.169.110", &address);
if (n == 0) {
    /* Error handling code */
}
...
```

The inet_addr() call converts and returns the specified string for an IP address in DDN to a 32-bit unsigned binary value in network byte order. Here is a brief description of the call.

```
#include <sys/types.h>
#include <arpa/inet.h>
in_addr_t inet_addr(const char *cp);
Success: IP address in Network Byte Order
Failure: INADDR_NONE
```