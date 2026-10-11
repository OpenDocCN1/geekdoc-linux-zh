**Example**
```
if ( (addr.sin_addr.s_addr = inet_addr("128.187.34.2")) == -1 )
    perror("Couldn't convert address");
```

# **inet_aton()**

Converts a human-readable IP address from the dot-notation to the binary, network-byte ordered form. This call replaces `inet_addr()`.

# ## Prototype

```
```c
#include <netinet/in.h>
int inet_aton(const char* ip_addr, struct in_addr *addr);
```
```

# ## Return Value

Non-zero if everything goes well. If an error occurs, the call returns a zero.

# ## Parameters

+   * **`ip_addr`** The ASCII string of the IP address (for example, 187.34.2.1).
+   * **`addr`** The destination. Typically, you would populate the `sin_addr` field from the `sockaddr_in` structure.

# ## Possible Errors

(errno not set)

# **Example**

```
```c
Struct sockaddr_in addr;
if ( inet_aton("187.43.32.1", &addr.sin_addr) == 0 )
    perror("inet_aton() failed");
```
```

# **inet_ntoa()**

This call converts the network-byte order binary to a human-readable form. Note that this call uses a static memory region; subsequent calls overwrite the older results.

# ## Prototype

```
```c
#include <netinet/in.h>
const char* inet_ntoa(struct in_addr *addr);
```
```

# ## Return Value

The address is in the returned string.

# ## Parameters

+   * **`addr`** The binary address (typically the address field of struct `sockaddr_in`)