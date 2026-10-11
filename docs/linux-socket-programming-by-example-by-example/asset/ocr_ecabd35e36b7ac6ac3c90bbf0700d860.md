# Table 9.2: The h_errno Codes

| Error Macro | Description |
| :--- | :--- |
| HOST_NOT_FOUND | The specified hostname is unknown. |
| NO_ADDRESS | The specified hostname is valid, but does not have an IP address. |
| NO_DATA | Same as NO_ADDRESS. |
| NO_RECOVERY | A non-recoverable name server error occurred. |
| TRY_AGAIN | A temporary error occurred on the authoritative name server. Try this operation again later. |

Notice that the TRY_AGAIN error code listed in Table 9.2 represents a condition that might be overcome with retry attempts. The NO_RECOVERY error, on the other hand, represents a name server error that should not be retried, since no recovery is possible for that condition. The NO_ADDRESS (or NO_DATA) error indicates that the name that was queried is known but that there is no IP address defined for it. Finally, the error code HOST_NOT_FOUND indicates that the name queried is unknown.

# Using the gethostbyname(3) Function

This is the most important function to learn about in this chapter. This function accepts the name of the host that you want to resolve, and it returns a structure identifying it in various ways. The function synopsis is as follows:

```
#include <netdb.h>
extern int h_errno;

struct hostent *gethostbyname(const char *name);
```

The function gethostbyname(3) accepts one input argument that is a C string representing the hostname that you want to resolve into an address. The value returned is a pointer to the hostent structure if the call is successful (see Listing 9.3). If the function fails, then a NULL pointer is returned, and the value of h_errno contains the reason for the failure.

![](bbox=[0.12, 0.76, 0.21, 0.86])

# Listing 9.3: The struct hostent Structure

```
struct hostent {
    char    *h_name;    /*  official name of host  */
    char    **h_aliases;  /*  alias list  */
    int     h_addrtype;   /*  host address type  */
    int     h_length;     /*  length of address  */
    char    **h_addr_list;  /*  list of addresses  */
};

/*  for backward compatibility  */
#define h_addr  h_addr_list[0]
```