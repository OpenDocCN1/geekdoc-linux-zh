
## 20.6.6.2 Library Functions to Manipulate IP Addresses

```c
struct hostent
{
    char *h_name;
    char **h_aliases;
    int h_addrtype;
    int h_length;
    char **h_addr_list;
#define h_addr h_addr_list[0] /* For backward compatibility */
};
```

The meaning of each field of the structure is given in Table 20.14.

**TABLE 20.14 Meaning of Each Field of the hostent Structure**

| Field | Purpose |
| --- | --- |
| h_name | Official name of host |
| h_aliases | NULL-terminated array of other names of host |
| h_addrtype | Address type (family) of host, usually AF_INET (currently defined as PF_INET) |
| h_length | Length (in bytes) of address; 4 bytes for IPv4 and 16 bytes for IPv6 |
| h_addr_list | NULL-terminated array of network addresses for host |
| h_addr | Used for backward compatibility; first address in h_addr_list |

### struct servent

The servent structure may be used to hold official information about a service on the Internet. It is defined in the /usr/include/netdb.h file as follows:

```c
struct servent
{
    char *s_name;
    char **s_aliases;
    int s_port;
    char *s_proto;
};
```

The meaning of each field of the structure is given in Table 20.15.

**TABLE 20.15 Meaning of Each Field of the servent Structure**

| Field | Purpose |
| --- | --- |
| s_name | Official name of service |
| s_aliases | NULL-terminated array of alternate names for the service |
| s_port | Port number for the service in network byte order |
| s_proto | Protocol used by the service |

A brief description of the inet_aton() call is given next. Note that it works for address domains PF_INET and PF_INET6.

```c
#include <netinet/in.h>
#include <arpa/inet.h>
int inet_aton(const char *cp, struct in_addr *pin);
Success: 1
Failure: 0 if address string is invalid
```

This function call converts the IP address in DDN specified as string cp to the IP address in network byte order and stores it in the structure specified as pin. The following code snippet shows sample use of this function.

```c
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

```c
#include <sys/types.h>
#include <arpa/inet.h>
in_addr_t inet_addr(const char *cp);
Success: IP address in Network Byte Order
Failure: INADDR_NONE
```

The return type of the function, in_addr_t, is defined as a 32-bit unsigned integer in the /usr/include/sys/types.h file. In the following code segment, we show a sample use of this call.

```c
#include <sys/types.h>
#include <arpa/inet.h>
...
struct sockaddr_in address;
...
memset(&address, '\0', sizeof(address));
if ((address.sin_addr.s_addr = inet_addr("39.59.169.110")) == INADDR_NONE) {
    /* Error handling code */
}
...
```

The call returns INADDR_NONE on failure. This symbolic constant is defined in /usr/include/netinet/in.h as all 1s (i.e., 0xffffffff). This means that this return value is -1.

The inet_ntoa() call converts and returns an IP address in network byte order binary form to the string of corresponding IP address in DDN. Here is a brief description of the call.

```c
#include <sys/types.h>
#include <arpa/inet.h>
char * inet_ntoa(struct in_addr in);
Success: IP address string in DDN
Failure: NULL
```

The following piece of code shows a sample use of the call.

```c
#include <netinet/in.h>
#include <arpa/inet.h>
...
char *ip_ddn;
struct in_addr address;
...
ip_ddn = inet_ntoa(address);
printf("IP Address is: %s\n",ip_ddn);
...
```

## 20.6.6.3 New Library Functions to Manipulate IP Addresses

The inet_addr() function received criticism and new programs used inet_aton() instead. The new versions of inet_ntoa() and inet_aton() that work with both IPv4 and IPv6 addresses are inet_ntop() and inet_pton(), respectively. Note that "n" stands for numeric and "p" for presentation. You should use the new calls in your code even if your system does not support IPv6.
