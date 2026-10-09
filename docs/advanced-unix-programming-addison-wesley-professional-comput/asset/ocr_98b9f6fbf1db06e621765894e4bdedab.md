```
```
struct if_nameindex—structure for network-interface functions
```

```c
struct if_nameindex {
    unsigned if_index;      /* interface index */
    char *if_name;          /* interface name */
};
```
```

Here's a function that displays the indexes and interfaces:

```
```c
static void ifdb(void)
{
    struct if_nameindex *ni;
    int i;

    ec_null( ni = if_nameindex() )
    for ( i = 0; ni[i].if_index != 0 || ni[i].if_name != NULL; i++)
        printf("index: %d; name: %s\n", ni[i].if_index, ni[i].if_name);
    if_freenameindex(ni);
    return;

EC_CLEANUP_BGN
    EC_FLUSH("ifdb")
EC_CLEANUP_END
}
```
```

The output on Solaris was:

```
```
index: 1; name: lo0
index: 2; name: iprb0
```
```

and on SuSE Linux:

```
```
index: 1; name: lo
index: 2; name: eth0
```
```

These sort of match up with the network names displayed by the functions in Section 8.8.2: a loopback interface, and an Internet interface using Ethernet.

There’s another function to map a name to its index:

```
```
if_nameetoindex—map network interface name to index
```

```c
#include <net/if.h>
unsigned if_nameetoindex(
    const char *ifname   /* interface name */
);
/* Returns index or 0 on error (errno not defined) */
```
```