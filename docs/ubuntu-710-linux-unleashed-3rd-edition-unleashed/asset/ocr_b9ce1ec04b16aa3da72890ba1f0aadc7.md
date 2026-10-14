Note that you could use a hostname instead of an IP address if desired. Another common use is to add the network to the routing table right after using the `ifconfig` command to configure the interface. Assuming that the 208.59.243.0 entry from the previous examples was missing, replace it using the following command:

```
$ sudo route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

You also can use route to configure a specific host for a direct (point-to-point) connection. For example, say that you have a home network of two computers. One of the computers has a modem through which it connects to your business network. You typically work at the other computer. You can use the route command to establish a connection through specific hosts using the following command:

```
$ sudo route add -host 198.135.62.25 gw 149.112.50.65
```

The preceding example makes the computer with the modem the gateway for the computer you are using. This type of command line is useful if you have a gateway or firewall connected to the Internet. There are many additional uses for the route command, such as manipulating the default packet size. See the man page for those uses.

```
/bin/netstat
```

The netstat command is used to display the status of your network. It has several parameters that can display as much or as little information as you prefer. The services are listed by sockets (application-to-application connections between two computers). You can use netstat to display the information in Table 14.2.

TABLE 14.2  netstat Options

| Option | Output |
|---|---|
| `-g` | Displays the multicast groups configured |
| `-i` | Displays the interfaces configured by `ifconfig` |
| `-s` | Lists a summary of activity for each protocol |
| `-v` | Gives verbose output, listing both active and inactive sockets |
| `-c` | Updates output every second (good for testing and troubleshooting) |
| `-e` | Gives verbose output for active connections only |
| `-C` | Displays information from the route cache and is good for looking at past connections |

Several other options are available for this command, but they are used less often. As with the route command, the man page can give you details about all options and parameters.

# Network Configuration Files

As previously stated, five network configuration files can be modified to make changes to basic network interaction of your system. The files are

+   - `/etc/hosts`—A listing of addresses, hostnames, and aliases
+   - `/etc/services`—Network service and port connections