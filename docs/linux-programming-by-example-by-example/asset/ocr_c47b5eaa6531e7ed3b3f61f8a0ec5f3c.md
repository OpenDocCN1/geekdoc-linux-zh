Fortunately, the TCP/IP protocol family includes the *Domain Name System* (DNS), a distributed database that, among other things, maps names, like `www.netscape.com`, to IP addresses, in this case, `205.188.247.73`. Although DNS encompasses many capabilities, the one covered here is how to convert a hostname to an address and vice versa. You must know about one structure, `struct hostent`, and two functions, `gethostbyname` and `gethostbyaddr`. They are declared in `<netdb.h>` as follows:

```
```
struct hostent {  
  char *h_name;                 /* Canonical machine name */
  char **h_aliases;            /* List of aliases */
  int h_addrtype;              /* AF_INET */
  int h_length;                /* sizeof(struct in_addr) */
  char **h_addr_list;          /* List of IP addresses */
};  
struct hostent *gethostbyname(const char *name);  
struct hostent *gethostbyaddr(const char *addr, int len, int type);
```
```

`gethostbyname` takes a hostname `name`, such as `ftp.netscape.com`, and returns a pointer to a `hostent` structure that contains the relevant information from the DNS. Similarly, `gethostbyaddr` takes an address structure, `struct in_addr` (which you have already seen), stored in `addr`, its length, stored in `len`, and its `type`, which is always `AF_INET`, and returns a pointer to a `hostent` structure. The pointer that both calls return points to a statically allocated buffer that is overwritten each time you call either function. So, if you need to save any of the information in the `hostent` structure pointer, save it in local variables.

Regarding the `hostent` structure itself, `h_name` is the canonical, or "official" (as in registered) machine name, `h_addrtype` is always `AF_INET`, and `h_length` is the size of address structure, which is `sizeof (struct in_addr)` at this time. `h_aliases` and `h_addr_list`, respectively, are pointers to strings containing all the names and IP addresses that a machine can have.

"Now wait a minute!" I hear you thinking. "Whyddya mean, 'all of the names and IP addresses that a machine can have?'" Simply put, the DNS is not a one-to-one mapping of hostnames to IP addresses. There are many reasons why a machine might have multiple IP addresses or multiple hostnames. In the case of multiple IP addresses, consider a *router*, a system that has multiple network cards. Each card has a different IP address to route incoming packets to the appropriate location, such as different networks or different systems.