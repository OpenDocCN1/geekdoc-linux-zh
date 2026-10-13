# Monitoring Your Network: ping, netstat, tcpdump, and Ethereal

With the ping program, you can check to see if you can actually access another host on your network. The ping program sends a request to the host for a reply. The host then sends a reply back, and it is displayed on your screen. The ping program continually sends such a request until you stop it with a break command, CTRL-C. You see one reply after another scroll by on your screen until you stop the program. If ping cannot access a host, it issues a message saying the host is unreachable. If ping fails, this may be an indication that your network connection is not working. It may be only the particular interface, a basic configuration problem, or a bad physical connection. ping uses the Internet Control Message Protocol (ICMP), discussed in Chapter 19. Networks may block these protocols as a security measure, also preventing ping from working. A ping failure may simply indicate a security precaution on the part of the queried network.

To use ping, enter ping and the name of the host.

```
$ ping ftp.redhat.com
```

# Ethereal

Ethereal is a network protocol analyzer that lets you capture packets transmitted across your network, selecting and examining those from protocols you want to check. You can examine packets from a particular transmissions, displaying the data in readable formats. The Ethereal interface displays three panes: a listing of current packets, the protocol tree for the currently selected packet, a display of the selected packets contents. The first pane categorizes entries by time, source, destination, and protocol. There are button headers for each. To sort a set of entries by a particular category, click its header. For example, group entries by protocol, click the Protocol button; for destinations, use the Destination button.

# Capture Options

To start Ethereal, you select the Start entry from the Capture menu. This opens an options window where you can select the network interface to watch. Here you can also select options such as the file to hold your captured information in and a size limit for the capture, along with a filter to screen packets. With the promiscuous mode selected, you can see all network traffic passing through that device, whereas with it off, you will see only those packets destined for that device.

The Capture Files option lets you select a file to save your capture in. If no file is selected, then data is simply displayed in the Ethereal window. If you want to keep a continuous running snapshot of your network traffic, you can use ring buffers. These are a series of files that are used to save captured data. When they fill up, the capture begins saving again to the first file, and so on.

+   - Display options control whether packets are displayed in real time on the Ethereal window.
+   - Capture limits let you set a limit for the capture either by packets, size, or time.
+   - Name resolution enables the display of host and domain names instead of IP addresses, if possible.

# Ethereal Filters

A filter lets you select packets that match specified criteria, such as packets from a particular host. Criteria are specified using expressions supported by the Packet Capture Library and implemented by tcpdump. Ethereal filters use similar expressions as those used by the tcpdump command. Check the tcpdump Man page for detailed descriptions.

An expression consists of an ID, such as the name or number of host, and a qualifier. Qualifiers come in three types: type, direction, and protocol. The type can reference the host, network, or port. The type qualifiers are host, net, and port. Direction selects either source or destination packets, or both. The source qualifier is src, and the destination, dst. With no destination qualifier, both directions are selected. Protocol lets you specify packets for a certain protocol. Protocols are represented using their lowercase names, such as icmp for ICMP. For example, the expression to list all packets coming in from a particular host would be src host hostname, where hostname is the source host. The following example will display