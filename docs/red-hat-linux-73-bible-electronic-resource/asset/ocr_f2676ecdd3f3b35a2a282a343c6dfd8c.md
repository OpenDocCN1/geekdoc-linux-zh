```
# ipchains -P forward DENY
# ipchains -A forward -i ppp0 -s 10.0.0.0/255.0.0.0 -j MASQ
```

This example shows that, by default, forwarding is denied (DENY). Forwarding is done, however, for a computer on the network 10.0.0.0 (with a netmask of 255.0.0.0); packets will be forwarded to the ppp0 interface and masqueraded (MASQ) as if they came from the local Red Hat Linux system.

You could use a shorter notation for entering the netmask. For a class A, B, or C network, the value is 8, 16, or 24, respectively. Instead of allowing the whole network, you could also just allow individual hosts. For example, you could have separate forward lines for 10.0.0.10, 10.0.0.11, 10.0.0.12, and so forth.

+   5. To set up your forwarding rules permanently, you can add them to the ipchains configuration file. This will run the rules each time the system reboots (or the network restarts). If you added the rules described above to the `/etc/sysconfig/ipchains` file, the file would appear as follows:

```
:input ACCEPT
:forward ACCEPT
-P forward DENY
-A forward -i ppp0 -s 10.0.0.0/255.0.0.0 -j MASQ
:output ACCEPT
```

+   6. At this point, you may want to restart your network and your firewall as follows:

```
# /etc/init.d/network restart
# /etc/init.d/ipchains restart
```

+   7. To check that your ipchains commands worked, print out the `ip_fwchains` proc file contents as follows:

```
# cat /proc/net/ip_fwchains | grep MASQ
forward 0A000000/FF000000->00000000/00000000 ppp0 0 0 0
0 0 0 0-65535 0-65535 AFF X00 00000000 0 0 MASQ
```

+   8. The output shows that the forwarding policy (forward) is set to do masquerading (MASQ) for computers on the network 10.0.0.0.

# Enabling on-demand dialing

Dial-up connections were not designed to be up all the time. People generally start a dial-up connection when they need to connect to the Internet and then stop it when they are finished. If your Red Hat Linux system is acting as a router for the other computers on your LAN, it needs to be able to start up the Internet connection when the connection is needed. To ensure this, configure on-demand dialing.

Configuring on-demand dialing is not that complicated. As root user, open the `/etc/sysconfig/network-scripts/ifcfg-ppp0` file (where ppp0 represents your dial-up interface). Then add the following lines to the file: