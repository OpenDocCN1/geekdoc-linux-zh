# 8.3. Interface Control Scripts

The interface control scripts activate and deactive system interfaces. There are two primary interface control scripts, /sbin/ifdown and /sbin/ifup, that call on control scripts located in the /etc/sysconfig/network-scripts/ directory.

The ifdown and ifup scripts are symbolic links to scripts in the /sbin/ directory. When either of these scripts are called, they require the value of the interface to be specified, such as:

At that point, the /etc/rc.d/init.d/functions and /etc/sysconfig/network-functions scripts are used to perform a variety of tasks. See Section 8.4 Network Function Files for more information.

After verifying that an interface has been specified and the user executing the request is allowed to control the interface, the correct script brings it up or down. The following are common interface control scripts:

+   - ifup-aliases — Configures IP aliases from interface configuration files when more than one IP address is associated with an interface.
- ifdown-cipcb and ifup-cipipb — Used to bring Crypto IP Encapsulation (CIPE) connections up and down.
- ifdown-ipv6 and ifup-ipv6 — Contains IPv6-related function calls using environment variables in interface configuration files and /etc/sysconfig/network.
- ifup-ipx — Used to bring up an IP interface.
- ifup-plip — Used to bring up a PLIP interface.
- ifup-plusb — Used to bring up a USB interface for network connections.
- ifdown-post and ifup-post — Contains commands to be executed after an interface is brought up or down.
- ifdown-ppp and ifup-ppp — Used to bring a PPP interface up or down.
- ifup-routes — Adds routes for a device as an interface is brought up.
- ifdown-sit and ifup-sit — Contains function calls related to binding up and down an IPv6 tunnel within an IPv4 connection.
- ifdown-sl and ifup-sl — Used to bring a SLIP interface up or down.

> Warning:Removing or modifying any scripts in the /etc/sysconfig/network-scripts/ directory can cause interface connections to act strangely or fail. Only advanced users should modify scripts related to a network interface.

The easiest way to manage all network scripts simultaneously is to use the /sbin/service network on the network (/etc/rc.d/init.d/network), as illustrated by the following command:

```
/sbin/service network <action>
```

In this example <action> can be either start, stop, or restart.