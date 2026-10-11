```
# Default domain:
domain threeoroomco.com
# Additional networks to search:
search twooroomco.com room2.threeoroomco.com
# Nameservers:
nameserver 192.168.33.101
nameserver 192.168.33.102
```

The **domain** line specifies the domain in which the computer resides, and the **search** line specifies one or more domains the computer searches so that you don't need to provide a complete computer name. For instance, if `threeoroomco.com` has computers called `polk` and `tyler`, and if `twooroomco.com` has the computers `elizabeth` and `henry`, you can specify any of these computer names without their corresponding domains and you'll get back the correct IP addresses. The **nameserver** lines, as you might guess, specify the addresses of the nameservers. You can have up to three **nameserver** lines in the `/etc/resolv.conf` file.

# ### Automatic Configuration with DHCP

Many networks use DHCP to make configuration of most systems easier. DHCP allows a network administrator to store most of the information I've just described on a central DHCP server computer. If your computer is on a network that uses DHCP, you still need to load the appropriate kernel driver, but the computer can obtain its IP address, set its route, and set appropriate nameservers automatically. Depending upon your Linux distribution, you use either the `dhcpd` or `dhclient` command to accomplish these tasks. To use these tools manually, type the program's name followed by the interface you want to configure, as in

```
dhclient eth0
```

If an appropriate server exists on your local network, it passes back appropriate information, and Linux configures itself using that information. Both `dhcpd` and `dhclient` support several additional parameters, so you should check their man pages for more information.

# ### GUI Network Configuration

Many Linux distributions include GUI tools to aid in network configuration. For instance, Figure 17.13 shows `linuxconf`, which comes with the Red Hat and Mandrake Linux distributions. You can use these tools to set most or all of the Linux network configuration options. The details of how these tools work vary substantially from one distribution to another, unfortunately.