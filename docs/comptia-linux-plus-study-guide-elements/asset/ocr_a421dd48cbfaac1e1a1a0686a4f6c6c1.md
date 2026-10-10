# ## Examining the ARP Cache

The **arp** utility examines or updates the ARP cache—the list of local IP addresses and their associated hardware addresses maintained by the computer. Used as a diagnostic tool, this utility can help you verify that some of the most fundamental parts of a network link are working.

Before using **arp** as a diagnostic tool, though, you must first at least attempt to contact a few other computers using other tools. Linux builds the ARP cache as network activity occurs. For instance, if you attempt to connect to **192.168.24.78**, Linux sends a query to the network looking for this system, and, if that system replies, Linux adds that system to its ARP cache. Only after that point will the **arp** command show the association.

You should also keep in mind that **arp** is a _local_ network tool; it returns data only on the computers that exist on the same network segment as the system on which it’s run. That is, you won’t get data on computers on the Internet at large; those systems are accessed via your network gateway system. You should see your Internet gateway system in the ARP cache, though—assuming you’ve accessed that gateway, either directly or by accessing systems to which it routes.

The simplest way to use **arp** is to type its name alone:

```
$ arp
  Address    HWtype  HWaddress       Flags  Mask  Iface
  hindmost.rodsbooks.com  ether  08:10:74:24:1b:d4  C         eth0
  hal900011a1ar.rodsboo  ether  00:0c:76:96:a3:73  C         eth0
  seeker.rodsbooks.com  ether  00:e0:4c:ee:59:e6  C         eth0
```

This use shows three systems in the ARP cache, identified by their hostnames, hardware types, hardware addresses, flags, masks, and network interfaces. If nothing appears in the ARP cache, then either you’ve made no network access attempts or something is seriously wrong with your configuration. Try using **ifconfig** to verify that the network interface is up, and check your network cabling. If several systems appear but one that should appear doesn’t, perhaps that system is down, or perhaps the cabling between the two systems is at fault—for instance, a cable could be disconnected, or a switch might be faulty.

Several **arp** options enable you to limit the program’s output. For instance, -H **type** limits output to specific hardware types, such as **ether** for Ethernet; -i **Iface** limits output to specific interfaces; and -n substitutes IP addresses for hostnames.

In addition to providing information, **arp** enables you to manipulate the ARP cache. This isn’t normally necessary, but it could be helpful if you’ve reconfigured a computer or if you want to delete an entry you believe is causing problems. The -d **address** option deletes the entry for a specified IP address, while -s **ip_address** **hw_address** adds an entry for the specified IP address and hardware address. These changes may not hold forever, though; the ARP table is dynamic, so any changes you make may be overridden as normal network operations occur.