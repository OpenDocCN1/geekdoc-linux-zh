
If your system has only the single Ethernet device as your IP interface, you could leave out the `dev eth0` parameter:

```bash
# route add 192.168.1.2
```

You can delete any route you establish by invoking `route` with the `del` argument and the IP address of that route, as in this example:

```bash
# route del 192.168.1.2
```

For a gateway, you first add a route to the gateway interface, and then add a route specifying that it is a gateway. The address of the gateway interface in this example is 192.168.1.1:

```bash
# route add 192.168.1.1
# route add default gw 192.168.1.1
```

If you are using the gateway to access a subnet, add the network address for that network (in this example, 192.168.23.0):

```bash
# route add -net 192.168.23.0 gw dev eth1
```

To add another IP address to a different network interface on your system, use the `ifconfig` and `route` commands with the new IP address. The following command configures a second Ethernet card (`eth1`) with the IP address 192.168.1.3:

```bash
ifconfig eth1 192.168.1.3
route add 192.168.1.3 dev eth1
```

## Monitoring Your Network: ping, netstat, tcpdump, EtherApe, Ettercap, and Wireshark

Several applications are available on Linux to let you monitor your network activity. Graphical applications like EtherApe, Ettercap, and Wireshark provide detailed displays and logs to let you analyze and detect network usage patterns. Other tools like `ping` offer specific services.

The EtherApe, Ettercap, and Wireshark tools can be accessed on the *Applications | Internet* menu. Tools like `ping`, `traceroute`, and `netstat` can be accessed with the GNOME Network Tools application accessible on the *Applications | System Tools* menu, as well as being run individually on a command line (Terminal window).

EtherApe provides a simple graphical display for your protocol activity. The *Preferences* dialog lets you set features like the protocol to check and the kind of traffic to report.

### ping

With the `ping` program, you can check to see if you can actually access another host on your network. The `ping` program sends a request to the host for a reply. The host then sends a reply back, and it is displayed on your screen. The `ping` program continually sends such a request until you stop it with a break command, `CTRL-c`. You see one reply after another scroll by on your screen until you stop the program. If `ping` cannot access a host, it issues a message saying the host is unreachable. If `ping` fails, this may be an indication that your network connection is not working. It may be only the particular interface, a basic configuration problem, or a bad physical connection. The `ping` utility uses the Internet Control Message Protocol (ICMP), discussed in Chapter 20. Networks may block these protocols as a security measure, also preventing `ping` from working. A `ping` failure may simply indicate a security precaution on the part of the queried network.

To use `ping`, enter **ping** and the name of the host.

```bash
$ ping ftp.redhat.com
```

### Ettercap

Ettercap is a sniffer program designed to detect Man in the Middle attacks. In this kind of attack, packets are detected and modified in transit to let an unauthorized user access a network. You can use either its graphical interface or its command line interface. Ettercap can perform Unified sniffing on all connections, or Bridged sniffing on a connection between network interfaces. Ettercap uses plugins for specific tasks, like `dos_attack` to detect Denial of Service attacks and `dns_spoof` for DNS spoofing detection. Check the plugins Help panel, or enter **ettercap -P list** for a complete listing. Ettercap can be run in several modes, including a text mode, a command line cursor mode, a script mode using commands in a file, and even as a daemon logging results automatically.

### Wireshark

Wireshark is a network protocol analyzer that lets you capture packets transmitted across your network, selecting and examining those from protocols you want to check. You can examine packets from a particular transmission, displaying the data in readable formats. The Wireshark interface displays three panes: a listing of current packets, the protocol tree for the currently selected packet, and a display of the selected packet's contents. The first pane categorizes entries by time, source, destination, and protocol. There are button headers for each. To sort a set of entries by a particular category, click its header. For example, to group entries by protocol, click the *Protocol* button; for destinations, use the *Destination* button.

#### Capture Options

To configure Wireshark, you select the *Options* entry from the *Capture* menu. This opens an options window where you can select the network interface to watch. Here you can also select options such as the file to hold your captured information in and a size limit for the capture, along with a filter to screen packets. With the promiscuous mode selected, you can see all network traffic passing through that device, whereas with it off, you will see only those packets destined for that device. You can then click the *Start* button to start Wireshark. To stop and start Wireshark, you select the *Stop* and *Start* entries on the *Capture* menu.

-   The *Capture Files* option lets you select a file to save your capture in. If no file is selected, then data is simply displayed in the Wireshark window. If you want to keep a continuous running snapshot of your network traffic, you can use ring buffers. These are a series of files that are used to save captured data. When they fill up, the capture begins saving again to the first file, and so on. Check *Use multiple files* to enable this option.
-   *Display options* control whether packets are displayed in real time on the Wireshark window.
-   *Limits* let you set a limit for the capture packet size.
-   *Capture filter* lets you choose the type of protocol you want to check.
-   *Name resolution* enables the display of host and domain names instead of IP addresses, if possible.

### Wireshark Filters

A filter lets you select packets that match specified criteria, such as packets from a particular host. Criteria are specified using expressions supported by the Packet Capture Library and implemented by `tcpdump`. Wireshark filters use similar expressions to those used by the `tcpdump` command. Check the `tcpdump` Man page for detailed descriptions.

You can set up either a Search filter in the *Find* panel (*Edit* menu) to search for certain packets, or set up a Capture filter in the *Options* panel (*Capture* menu) to select which packets to record. The filter window is the same for both. On the filter window you can select the protocol you want to search or capture. The *Filter name* and *string* will appear in the *Properties* segment. You can also enter your own string, setting up a new filter of your own. The string must be a filter expression.

To create a new filter, enter the name you want to give it in the *Filter Name* box. Then in the *Filter String* box, enter the filter expression, like `icmp`. Then click *New*. Your new filter will appear in the list. To change a filter, select it and change its expression in the *Filter String* box, then click *Change*.

A filter expression consists of an ID, such as the name or number of a host, and a qualifier. Qualifiers come in three types: type, direction, and protocol. The type can reference the host, network, or port. The type qualifiers are `host`, `net`, and `port`. Direction selects either source or destination packets, or both. The source qualifier is `src`, and the destination, `dst`. With no direction qualifier, both directions are selected. Protocol lets you specify packets for a certain protocol. Protocols are represented using their lowercase names, such as `icmp` for ICMP. For example, the expression to list all packets coming in from a particular host would be `src host hostname`, where `hostname` is the source host. The following example will display all packets from the 192.168.0.3 host:

```bash
src host 192.168.0.3
```

Using just `host` will check for all packets going out as well as coming in for that host. The `port` qualifier will check for packets passing through a particular port. To check for a particular protocol, you use the protocol name. For example, to check for all ICMP packets you would use the expression

```bash
icmp
```

There are also several special qualifiers that let you further control your selection. The `gateway` qualifier lets you detect packets passing through a gateway. The `broadcast` and `multicast` qualifiers detect packets broadcast to a network. The `greater` and `less` qualifiers can be applied to numbers such as ports or IP addresses.
