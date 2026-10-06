# Dynamic Host Configuration Protocol (DHCP) 569

Some releases of Red Hat Linux require you to place the dhcpcd.leases file in /etc.

Once the DHCP service starts, it stores the assignments it makes—called
leases—in the dhcpcd.leases file, which you can view by using, for example,
the more command or a text editor. Here is an example of such leases:

```
lease 192.168.1.20 (
    starts 6 2000/02/12 09:20:15;
    ends 2 2000/05/09 13:58:16;
    hardware ethernet 00:e0:98:77:08:40;
    uid 01:00:e0:98:77:08:40;
    client-hostname "OEMComputer"
)
```

```
lease 192.168.1.24 (
    starts 0 2000/03/12 18:20:23;
    ends 0 2000/03/12 18:20:23;
    hardware ethernet 00:50:56:be:01:03;
)
```

```
lease 192.168.1.23 (
    starts 6 2000/03/11 21:52:29;
    ends 6 2000/03/11 23:52:29;
    hardware ethernet 00:50:56:a0:01:03;
)
```

```
lease 192.168.1.22 (
    starts 6 2000/03/11 21:46:24;
    ends 6 2000/03/11 23:46:24;
    hardware ethernet 00:50:56:b9:01:03;
)
```

```
lease 192.168.1.21 (
    starts 6 2000/03/11 18:17:53;
    ends 6 2000/03/11 18:18:39;
    hardware ethernet 00:50:56:a7:01:03;
)
```

Leases are assigned for a finite time, specified in /etc/dhcpd.conf,
which they must be renewed by the client.
To start the configured DHCP server, issue the command

```
/etc/rc.d/init.d/dhcpd start
```