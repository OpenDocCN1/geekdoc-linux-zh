```
bootparams:	nisplus [NOTFOUND=return] files
ethers:	files
netmasks:	files
networks:	files
protocols:	files
rpc:	files
services:	files
netgroup:	nisplus
publickey:	nisplus
automount:	files
aliases:	files nisplus
```

# Network Interfaces and Routes: ifconfig and route

Your connection to a network is made by your system through a particular hardware interface,
such as an Ethernet card or a modem. Data passing through this interface is then routed to
your network. The ifconfig command configures your network interfaces, and the route
command sets up network connections accordingly. If you configure an interface with a
network configuration tool, such as system-config-network, you needn’t use ifconfig or
route. However, you can directly configure interfaces using ifconfig and route, if you
want. Every time you start your system, the network interfaces and their routes must be
established. This is done automatically for you when you boot up by ifconfig and route
commands executed for each interface by the /etc/rc.d/init.d/network initialization file, which
is executed whenever you start your system. If you are manually adding your own interfaces,
you must set up the network script to perform the ifconfig and route operations for your
new interfaces.

# Network Startup Script: /etc/rc.d/init.d/network

Your network interface is started up using the network script in the /etc/rc.d/init.d directory.
This script will activate your network interface cards (NICs) as well as implement configuration
information such as gateway, host, and name server identities. You can manually shut down
and start your network interface using this script and the restart, start, or stop options,
as well as system-config-services. You can run the script with the service command. The
following commands shut down and then start up your network interface:

```
service network stop
service network start
```

If you are changing network configuration, you will have to restart your network
interface for the changes to take effect:

```
service network restart
```

To test if your interface is working, use the ping command with an IP address of a
system on your network, such as your gateway machine. The ping command continually
repeats until you stop it with a CTRL-C.

```
ping 192.168.0.1
```