**endprotoent**—end protocol-database scan

```C
#include <netdb.h>
void endprotoent(void);
```

**struct protoent**—structure for protocol-database functions

```C
struct protoent {
    char  *p_name;         /* official protocol name */
    char **p_aliases;      /* array of alternative protocol names */
    int   p_proto;         /* protocol number */
};
```

On some systems, you can use a protocol number for a protocol level when you call `setsockopt` or `getsockopt`, but that’s nonstandard.

The example code is pretty obvious if you’ve been reading along:

```
```C
static void protodb(void)
{
    struct protoent  *p;

    setprotoent(true);
    while ((p = getprotoent()) != NULL)
        display_protoent(p);
    endprotoent();
}

static void display_protoent(struct protoent *p)
{
    int i;

    printf("name: %s; number: %d\n", p->p_name, p->p_proto);
    for (i = 0; p->p_aliases[i] != NULL; i++)
        printf("\t%s\n", p->p_aliases[i]);
}
```
```

But the output is pretty interesting. On SuSE Linux I got 135 protocols. Here’s just part of the output:

```
```
...  
name: mobile; number: 55
       MOBILE
name: tlsp; number: 56
       TLSP
name: sktp; number: 57
       SKIP
name: ipv6-icmp; number: 58
       IPv6-ICMP
```
```