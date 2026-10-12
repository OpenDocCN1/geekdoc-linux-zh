# Warning

In **linuxconf** there is a screen called Configure the routed Daemon. This will remain by default in the Does Not Export Any Routes (Silent) mode for most users. Making changes to the way your routed daemon behaves may cause undesirable behavior on the part of your system. Unless you are configuring your system to perform routing functions, leave this alone.

# Host-Based Static Routes

Although the *route* command is most often used to manipulate *network* routes (those that point to a remote network), sometimes it is necessary to add routes to specific hosts. This can be necessary, for example, if a host is connected through a point-to-point link (for example, through a modem or serial cable). See Figure 20.8 for an example.

# FIGURE 20.8
*Host-based static routes are needed when a host is connected via a point-to-point link.*

![](bbox=[0.25, 0.46, 0.68, 0.72])

In this example, host 10.1.1.1 won't know how to get to host 10.2.1.1 without the following *route* command:

```
# /sbin/route add -host 10.2.1.1 gw 10.1.1.2
```

# Checking Network Status: netstat

The */bin/netstat* command displays the status of all TCP/IP network services. It has several options, depending on the information you want to display.