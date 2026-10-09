```
#include <netdb.h>
struct hostent \*gethostname(const char \*name);
```

# Return Value

The call returns a pointer `struct hostent`; if it fails, the return value is `NULL`. The structure lists all the names and addresses the host owns. The macro `h_addr` provides backward compatibility.

```
#define h_addr h_addr_list[0]
struct hostent {
    char *h_name;          /* official name of host */
    char **h_aliases;      /* alias list */
    int h_addrtype;        /* host address type */
    int h_length;          /* length of address */
    char **h_addr_list;    /* list of addresses; 0th is the primary */
};
```

# Parameters

| name |
The hostname to search or the IP address |
| --- | --- |

# Possible Errors

| ENOTFOUND | The specified host is unknown. |
| --- | --- |
| NO_ADDRESS, NO_DATA | The requested name is valid but does not have an IP address. |
| NO_RECOVERY | A non-recoverable name server error occurred. |
| EAGAIN | A temporary error occurred on an authoritative name server. Try again later. |

# Example

```
int i;
struct hostent \*host;
host = gethostname("sunsite.unc.edu");
if ( host != NULL )
{
    printf("Official name: %s\ n", host->h_name);
    for ( i = 0; host->h_aliases[i] != 0; i++ )
        printf("    alias[%d]: %s\ n", i+1, host->h_aliases[i]);
    printf("Address type=%d\ n", host->h_addrtype);
    for ( i = 0; i < host->h_length; i++ )
        printf("Addr[%d]: %s\ n", i+1,
            inet_ntoa(host->h_addr_list[i]));
}
else
    perror("sunsite.unc.edu");
```