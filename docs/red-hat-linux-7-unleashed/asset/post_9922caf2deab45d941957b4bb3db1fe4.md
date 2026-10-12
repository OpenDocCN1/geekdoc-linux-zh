
> **Tip**
>
> If you issue a route command and it hangs, press Ctrl+C to interrupt it and issue `route -n`. Issuing `route` without the `-n` parameter causes it to do a reverse lookup of every IP in the routing table. If DNS is configured and the host is currently not connected to the network, issuing `route` by itself can take a long time.

# Manipulating the Routing Table

The `route` command also adds and removes routes from the routing table. This is done via the following commands:

```
route add|del -net|-host target gw gateway \netmask netmask dev interface
```

The `add` or `del` commands indicate, respectively, whether you want to add or delete a route.

The optional `-net` or `-host` options indicate whether you want to operate on a net or a host route. (See the following “Host-Based Static Routes” section for more information on net or host routes.) Providing any ambiguity is usually best. For example, the address `10.0.1.0` can be either the network address of a class C network, or the address of a host in a class A or B network.

The `target` parameter is the host address or network number of the destination. You would use the keyword `default` as the target for setting or deleting the default route.

The optional `gateway` parameter indicates which gateway to use for this route. If omitted, the `route` command assumes that the host or network is connected directly to this host. It’s important to add a route to the local network after configuring an interface with `ifconfig`:

```
# /sbin/ifconfig eth0 10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
# /sbin/route add -net 10.1.1.0
```

As its name implies, the optional `netmask` parameter sets the netmask for the route, which will be applied to the target address. If omitted, the netmask will be taken either from the default netmask for the IP address or (in the case of routes to local networks) from the interface’s netmask. (See “Netmasks and Network Classes” earlier in this chapter for more information on the default netmask.)

The optional `dev` parameter sets the interface on which the packets to this destination will be sent. If omitted, the `route` command checks the current routing table to find which interface has a route to the gateway. If no gateway is provided, it determines which interface can be used to get directly to the target.

# Warning

In **linuxconf** there is a screen called Configure the routed Daemon. This will remain by default in the Does Not Export Any Routes (Silent) mode for most users. Making changes to the way your routed daemon behaves may cause undesirable behavior on the part of your system. Unless you are configuring your system to perform routing functions, leave this alone.

# Host-Based Static Routes

Although the *route* command is most often used to manipulate *network* routes (those that point to a remote network), sometimes it is necessary to add routes to specific hosts. This can be necessary, for example, if a host is connected through a point-to-point link (for example, through a modem or serial cable). See Figure 20.8 for an example.

**FIGURE 20.8**
*Host-based static routes are needed when a host is connected via a point-to-point link.*

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_710_0.png)

In this example, host `10.1.1.1` won't know how to get to host `10.2.1.1` without the following *route* command:

```
# /sbin/route add -host 10.2.1.1 gw 10.1.1.2
```

# Checking Network Status: netstat

The */bin/netstat* command displays the status of all TCP/IP network services. It has several options, depending on the information you want to display.

`netstat` by itself lists all connected sockets. The `-a` (all) option lists all open or listening sockets, not just those that have connections. The information listed for each socket includes

-   The protocol (tcp or udp).
-   Number of bytes currently in the send and receive queues (bytes that the local process hasn’t read or that the remote process hasn’t acknowledged).
-   Addresses of the local and remote hosts. The remote host address is displayed as *:* for sockets that are in LISTEN state.
-   Socket state. This can be ESTABLISHED, SYN_SENT, SYN_RECV, FIN_WAIT1, FIN_WAIT2, TIME_WAIT, CLOSED, CLOSE_WAIT, LAST_ACK, LISTEN, CLOSING, or UNKNOWN. In general, the SYN_ states indicate that a connection is in the process of being opened, the _WAIT states indicate the socket is in the process of being closed, ESTABLISHED means the socket is connected, LISTEN means a daemon is waiting for clients to connect, and CLOSED means the socket is unused.

The `netstat -e` (extended) option lists, in addition to this information, the user currently using the socket.

`netstat -r` (routes) lists the routing table. It lists the same information as the `route` command with no parameters.

`netstat -i` (interfaces) lists the network interfaces and statistics on each interface. It displays the same statistics as the `ifconfig` argument, but is in table form for easy parsing.

As with the `route` command, you can also add the `-n` option to view numeric IP addresses instead of hostnames.

## Network Daemons

