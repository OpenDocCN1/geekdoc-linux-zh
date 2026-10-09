for an extremely tiny measure of added security. If you're not sure whether you're using them, ask your network administrator.

```
icmp_drop_redirect="NO"
```

If you *are* the network administrator and you're not sure whether your network uses ICMP redirects, there's an easy way to find out—just log all redirects received by your system to `/var/log/messages`.$^{3}$ Note that if your server is under attack, this can fill your hard drive with redirect logs fairly quickly.

```
icmp_log_redirect="NO"
```

To get on the network, you'll need to assign each interface an IP address. We'll discuss this in some detail in Chapter 8. You can get a list of your network interfaces with the `ifconfig(8)` command. List each network interface on its own line, with its network configuration information in quotes. For example, to give your em0 network card an IP address of 172.18.11.3 and a netmask of 255.255.254.0, you would use:

```
ifconfig_em0="inet 172.18.11.3 netmask 255.255.254.0"
```

If your network uses DHCP, use the value `dhcp` as an IP address.

```
ifconfig_em0="dhcp"
```

Similarly, you can assign aliases to a network card. An alias is not the card's actual IP address, but the card answers for that IP address, as discussed in Chapter 8. FreeBSD supports hundreds of aliases on a single card, with `rc.conf` entries in the following form:

```
ifconfig_em0_alias#="address netmask 255.255.255.255"
```

The alias numbers must be continuous, starting with 0. If there's a break in numbering, aliases above the break won't be installed at boot time. (This is a common problem, and when you see it, check your list of aliases.) For example, an alias of 192.168.3.4 would be listed as: