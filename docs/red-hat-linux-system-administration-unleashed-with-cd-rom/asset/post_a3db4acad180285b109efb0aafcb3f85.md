
## Networking options

- [Y] Kernel/User netlink socket
- [Y] Network firewalls
- [Y] Socket Filtering
- [Y] TCP/IP networking
- [Y] IP: firewalling
- [Y] IP: firewall packet netlink device
- [Y] IP: always defragment (required for masquerading)
- [Y] IP: transparent proxy support
- [Y] IP: masquerading
- [Y] IP: ICMP masquerading
- [Y] IP: masquerading special modules support
- [Y] IP: aliasing support
- [Y] IP: TCP syncookie support (not enabled per default)

## Network device support

- [Y] Network device support
- <> Dummy net driver support
- [Y] Ethernet (10 or 100Mbit)
- Select your particular network card

Once you have finished the kernel configuration, do a

```
make clean, make dep, make zImage (or make bzImage)
```

Install the new kernel in /boot, and edit /etc/lilo.conf to reflect the new kernel. At this time, it is best not to install the new kernel as the default because it may have a problem somewhere (such as an incorrect ethernet device driver, and so on). Always test a new kernel before making it the default in lilo.

## Transproxy

Transproxy is a tool that performs transparent redirection of requests from one port to another, hence the name transproxy (transparent proxy). This tool is very useful. Transproxy provides the capability to configure a transparent proxy without having to recompile the kernel or add redirection rules to an existing firewall. In essence, this userspace program provides the same capabilities as the redirection rules in ipfwadm or the Jump chains provided in ipchains.

The first thing to do is obtain the latest version of the software. It can be found in the location shown in Table 26.1. Once the file has been downloaded, simply unpack it and build:

```
# gzip -dc transproxy_0.3.orig.tar.gz | tar -xvf -
# cd transproxy-0.3
# make
# make install
```

Once installed, transproxy can be configured to run called from inetd, the network superdaemon, or as a standalone service. Either way, the following line should be added to /etc/services:

```
tproxy    tcp/81    # Transparent Proxy
```

### Installing Transproxy

To install transproxy running under inetd, /etc/inetd.conf should be modified by adding the following line to it:

```
tproxy stream tcp nowait nobody /usr/sbin/tcpd in.tproxyd <destination> 8080
```

This tells inetd to accept requests on port 81 and start tproxyd, which will pass these requests to the proxy-server destination on port 8080. Say, for example, you were running a Web server called www.foo.com on the host me.foo.com, but you didn't want to run the server directly on port 80 because it is a reserved port and requires that the software be run as root. You could reconfigure your Web server software to run on port 8080, then adjust the <destination> setting to be as follows:

```
/etc/services:

    tproxy    tcp/80    # Transparent Proxy

/etc/inetd.conf:

    tproxy stream tcp nowait nobody /usr/sbin/tcpd in.tproxyd me.foo.com 8080
```

Thus, every time someone makes a connection to www.foo.com, the request is automatically redirected to port 8080 on me.foo.com. The user doesn't see the difference and doesn't have to know what port the server is actually running on. Of course, this is only one possible example and in fact, for a Web server, running tproxy out of inetd is not the best configuration. The good news is that transproxy can be run as a standalone service. In this case, inetd knows nothing about the transproxy service so every time a request comes in, inetd does not have to start up another tproxyd daemon.