A daemon is a program that waits for another program to ask it to do something. Network daemons in particular are similar to the jacks in an operator’s switchboard. They create one or more sockets and listen to those sockets, waiting for another process to connect. In Linux, as with most variants of UNIX, network services can be provided in one of two ways: as standalone daemons where they handle each session themselves or incorporated into another configuration (such as `inetd`) that handles the connections and disconnections for it.

Originally, all UNIX network servers were standalone daemons. When you wanted to start a server, you ran a program that created the socket and listened to it. Many UNIX server programs still run in this manner. Examples are Squid, the Web cache/proxy server; Samba, the SMB file/print server; Apache, the Web server, and many others (see Chapter 12, "Apache Server," and Chapter 17, "Samba").

Even though they have many functions, most network daemons usually share a few characteristics:

-   Their names end with a $d$ (for *daemon*).
-   They respond to the HUP signal (HANG UP signal; read `man 7 signal` for more information) by rereading their configuration files. The HUP signal is sent by the `kill -HUP` command.
-   They are usually started at boot time by scripts in the `/etc/init.d` directory. These scripts minimally accept the `start` and `stop` parameters to start and end the daemons. Most of them accept the `restart` parameter to tell the daemon to reread its configuration files.
-   When they receive a request, they create another copy of themselves to service it. Thus, there may be several copies of each daemon running simultaneously at any given time.

## Networking Service Control

In the standalone daemon model, each service you run on a server has a corresponding daemon. This poses several problems:

-   If you have many services on a server, you need to have many daemons running, even if they are idle. Although inactive daemons will probably be swapped out to disk, they still take up valuable resources, such as virtual memory and process table entries.
-   There is no centralized way of modifying the daemons to provide services such as encryption or access control. Each daemon program must be modified to provide these services.
-   If a daemon dies because of user or programmer error, the service will not be available until it is restarted. The restart procedure can be automated, but then the program that restarts the daemon can also die.
-   Programming a network daemon isn't easy, especially because most daemons must be multithreaded. Being multithreaded enables them to manage several requests at once.

Eventually someone came up with a solution. How about a single daemon that could be configured to listen to any number of sockets and transfer control to different programs when it was needed? This daemon would also take care of multithreading and of managing the sockets. Thus was born *inetd*, the original so-called “Internet super-server.” This is the time we should mention a relatively new addition to Red Hat Linux: *xinetd*. This program is meant to be a secure replacement for *inetd*. Though not completely secure, it is much more secure than *inetd*.

# Configuring xinetd

*xinetd* has built-in access control features for stopping connections from undesired clients or only allowing desired connections. It can limit the number of incoming connections, number of incoming connections from specific hosts, or total number of connections for a service. This feature is particularly useful in assistance in thwarting what is known as DDoS (Distributed Denial of Service) attacks. It can limit access to services based on access time of day. *xinetd* can have services bind to specific IPs. This lets you provide different services to internal clients than external clients. *xinetd* is installed at installation time with Red Hat Linux if you select the Everything option for your installation.

When *xinetd* is installed, a Perl script is supplied in the same directory as the *xinetd* binary that conveniently converts an *inetd*.conf into an *xinetd*.conf. It may be run when you are logged in as root by typing the string `/usr/sbin/xconf.l < /etc/inetd.conf > /tmp/xinetd.conf`, where `/usr/sbin` is your path to the *xinetd* executable. The *xinetd*.conf looks much like a legacy *inetd*.conf file and may be edited much the same as well. As with most subjects with regard to Red Hat Linux, an entire chapter could be written on *xinetd*. You may read more in depth about *xinetd* at `http://www.synack.org/xinetd/`. Here are some of the keywords most commonly used when configuring this new “Super Server”:

| Keyword | Description |
| :--- | :--- |
| wait | This attribute determines if the service is single-threaded or multi-threaded. If its value is `yes` the service is single-threaded; this means that *xinetd* will start the server and then it will stop handling requests for the service until the server dies. If the attribute value is `no`, the service is multithreaded and *xinetd* will keep handling new service requests. |
| user | Determines the *uid* for the server process. The user name must exist in `/etc/passwd`. This attribute is ineffective if the effective user ID of *xinetd* is not superuser. |
| group | Determines the *gid* for the server process. The group name must exist in `/etc/group`. If a group is not specified, the group of *user* will be used (from `/etc/passwd`). This attribute is ineffective if the effective user ID of *xinetd* is not superuser. |
