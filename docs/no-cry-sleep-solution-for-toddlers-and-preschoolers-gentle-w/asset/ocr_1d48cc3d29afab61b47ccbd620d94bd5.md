each. To sort a set of entries by a particular category, click its header. For example, group entries by protocol, click the Protocol button; for destinations, use the Destination button.

# Capture Options

To start Ethereal, you select the Start entry from the Capture menu. This opens an options window where you can select the network interface to watch. Here you can also select options such as the file to hold your captured information in and a size limit for the capture, along with a filter to screen packets. With the promiscuous mode selected, you can see all network traffic passing through that device, whereas with it off, you will see only those packets destined for that device.

+   - The Capture Files option lets you select a file to save your capture in. If no file is selected, then data is simply displayed in the Ethereal window. If you want to keep a continuous running snapshot of your network traffic, you can use ring buffers. These are a series of files that are used to save captured data. When they fill up, the capture begins saving again to the first file, and so on.

+   - Display options control whether packets are displayed in real time on the Ethereal window.

+   - Capture limits let you set a limit for the capture either by packets, size, or time.

+   - Name resolution enables the display of host and domain names instead of IP addresses, if possible.

# Ethereal Filters

A filter lets you select packets that match specified criteria, such as packets from a particular host. Criteria are specified using expressions supported by the Packet Capture Library and implemented by tcpdump. Ethereal filters use similar expressions as those used by the tcpdump command. Check the tcpdump Man page for detailed descriptions.

An expression consists of an ID, such as the name or number of host, and a qualifier. Qualifiers come in three types: type, direction, and protocol. The type can reference the host, network, or port. The type qualifiers are host, net, and port. Direction selects either source or destination packets, or both. The source qualifier is src, and the destination, dst. With no destination qualifier, both directions are selected. Protocol lets you specify packets for a certain protocol. Protocols are represented using their lowercase names, such as icmp for ICMP. For example, the expression to list all packets coming in from a particular host would be src host hostname, where hostname is the source host. The following example will display all packets from the 192.168.0.3 host.

```
src host 192.168.0.3
```

Using just host will check for all packets going out as well as coming in for that host. The port qualifier will check for packets passing through a particular port. To check for a particular protocol, you use the protocol name. For example, to check for all ICMP packets you would use the expression

```
icmp
```

There are also several special qualifiers that let you further control your selection. The gateway qualifier lets you detect packets passing through a gateway. The broadcast and