This is what will appear in the Network Neighborhood browser window on Windows servers and workstations. If your Ubuntu Samba server is participating on a network with WINS support, you can remove the comments in the two wins lines and enter the appropriate settings for your WINS network.

WINS networks can also utilize the standard domain name system (DNS) to advertise Windows server names and IP addresses. If your network utilizes this service you can set the dns proxy parameter to yes.

The name resolve order parameter defines what order the Samba software uses to attempt to resolve a hostname into an IP address on the network. The lmhosts file is the Windows version of the Linux host file, but it relates Windows hostnames to IP addresses.

# Networking

The networking part of the global section defines settings for interfacing the Samba server on the network.

```
interfaces = 127.0.0.1/8 eth0
; bind interfaces only = yes
```

The interfaces parameter defines which network interfaces the Samba software will use to listen for connection attempts. By default, this value is set to only the 127.0.0.1 localhost address for the server. To allow remote clients and servers to connect to your Ubuntu Samba server, you'll need to add either the interface name of your network interface (such as eth0, as shown in this example) or the IP address of the interface.

If you don't have a firewall between your Ubuntu server and the network you can enable the bind interfaces only parameter. This parameter restricts connections to only those destined to the server's IP address. Broadcast messages aren't accepted.

# Debugging/Accounting

The debugging part of the global section defines some features that provide logs allowing you to monitor the Samba server activity for problems.

```
log file = /var/log/samba/log.%m
max log size = 1000
# syslog only = no
syslog = 0
panic action = /usr/share/samba/panic-action %d
```