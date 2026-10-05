# TCP/IP and Linux Protocol Implementation

```
#if i
    printk(KERN_CRIT "impossible 888\n");
#endif
    return;
}
```

# FIB Proc FS

As well as RTNetlink, we also have the proc fs interface to modules:

FIB 8.58 FIB semantics—PROC FS interface: linux/net/ipv4/fib_semantics.c.

```
static unsigned fib_flag_trans(int type, int dead, u32 mask, struct fib_info *fi)
{
    static unsigned type2[RT_MAX+1] = {
        0, 0, 0, 0, 0, 0, 0, RT_REJECT, RT_REJECT, 0, 0, 0
    };
    unsigned flags = type2[type];

    if (fi && fi->fib_nh->gw)
        flags |= RT_GATEWAY;
    if (mask == 0xFFFFFFFF)
        flags |= RT_HOST;
    if (dead)
        flags |= RT_UP;
    return flags;
}

void fib_node_get_info(int type, int dead, struct fib_info *fi, u32 prefix, u32 mask, char *buffer)
{
    int len;
    unsigned flags = fib_flag_trans(type, dead, mask, fi);

    if (fi) {
        len = sprintf(buffer, "%08X\t%08X\t%04X\t%u\t%08X\t%u\t%u\t%u",
            fi->fib_dev, 7->fi->fib_dev, " :%s", prefix,
            fi->fib_nh->gw, flags, 0, 0, fi->fib_priority,
            mask, fi->fib_advmss+40, fi->fib_window, fi->fib_rtt>>3);
    } else {
        len = sprintf(buffer, "%08X\t%08X\t%04X\t%u\t%08X\t%u\t%u\t%u",
            prefix, 0,
            flags, 0, 0,
            mask, 0, 0);
    }
    memset(buffer+len, ' ', 127-len);
    buffer[127] = '\n';
}}
```