To configure transproxy for standalone service, the /etc/services file should be modified by adding the preceding example entry. Once that is done, all that needs to be accomplished is the startup of the tproxy server. As root, type the following (the # character is the root prompt and should not be typed):

```
# /usr/sbin/in.tproxyd -s 80 -r nobody me.foo.com 8080
```

Now the tproxy program is running on its own, listening on port 80 (-s 80) with the user id of nobody (-r nobody) and redirecting to port 8080 on the machine me.foo.com. To ensure that the transproxy daemon gets started every time the machine is rebooted, add the following to the Red Hat /etc/rc.d/rc.local file:

```
#
# Start the transproxy service to redirect port 80 to port
# 8080
#
echo Starting transproxy service: port 80 -> port 8080
/usr/sbin/in.tproxyd -s 80 -r nobody me.foo.com 8080
```

It is possible to use firewall rules to redirect port 80 to port 81 so that you don't have to have an actual service running on port 80. You can do that if you want to be able to leave the original port 80 entries in your /etc/services. An example of such redirection will be given later in the chapter when we discuss ipfwadm and ipchains. Transproxy is not limited to Web server proxying—it can also be used to proxy other services such as telnet, ftp, SSH, and more.

## SOCKS Proxy Server

The SOCKS proxy server package has been around for quite some time. The package comes with a SOCKS server daemon as well as some client programs (as of this writing, the latest SOCKS version is 4.2beta and supports the following client programs: ftp, telnet, whois, and finger). The SOCKS program, despite its age, can still be used effectively to provide proxying service for a network. With SOCKS, a single configuration file and a single daemon are the only things that need to be set up. The daemon handles all services.

### Setting Up SOCKS

To compile SOCKS, obtain the gzipped tarfile from the FTP site listed in Table 26.1. Once the gzipped tarfile has been downloaded, untar the file as shown here and build the socks server and clients:

```
# gzip -dc socks-linux-src.tgz | tar -xvf .
# cd socks42b
```

```
edit the top-level Makefile as well as include/socks.h

# make
# make install.server (this will install the SOCKS server,sockd, into the destination

directory defined in the top-level Makefile, as well as a
config file, test_sockd_conf and
the documentation).
# make install.clients (this will install the SOCKified
clients to the destination
directory defined in the top-level Makefile
```

Note that you will need to install the clients on every machine that is being served by the SOCKS proxy server. As with any other software package that you build, be sure to read the instructions included with the package.

Once the server is installed, edit the file /etc/services and add the following line:

```
socks 1080/tcp #SOCKS proxy service
```

Add the following to /etc/inetd.conf:

```
socks stream tcp nowait nobody <path/to/sockd>/sockd sockd
```

### Tuning SOCKS Configuration Files

There are at least two and possibly three configuration files that will need to be tuned to fit your circumstances. If you have a dual-homed host and you have disabled IP forwarding (either directly in the kernel configuration or by the command "echo 0 > /proc/sys/net/ipv4/ip_forward"), you will need to edit /etc/sockd.conf, /etc/socks.conf, and /etc/sockd.route files. A dual-homed host has more than one network interface (physical or logical). If you have a host with only one network interface or you have enabled IP forwarding (in the kernel configuration and by the command "echo 1 > /proc/sys/net/ipv4/ip_forward"), you only need /etc/sockd.conf.

The file /etc/sockd.conf determines whether a client can have access to the sockd proxy server. This file consists of two categories of entries: permit and deny. The format for the entries is

```
<Identifier Key> <IP address> <Netmask>
```

The identifier key is one of two values: permit or deny; the IP address refers to the source address of the requesting client; and the netmask is the modifier for that particular network. For example, say you have a private network with an assigned network range of 192.168.1.*. To permit all of the systems in the network to access the SOCKS proxy server, the following entry should be in the /etc/sockd.conf of your proxy server:

```
permit 192.168.1.0 255.255.255.0
```

This entry permits any machine whose IP address begins with 192.168.1 to connect to sockd. The best thing to do is to have the “permit” entries first and then deny everything. In essence, this causes the SOCKS server to deny everything except what was specified in the permit lines. Continuing with the preceding example, to have the sockd server only allow access from machines in the 192.168.1.* network, the sockd.conf file may consist of these entries:

```
permit 192.168.1.0 255.255.255.0
deny 0.0.0.0 0.0.0.0
```

The clients file, /etc/socks.conf, is used by SOCKS clients to determine whether to use a direct or proxied connection to a given destination. Unlike the sockd.conf file, the clients file has three entries: deny, direct, and sockd. Deny specifies which addresses the sockd server should reject. Direct specifies which IP addresses do not need to use the sockd server. Both deny and direct have the same format as in the sockd.conf file:

```
<Identifier Key> <IP address> <Netmask>
```

The sockd entry specifies which host is running the sockd server. The format for this entry is

```
sockd @=<serverlist> <IP address> <Netmask>
```

A simple example of a clients file would be

```
direct 127.0.0.1 255.255.255.255
direct 192.168.1.0 255.255.255.0
sockd @=<192.168.1.1> 0.0.0.0 0.0.0.0
```

Here the loopback address is directly attached. Any system on the local network (192.168.1.0) is also considered to be directly attached since it is on the same LAN. All other addresses must use the sockd proxy server on the host 192.168.1.1 for their connections. This channels all connections from the internal network through the SOCKS proxy host.

The file /etc/sockd.routes is used by a multi-homed SOCKS server to determine which of its network interfaces to use to reach a given destination address. Communication between hosts on the same side of a firewall would not need to be defined in the routing file so long
