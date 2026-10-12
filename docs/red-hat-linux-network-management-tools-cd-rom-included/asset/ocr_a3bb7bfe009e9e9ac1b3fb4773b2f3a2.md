+   * operating modes 
+   * display options 
+   * packet filter options

# Operating Mode Options

These options are used to control how **tcpdump** will capture and display network traffic. The available options are summarized in Table 4.10 and described fully below.

**Table 4.10** *tcpdump operating mode options*

| Option | Description |
| --- | --- |
| -c | Captures specified number of packets |
| -F | Uses file as source for filter expression |
| -i | Captures packets using alternate network interface |
| -p | Disables capturing in promiscuous mode |
| -r | Reads capture file instead of network interface |
| -w | Saves raw packets to file |

Normally, **tcpdump** will listen for traffic on the primary network interface. Usually the primary interface has the smallest numeric identifier if the system contains two or more interfaces of the same type. For example, eth0 is considered the primary when the system contains two Ethernet interfaces: eth0 and eth1. However, if you want to run **tcpdump** on a different interface, use the -i option and the device name to specify the alternate interface. For example, to select the point-to-point (ppp) interface, use the following command:

```
# tcpdump -i ppp0
tcpdump: listening on ppp0
```

As previously indicated, **tcpdump** will capture packets until ^C is typed from the controlling terminal (or if placed in the background, until the process is terminated with the **kill** command). If you wish to specify the number of packets to be captured, use the -c option