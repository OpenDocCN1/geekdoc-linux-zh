# IDE HARD DRIVE

You can also add four other IDE hard drives. They correspond to hde to hdh, and each one can have partitions 1 through 16.

```
brw-r-----    1 root       disk        33,     0 Aug 18 1995 hde
brw-r-----    1 root       disk        33,    64 Aug 18 1995 hdf
brw-r-----    1 root       disk        34,     0 Aug 18 1995 hdg
brw-r-----    1 root       disk        34,    64 Aug 18 1995 hdh
```

# NETWORKING DEVICE FILES

The following list shows device files for TCP/IP networking devices, as well as for core UNIX networking (`/dev/inet` and `/dev/unix`). ICMP (which is `/dev/icmp`) is the messaging network that TCP/IP uses (the ping command uses ICMP). The IP device (`/dev/ip`) is the addressing that TCP/IP uses. Transport can be either UDP or TCP (`/dev/udp` and `/dev/tcp` respectively).

```
crw-------    1 root       root        18,     2 Feb 18 1994 icmp
drwxr-xr-x    2 root       root      1024 May  4 14:26 inet
crw-------    1 root       root        18,     1 Feb 18 1994 ip
crw-------    1 root       root        18,     3 Feb 18 1994 tcp
crw-------    1 root       root        18,     4 Feb 18 1994 udp
crw-------    1 root       root        17,     0 Feb 18 1994 unix
```

![](bbox=[0.14, 0.61, 0.26, 0.69])

For more information on networking, see Chapter 11.

# INIT

This device file controls init, which is the root process.

```
brw-r-----    1 root       disk      1,   250 May 14 1996 initrd
```

![](bbox=[0.15, 0.87, 0.26, 0.95])

Chapter 7 explains the init process.