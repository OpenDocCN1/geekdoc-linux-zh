
In older versions of Solaris, the network startup scripts were files in /etc/init.d (chiefly rootusr, inetinit, sysid.net, and inetsvc). Solaris 10 radically restructured the way that startup files and system services are managed. The scripts have been refactored and now live in /lib/svc/method. See page 97 for an overview of Solaris’s Service Management Facility.

If /etc/defaultrouter exists, it is assumed to contain the identity (which again can be either a hostname or a numeric address) of the default gateway, and no further routing configuration is performed. As usual, a numeric address is preferable; using a name requires an /etc/hosts entry or a DNS server on the local network.

Solaris used to run routed (which it actually called in.routed) whenever no default gateway was specified, but in Solaris 10 and later you must enable routed explicitly with svcadm enable routing/route. Use the command svcs route to determine the service’s current state.

Beware: routed will go into server (talkative) mode automatically if the machine has more than one network interface or the file /etc/gateways exists. This is generally not what you want. You can prevent routed from squawking by turning on the “quiet mode” flag:

```
solaris# svccfg -s routing/route:default setprop routing/quiet_mode = true
```

## Solaris configuration examples

Here are some examples of the commands needed to bring up a Solaris interface and add a route to a default gateway:

```
solaris$ sudo ifconfig e1000g0 plumb
solaris$ sudo ifconfig e1000g0 192.108.21.48 netmask 255.255.255.0 up
solaris$ sudo route add default 192.108.21.254
```

The following examples show how to see the status of network interfaces and routing tables. Commands prefixed with sudo must be run as root. The final example shows a feature of the Solaris route command that is not present on our other architectures: the get argument shows the next hop to a particular destination. We have taken some liberties to make the examples fit on the page.

```
solaris$ netstat -nr
Routing Table: IPv4
Destination        Gateway           Flags Ref Use Interface
----------         -------           ----- --- --- ---------
default            192.108.21.254    UG    1   9959
192.108.21.0       192.108.21.48     U     1   4985 e1000g0
127.0.0.1           127.0.0.1         UH    1   107  lo0
```

```
solaris$ sudo route get google.com
route to: gw-in-f100.google.com
destination: default
mask: default
gateway: 192.108.21.254
interface: e1000g0
flags: <UP,GATEWAY,DONE,STATIC>
recvpipe sendpipe ssthresh rtt,ms rttvar,ms hopcount mtu expire
0       0       0       0       0       0       1500    0
```

## Solaris DHCP configuration

Solaris includes a DHCP client and wins the prize for the easiest and most sensible DHCP client configuration:

```
solaris$ sudo ifconfig interface dhcp
```

It just works! ifconfig calls the dhcpagent program to get the parameters for the interface from DHCP and to configure the interface with them. You can include several options on the ifconfig command line to specify the interface as the primary one, set timeouts, increase lease times, or display the status of the interface. To manually unconfigure DHCP, just run

```
solaris$ sudo ifconfig interface drop
```

This is all very nice, but you probably want DHCP to be automatically consulted at boot time. You can set this up either by providing no configuration files for an interface at all (thus relying on autoconfiguration, similar to Linux's Network Manager) or by creating an /etc/dhcp.interface file to go with the corresponding /etc/hostname.interface file. If you like, the dhcp.interface file can contain additional command-line parameters to be passed to the ifconfig command.

The hostname.interface file must still exist to get the interface to be plumbed; however, it can be left empty. If the hostname.interface file is not empty, the startup scripts will first statically configure the interface by using its contents and then later reconfigure the interface by using DHCP.
