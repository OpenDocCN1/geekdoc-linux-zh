If there was no response, the troubleshooting should continue below the ARP layer. Figure 4-24 shows how to check the ARP table using the arp command.

```
# arp
Address (1)          HWtype  HWaddress (2)          Flags Mask (3)  Iface (4)
172.20.3.182         ether   00:03:47:38:77:8A      C               bond0
```

+   (1) IP address of the other side
+   (2) MAC address of the other side
+   (3) entry type
+     C : normal entry, drop out after a certain period of time
+     M : persistent entry
+     P : entry for Proxy ARP
+   (4) interface name
+   ARP table is managed per interface

Figure 4-24 Using the arp command for diagnosis

# Survey in the QETH layer

Figure 4-25 shows the different things that can be surveyed in the QETH layer. The main thing that needs to be checked in this layer is whether the qeth device driver has recognized the devices. Figure 4-26 on page 133 shows a sample output of the /proc/qeth file indicating how to check whether the network device is recognized by the qeth device driver.

![](bbox=[0.25, 0.74, 0.85, 0.9])

+   /proc/qeth
+     - check whether the qeth device driver recognize the devices
+   lsqeth
+     - check whether the qeth device driver recognize the devices
+     - confirmation of Layer2/Layer3 mode
+   /var/log/messages
+     - confirmation of the error messages related to qeth
+   /proc/qeth_perf
+     - the statistics information of qeth device driver
+   s390dbf
+     - the trace related to qeth

Figure 4-25 Survey in the QETH layer