# Using the endprotoent(3) Function

When your program is finished consulting with the /etc/protocols file, it can request that the implicitly opened file be closed. This is especially important for server programs to do, because file descriptors are often scarce. The function prototype for endprotoent(3) is given as follows:

```
#include <netdb.h>

void endprotoent(void);
```

There are no arguments to this function, and there are no return value or errors to check.

# Looking Up a Protocol by Name

Sometimes it is necessary for an application program or utility program, which can work with multiple protocols, to look up a protocol by name. While this can be done by using the previous functions, getprotobyname(3) saves the programmer some effort. The function prototype is as follows:

```
struct protoent *getprotobyname(const char *name);
```

The one input argument is a C string containing the protocol name (“udp”, for example). The value returned is a pointer to the protoent structure, or is a NULL pointer, indicating that it could not be found.

> **CAUTION**
> 
> The pointer returned by getprotobyname(3) is only valid until the next call to the same function.

# Looking Up a Protocol by Number

When your application has the protocol number, and it needs to display it in human readable terms, the getprotobynumber(3) routine is used. The function prototype is as follows:

```
#include <netdb.h>

struct protoent *getprotobynumber(int proto);
```

This function accepts the protocol number as the input argument, and returns the pointer to a protoent structure if a match is found. Otherwise, the NULL pointer is returned to indicate that the protocol is not known by the mini-database. For example, if the input argument is 6 (or the C macro constant IPPROTO_TCP), then you should get a structure pointer returned that has the value “tcp” in the member p_name.