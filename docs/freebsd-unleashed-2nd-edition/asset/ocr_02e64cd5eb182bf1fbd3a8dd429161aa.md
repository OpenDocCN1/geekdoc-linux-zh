# ## Mapping Names to IP Addresses with the /etc/hosts File

We need a way for hostnames to map to IP addresses. Normally, this is done with DNS, but we don’t have DNS set up yet. In the meantime, we can provide mappings for hosts we know about—such as hosts on our local network—with the `/etc/hosts` file.

`/etc/hosts` allows you to build a table in which each entry lists an IP address, its most common (or “official”) hostname, and any aliases (additional names that map to the same IP address). Each of these items is separated by spaces or tabs. This table is consulted before any DNS queries are made, so `/etc/hosts` acts both as a backup to DNS (if it’s not available) and an override (if it’s not serving correct information). The aliases can even be used as a shorthand for favorite hosts whose names you don’t want to have to remember, as with shell aliases (which we discussed in the “Shell Initialization Files” section of Chapter 11, “Customizing the Shell”).

Here are a few sample lines from `/etc/hosts`:

```
64.41.131.132          ns          ns.somewhere.com     lion.somewhere.com
64.41.131.133          www2        www2.somewhere.com
64.41.132.165          www3        www3.somewhere.com
114.235.123.11         www.foobar.com fred
```

With this table in place, you can connect to the listed hosts by name—either the “official” name in the second column or any of the aliases listed in the third column—even if no DNS servers can be reached.

# ## Testing Network Connectivity with ping

After you’ve finished your network configurations, setting them either with sysinstall or with `/etc/netstart`, you can use `ping` to make sure the settings are correct. The `ping` program is a simple ICMP-based tool that checks for echoes from a specified host and reports the roundtrip time it takes each packet to get to the host and back.

The use of `ping` is pretty simple. You can run it against either an IP address or a hostname (or `/etc/hosts` alias), and it will run until you interrupt it with Ctrl+C:

```
# ping fred
PING fred (114.235.123.11): 56 data bytes
64 bytes from 114.235.123.11: icmp_seq=0 ttl=243 time=485.344 ms
64 bytes from 114.235.123.11: icmp_seq=1 ttl=243 time=351.589 ms
^C
--- fred ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max/stddev = 351.589/418.466/485.344/66.877 ms
```