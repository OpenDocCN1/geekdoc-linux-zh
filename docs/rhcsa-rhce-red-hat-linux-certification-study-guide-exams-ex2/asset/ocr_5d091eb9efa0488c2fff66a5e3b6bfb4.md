# FIGURE 5-11

The ifconfig command

```
[root@server1 ~]# ifconfig
eth0      Link encap:Ethernet  HWaddr 52:54:00:55:08:A2
          inet addr:192.168.122.50  Bcast:192.168.122.255  Mask:255.255.255.0
          inet6 addr: fe80::5054:ff:fe55:0a2/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:16895 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15364 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:5725595 (5.4 MiB)  TX bytes:8162800 (5.8 MiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:15889 errors:0 dropped:0 overruns:0 frame:0
          TX packets:15889 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:9089760 (8.6 MiB)  TX bytes:9089760 (8.6 MiB)

[root@server1 ~]#
```

The ifconfig command can also be used to configure network interfaces. For example, you can assign a new IP address for eth0 with the following command:

```
# ifconfig eth0 192.168.122.250
```

The first parameter, eth0, tells you which interface is being configured. The next argument, 192.168.122.250, indicates the new IP address being assigned to this interface. To make sure the change worked, issue the ifconfig command again (with the name of the adapter device) to view its current settings.

With the right switch, the ifconfig command can modify a number of other settings for your network adapter. Some of these switches are shown in Table 5-6.

Of course, you'll want to make sure the changes survive a reboot, whether it be for the exam, or for a server that you want to administer remotely. That depends on appropriate changes to configuration files in the /etc/sysconfig/network-scripts directory, described shortly. And any changes made with the ifconfig command are, by definition, temporary.