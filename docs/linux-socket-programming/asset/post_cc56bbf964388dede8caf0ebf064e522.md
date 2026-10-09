
## inet_aton()

`addr`
The destination. Typically, you would populate the `sin_addr` field from the `sockaddr_in` structure.

### Possible Errors

(`errno` not set)

### Example

```c
struct sockaddr_in addr;
if ( inet_aton("187.43.32.1", &addr.sin_addr) == 0 )
    perror("inet_aton() failed");
```

## inet_ntoa()

This call converts the network-byte order binary to a human-readable form. Note that this call uses a static memory region; subsequent calls overwrite the older results.

### Prototype

```c
#include <netinet/in.h>
const char* inet_ntoa(struct in_addr *addr);
```

### Return Value

The address is in the returned string.

### Parameters

`addr`
The binary address (typically the address field of `struct sockaddr_in`).

### Possible Errors

(`errno` not set)

### Example

```c
clientfd = accept(serverfd, &addr, &addr_size);
if ( clientfd > 0 )
    printf("Connected %s:%d\n",
        inet_ntoa(addr.sin_addr), ntohs(addr.sin_port));
```

## inet_pton()

Converts a human-readable IPv4 or IPv6 address from the dot/colon-notation to the binary, network-byte ordered form.

### Prototype

```c
#include <netinet/in.h>
int inet_pton(int domain, const char* psrcnt, void *addr);
```

### Return Value

Non-zero if everything goes well. If an error occurs, the call returns zero.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `domain` | The network type (`AF_INET` or `AF_INET6`). |
| `psrcnt` | The ASCII string of the IP address (for example, `187.34.2.1` or `FFFF::B090:A03:3245`). |
| `addr` | The destination. Typically, you would populate the `sin_addr` field from the `sockaddr_in` structure or `sin6_addr` field from the `sockaddr_in6` structure. |

### Possible Errors

(`errno` not set)

### Example

```c
struct sockaddr_in addr;
if ( inet_pton(AF_INET6, "187.43.32.1", &addr.sin6_addr) == 0 )
    perror("inet_pton() failed");
```

## inet_ntop()

This call converts the network-byte order binary to a human-readable form. Unlike the `inet_ntoa`, you need to supply it a scratchpad string. This function supports both `AF_INET` and `AF_INET6`.

### Prototype

```c
#include <arpa/inet.h>
char* inet_ntop(int domain, struct in_addr *addr, char* str, int len);
```

### Return Value

The call returns the parameter `str`.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `domain` | The network type (`AF_INET` or `AF_INET6`) |
| `addr` | The binary address (typically the address field of `struct sockaddr_in`) |
| `str` | The string buffer |
| `len` | The number of bytes available in `str` |

### Possible Errors

(`errno` not set)

### Example

```c
char str[100];
clientfd = accept(serverfd, &addr, &addr_size);
if ( clientfd > 0 )
    printf("Connected %s:%d\n",
        inet_ntop(AF_INET, addr.sin_addr, str, sizeof(str)),
        ntohs(addr.sin_port));
```

# Network Addressing Tools

Like the data and addressing tools, the API gives you access to the naming services. These services include domain name services (DNS), the protocols, and so on. This section describes the calls for converting human-readable names.

## getpeername()

This routine gets the bound address or name of the connected peer at the other end of the `sockfd` channel. The call places the results in `buf`. The `buf_len` is the number of bytes available in `buf`. If too small, the information gets truncated. This is the same information you get with the `accept()` call.

### Prototype

```c
#include <sys/socket.h>
int getpeername(int sockfd, struct sockaddr *addr,
socklen_t *addr_len);
```

### Return Value

Zero if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The connected socket channel. |
| `addr` | A buffer that holds the address structure. |
| `addr_len` | The number of bytes available in `addr`. This is passed by reference (the call changes this field). |

### Possible Errors

| Error | Description |
| :--- | :--- |
| `EBADF` | The argument `sockfd` is not a valid descriptor. |
| `ENOTSOCK` | The argument `sockfd` is a file, not a socket. |
| `ENOTCONN` | The socket is not connected. |
| `ENOBUFS` | Insufficient resources were available in the system to perform the operation. |
| `EFAULT` | The `addr` parameter points to memory that is not in a valid part of the process address space. |

### Example

