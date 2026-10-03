# APPLY YOUR KNOWLEDGE

# Exercises

The following exercises require two hosts connected via Ethernet. You should have two hosts connected via a network, one named hostA and the other named hostB.

# 13.1 Obtaining Network Information

In this exercise, you’ll use the various network commands and utilities to obtain information about your system and network.

Estimated Time: 15 minutes

+   1. Log in as root on hostA. Make sure you have an entry in your /etc/inet/hosts file for hostB.

+   2. As root, use the ifconfig command to display information about your network interface:

```
ifconfig -a
lo0: \
flags=1000849<UP,LOOPBACK,RUNNING,MULTICAST,\
IPv4> mtu 8232 index 1
inet 127.0.0.1 netmask ff000000
hme0: \
flags=1004843<UP,BROADCAST,RUNNING,MULTICAST,\
DHCP,IPv4> mtu 1500 index 2 \
inet 192.168.1.106 netmask ffffff00 broadcast\
192.168.1.255 \
ether 8:0:20:a2:63:82
```

The ifconfig utility shows that the Ethernet address of the hme0 interface is 8:0:20:a2:63:82. The first half of the address is generally specific to the manufacturer. In this case, 8:0:20 is Sun Microsystems. The last half of the address, a2:63:82, is unique for every system.

+   3. Use ping to send ICMP echo requests from hostA to hostB.

```
ping hostB
```

On hostA, use the rpcinfo utility with the -p option to list the registered RPC programs:

```
rpcinfo
```

+   4. Look for the sprayd service on your system:

```
rpcinfo | grep sprayd
```

+   5. Stop the sprayd service on your local system as follows:

```
rpcinfo -d sprayd 1
```

+   6. Verify that the sprayd service is gone:

```
rpcinfo | grep sprayd
```

+   7. Restart the sprayd service by sending a HUP (hangup) signal to the inetd daemon, as follows:

```
pkill -HUP inetd
```

+   8. Verify that the sprayd service is running:

```
rpcinfo | grep sprayd
```

# 13.2 Using snoop to Display Network Information

In this exercise, you’ll use the snoop, spray, and ping commands to obtain information from your network.

Estimated Time: 10 minutes

+   1. On hostA, log in as root into a CDE session. In one window, start up the snoop utility as follows:

```
snoop hostA hostB
```

+   2. snoop will show what actually happens when hostA uses the ping command to communicate with hostB. In a second window on hostA, type the following:

```
ping hostB
```

+   3. Watch the information that is displayed in the first window that is running snoop.

+   4. Now issue the spray command to send a one-way