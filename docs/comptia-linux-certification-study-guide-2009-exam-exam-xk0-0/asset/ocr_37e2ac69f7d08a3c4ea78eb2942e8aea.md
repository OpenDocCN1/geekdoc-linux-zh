```
```
:: SERVER: 68.87.85.98#53(68.87.85.98)
:: WHEN: Thu May 14 14:59:37 2009
:: MSG SIZE  rcvd: 106
```
```

The slightly outdated command `nslookup` (superseded by the `dig` command) is still useful, in both interactive and noninteractive modes. `nslookup` enters interactive mode when no arguments are passed to it, as shown below.

```
```
$ nslookup
> www.syngress.com
Server:        68.87.85.98
Address:       68.87.85.98#53

Non-authoritative answer:
www.syngress.com    canonical name = sygpress.com.
Name:    sygpress.com
Address: 145.36.40.200
```
```

# **EXERCISE 5.3: Troubleshooting IP Address Conflicts**

On occasion, there are address conflicts within a system. To resolve this, you can do the following.

+   1.  On the system (or systems) that appear to have the IP address conflict, use the `/sbin/ifconfig` command to check the network cards and to look at the hardware and IP addresses.

+   2.  On the DHCP server, check the ARP addresses associated with the IP address and see which system it matches.

+   3.  Release and renew the IP address locally using the `dhcpcd` command
+       ```
+       dhcpcd --release
+       dhcpcd --renew
+       ```

+   4.  Check the IP address. It should now be a unique address. If there are still conflicts, a static address may have been assigned to another system. In this case, turn off your system and use traceroute from the DHCPD server to locate the rogue system.

# **Remote Access**

There are a number of methods to access a Linux system from another system, either on the local area network (LAN) or externally (often via the Internet). These accesses can be to simply retrieve data, using commands such as via a Web browser or to run a shell on the remote machine, using