```c
struct sockaddr in_addr;
int addr_len = sizeof(addr);
if ( getpeername(client, &addr, &addr_len) != 0 )
    perror("getpeername() failed");
printf("Peer: %s:%d\n", inet_ntoa(addr.sin_addr),
    ntohs(addr.sin_port));
```

## gethostname()

Gets the localhost's name. The call places the result in the `name` parameter up to `len` bytes.

### Prototype

```c
#include <unistd.h>
int gethostname(char *name, size_t len);
```

### Return Value

Zero if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `name` | The buffer to accept the name of the localhost |
| `len` | The number of bytes available in `name` |

### Possible Errors

| Error | Description |
| :--- | :--- |
| `EINVAL` | `len` is negative or, for `gethostname()` on Linux/i386, `len` is smaller than the actual size. |
| `EFAULT` | `name` is an invalid address. |

### Example

```c
char name[50];
if ( gethostname(name, sizeof(name)) != 0 )
    perror("gethostname() failed");
printf("My host is: %s\n", name);
```

## gethostbyname()

Search for and translate the hostname to an IP address. The `name` can be a hostname or an address. If it is an address, the call does no searches; instead, it returns the address in the `h_name` and `h_addr_list[0]` fields of the `hostent` structure.

If the hostname ends with a period, the call treats the name as an absolute name with no abbreviation. Otherwise, the call searches the local subnetwork names. If you have `HOSTALIASES` defined in your environment, the call searches the file to which `HOSTALIASES` points.

### Prototype

```c
#include <netdb.h>
struct hostent *gethostbyname(const char *name);
```

### Return Value

The call returns a pointer to `struct hostent`; if it fails, the return value is `NULL`. The structure lists all the names and addresses the host owns. The macro `h_addr` provides backward compatibility.

```c
#define h_addr h_addr_list[0]
struct hostent {
    char *h_name;          /* official name of host */
    char **h_aliases;      /* alias list */
    int h_addrtype;        /* host address type */
    int h_length;          /* length of address */
    char **h_addr_list;    /* list of addresses; 0th is the primary */
};
```

### Parameters

| Parameter | Description |
| :--- | :--- |
| `name` | The hostname to search or the IP address |

### Possible Errors

| Error | Description |
| :--- | :--- |
| `ENOTFOUND` | The specified host is unknown. |
| `NO_ADDRESS`, `NO_DATA` | The requested name is valid but does not have an IP address. |
| `NO_RECOVERY` | A non-recoverable name server error occurred. |
| `EAGAIN` | A temporary error occurred on an authoritative name server. Try again later. |

### Example

```c
int i;
struct hostent *host;
host = gethostbyname("sunsite.unc.edu");
if ( host != NULL )
{
    printf("Official name: %s\n", host->h_name);
    for ( i = 0; host->h_aliases[i] != 0; i++ )
        printf("    alias[%d]: %s\n", i+1, host->h_aliases[i]);
    printf("Address type=%d\n", host->h_addrtype);
    for ( i = 0; i < host->h_length; i++ )
        printf("Addr[%d]: %s\n", i+1,
            inet_ntoa(host->h_addr_list[i]));
}
else
    perror("sunsite.unc.edu");
```

## getprotobymname()

This function reads the `/etc/protocol` file to get the protocol that matches `pname`. You use this call to translate names such as HTTP, FTP, and Telnet into their default port numbers.

### Prototype

```c
#include <netdb.h>
struct protoent *getprotobymname(const char *pname);
```

### Return Value

The call returns a pointer to `protoent` (defined later in this appendix) if successful. Otherwise, it returns `NULL`.

```c
struct protoent {
        char    *p_name;        /* official protocol name */
        char    **p_aliases;    /* alias list */
        int     p_proto;        /* protocol number */
} ;
```

The field `p_proto` is the port number.

### Parameters

`pname`
Protocol name. This can be any of the recognized protocol names or aliases.

### Possible Errors

(`errno` not set)

### Example

```c
#include <netdb.h>
...
int i;
struct protoent *proto = getprotobymname("http");
if ( proto != NULL )
{
        printf("Official name: %s\n", proto->p_name);
        printf("Port#: %d\n", proto->p_proto);
        for ( i = 0; proto->p_aliases[i] != 0; i++ )
                printf("Aliases[%d]: %s\n", i+1,
                        proto->p_aliases[i]);
}
else
        perror("http");
```
