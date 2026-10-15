```
struct hostent
{
    char *h_name;
    char **h_aliases;
    int h_addrtype;
    int h_length;
    char **h_addr_list
#define h_addr h_addr_list[0] /* For backward compatibility */
};
```

The meaning of each field of the structure is given in Table 20.14.

```
struct servent
```

The servent structure may be used to hold official information about a host on the Internet. It is defined in the /usr/include/netdb.h file as follows:

```
struct servent
{
    char *s_name;
    char **s_aliases;
    int s_port;
    char *s_proto;
};
```

The meaning of each field of the structure is given in Table 20.15.

# 20.6.6.2 Library Functions to Manipulate IP Addresses

UNIX provides several library functions for manipulating IP addresses from ASCII, that is, strings in dotted decimal notation (DDN) to binary and vice versa. These functions are listed in Table 20.2. Here, we briefly discuss these calls and demonstrate their use with small code snippets.

TABLE 20.14 Meaning of Each Field of the hostent Structure
| Field | Purpose |
| h_name | Official name of host |
| h_aliases | NULL-terminated array of other names of host |
| h_addrtype | Address type (family) of host, usually AF_INET (currently defined as PF_INET) |
| h_length | Length (in bytes) of address; 4 bytes for IPv4 and 16 bytes for IPv6 |
| h_addr_list | NULL-terminated array of network addresses for host |
| h_addr | Used for backward compatibility; first address in h_addr_list |