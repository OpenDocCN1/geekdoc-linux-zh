The cmd value F_SETOWN allows ownership of the socket to be established, for the process ID given in arg.

# ## **ioctl(2)** to Test for Mark

```
```
#include <sys/ioctl.h>
int z;   /* Status */
int s;   /* Socket */
int flag; /* True when at mark */

z = ioctl(s, SIOCGETMARK, &flag);
if ( z == -1 )
    abort();           /* Error */
if ( flag ! = 0 )
    puts("At Mark");
else
    puts("Not at mark.");
```
```

# ## Network Support Functions

# ### **byteorder(3)**

```
```
#include <netinet/in.h>
unsigned long htonl(unsigned long hostlong);
unsigned short htons(unsigned short hostshort);
unsigned long ntohl(unsigned long netlong);
unsigned short ntohs(unsigned short netshort);
```
```

# ### **inet_addr(3)**

```
```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
unsigned long inet_addr(const char *string);
```
```

# ### **inet_aton(3)**

```
```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
int inet_aton(const char *string, struct in_addr *addr);
```
```