
# CHAPTER 13 Network Connectivity

| 208.559.243.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | lo |
| 0.0.0.0 | 149.112.50.65 | 0.0.0.0 | UG | 0 | 0 | eth0 |

The route command can add to the table using the add option. With the add option, you can specify a host (-host) or a network (-net) as the destination. If no option is used, the route command assumes that you are configuring the issuing command. The most common uses for the route command is to add the default gateway for a host, for a host that has its routing table, or if the gateway address has changed. For example, to add a gateway with a specific IP address, you could use the following:

```
# /sbin/route add default gw 149.112.50.65
```

Note that you can use a hostname instead of an IP address if desired. Another common use is to add the network to the routing table right after the ifconfig command to configure the interface. Assuming that the 208.59.243.0 entry from the previous example was missing, replace it using the following command:

```
# /sbin/route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

You can also use /sbin/route to configure a specific host for a direct (point-to-point) connection. For example, say that you have a network of two computers. One of the computers has a modem through which it connects to your business network. You typically work at the other computer. You can use the route command to establish a connection through specific hosts using the following command:

```
# /sbin/route add -host 198.135.62.25 gw 149.112.50.65
```

The preceding example makes the computer with the modem the gateway for the computer you are using. This type of command is useful if you have a gateway or firewall connected to the Internet. There are many additional uses for the route command, such as manipulating the default packet size. See the man page for those uses.

### /bin/netstat
The netstat command is used to display the status of your network. It has several parameters that can display as much or as little information as you prefer. The services are listed by sockets (application-to-application connections between two computers). You can use netstat to display the information in Table 13.2.

### TABLE 13.2 netstat Options

| Option | Output |
| --- | --- |
| -g | Displays the multicast groups configured |
| -i | Displays the interfaces configured by ifconfig |
| -s | Lists a summary of activity for each protocol |

### TABLE 13.2 Continued Output

| Option | Output |
| --- | --- |
| -v | Gives verbose output, listing both active and inactive sockets |
| -c | Will update output every second (good for testing and troubleshooting) |
| -e | Gives verbose output for active connections only |
| -C | Displays information from the route cache and is good for looking at past connections |

Several other options are available for this command, but they are used less often. As with the /sbin/route command, the man page can give details about all options and parameters.

## Red Hat Network Configuration Files

As previously stated, seven network configuration files can be modified to make changes to basic network interaction of your system. The files are:

- /etc/hosts—Listing of addresses, hostnames, and aliases
- /etc/services—Network service and port connections
- /etc/nwitch.conf—Linux network information service configuration
- /etc/resol.conf—Domain Name Service domain (search) settings
- /etc/host.conf—Network information search order (by default, /etc/hosts and then DNS)
- /etc/HOSTNAME—the host; traditionally supported but not used by Red Hat Linux
- /etc/sysconfig/network—hostname, IP address, boot control, and gateway settings

As the first six of these files are modified, the changes are active. With configuration files, comments can be added with a hash (#) preceding the comment. The last file (/etc/sysconfig/network) requires the networking daemons to be restarted after the file is used. All seven of these files have a man page written about them for information.

### Adding Hosts to /etc/hosts

The /etc/hosts file is a map of IP to hostnames. If you're not using DNS or another naming service and are connected to a large network, this file can get quite large and be a real headache to manage. A small /etc/hosts file can look like this:

```
127.0.0.1       localhost  localdomain
128.112.50.6    mydomain.com    yourhost
```

Wait, let's re-examine the text. "The first entry is for loopback. The second is for the name of the machine. The third is another machine on the network. If naming service is in use on the network, the only host that will recognize by name is your own IP addresses on the network. If you are using a naming service, the last line isn't needed and can be deleted. However, if /etc/hosts connects frequently, it might be good to leave the entry so that host does not need to consult the naming service each time. This can save time and reduce the strain on the network or naming service."

### Service Settings in /etc/services

The /etc/services file maps numbers to services. The first few lines look similar to this (/etc/services file can be quite long, with more than 500 lines):

```
# Each line describes one service, and is of the form:
# service-name port/protocol [aliases] [comment]

rpc      1/tcp          # TCP port multiplexer
rpc      1/udp          # UDP port multiplexer
rlogin   5/tcp           # Remote Job Entry
rlogin   5/udp           # Remote Job Entry
echo        7/tcp
echo        7/udp
discard  9/tcp          null
discard  9/udp          null
sysstat  11/tcp         users
```

Typically, there are two entries for each service because most services can use either TCP or UDP for their transmissions. Usually /etc/services is initially configured, you will not need to change it.

### Using /etc/nswitch.conf After Naming Services

This file was initially developed by Sun Microsystems to specify the order that services are accessed on the system. A number of services are listed in the /etc/nswitch.conf file but the most commonly modified entry is the hosts entry. A portion of the file can look like this:

```
passwd:  files
shadow: files
group:  files
hosts:  db nisplus dns
hosts:   files
```

### Using Red Hat Linux Network Configuration Tools

This tells services that they should consult standard UNIX/Linux files for passwd, shadow, and group (/etc/passwd, /etc/shadow, /etc/group, respectively lookups). For host lookups, the system will check /etc/hosts and if there is no entry, it will check DNS. The commented hosts entry lists the possible values for hosts. Only edit this file if your naming service has changed.

### Setting a Name Server with /etc/resolv.conf

/etc/resolv.conf is used by DNS, the Domain Name Service. (DNS is covered in detail in Chapter 14.) The following is an example of resolv.conf:

```
nameserver 192.172.2.3
nameserver 192.172.3.9
search mydomain.com
```

This sets the nameservers and the order of domains for DNS to use. The contents of this file will be set automatically if you use Dynamic Host Configuration Protocol, or DHCP (see the section on "DHCP" later after this).

### Setting DNS Search Order with /etc/host.conf

/etc/host.conf file lists the order in which your machine will search for hostname resolution. The following is the default /etc/host.conf file:

```
order hosts, bind
```

In this example, the file will check /etc/hosts file first and then perform a DNS lookup. Couple more options control how the name service is used. The only reason to modify this file is if you use NIS for your name service or you want one of the optional services. The nosport option can be a good option for system security. It will compare a standard DNS lookup to a reverse lookup (host-to-IP then IP-to-host) and fail if they don't match. The drawback is that when proxy services are used, the lookup will fail, so you want to use this with caution.

### Using /etc/HOSTNAME After Hostname Changes

This file contains a single word, your hostname. It is initially created from the /etc/sysconfig/network file. If your hostname changes, the /etc/HOSTNAME file is no longer used by Red Hat Linux; however to avoid confusion, it is best to include this file when making changes.

### Examining Host Network Settings in /etc/sysconfig/network

Changes to /etc/sysconfig/network won't take effect until you restart the networking daemons or reboot. If you use Red Hat's graphical configuration network tools (described in the next section), you should not edit this file. The file looks like this:
