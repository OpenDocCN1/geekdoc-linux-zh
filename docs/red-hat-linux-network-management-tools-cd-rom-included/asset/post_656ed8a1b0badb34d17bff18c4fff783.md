
The Email includes the hostname (if available), the IP address, Ethernet Address, Ethernet Vendor, and date/time stamp of the event. In this case, a RMON probe was installed on the local network and **arpwatch** detected this new device. Also, a message is sent to the syslog process that will find its way into the `/var/log/messages` file. The format of the *syslog* message is different than the format of the Email shown here:

> Dec 27 13:05:09 probe arpwatch: new station 10.0.2.50
> 0:c0:d4:0:9:40

Clearly, being informed regarding this type of change on the network could really come in handy. New station messages will only be generated once when the device is first installed and powered up. Once this event has been logged for the first time, no additional messages will be generated, even if the device is booted multiple times or is disconnected from the network and re-attached at a later time. As long as the **arpwatch** database is maintained and preserved, a new station message will truly indicate that a new device has been added to the network. This is an excellent way to be informed when users add devices to the network without your explicit knowledge.

## Changed Ethernet Address

This message is generated because **arpwatch** has detected that the datalink address of a device has changed, but the IP address has remained the same. This could happen when a new interface card is installed to replace a defective unit or the datalink addresses are changed for some other reason, perhaps even on purpose. The associated Email message that is generated includes the following:

> From root Fri Dec 24 23:07:43 1999
> Date: Fri, 24 Dec 1999 23:07:43 -0400
> From: arpwatch@socrates.home.com (Arpwatch)
> To: root@socrates.home.com
> Subject: changed ethernet address (switch.home.com)
>
> hostname: switch.home.com
> ip_address: 10.0.2.60
> ethernet address: 0:0:1d:a:5d:1
> ethernet vendor: Cabletron
> old ethernet address: 0:0:1d:a:5c:ff
> old ethernet vendor: Cabletron
> timestamp: Friday, December 24, 1999 23:07:42 -0400
> previous timestamp: Thursday, December 23, 1999 21:25:30 -0400
> delta: 1 day

Actually, this message was not the result of a new interface being installed in a device. Rather, because this device is a multiport Cabletron Ethernet switch, it contains a large number of network interfaces. Because the connection to the network for this device was moved from one port to another, arpwatch detected the change. The original interface had an address of 0:0:1d:a:5c:ff, while the new port had the address of 0:0:1d:a:5d:1. Note that in both cases, the vendor was identified as Cabletron, which was the correct vendor of the hardware. To make this report a little more useful, the delta of elapsed time is shown. This represents the amount of time that has passed when arpwatch first recorded the datalink/IP pair and when the port change first happened.

## Flip Flop

This message type indicates that the host mentioned was the most recently monitored address, but now has become the second most-monitored address. For instance, the message

```
From root Sat Jul 31 14:07:15 1999
Date: Sat, 31 Jul 1999 14:07:15 -0400
From: arpwatch@socrates.home.com (Arpwatch)
To: root@socrates.home.com
Subject: flip flop (durer.home.com)

hostname: durer.home.com
ip address: 10.0.2.10
ethernet address: 0:60:97:e:a3:6
ethernet vendor: 3Com
old ethernet address: 0:0:1d:a:5c:ff
old ethernet vendor: Cabletron
timestamp: Saturday, July 31, 1999 14:07:15 -0400
previous timestamp: Saturday, July 31, 1999 14:06:29 -0400
delta: 46 seconds
```

indicates that the most recently seen host is called durer.home.com, which contains the datalink address of 0:60:97:e:a3:6 and uses a 3Com interface card. The second most-seen address was the Cabletron device with the datalink address of 0:0:1d:a:5c:ff.

Before this message was issued, the Cabletron device was the most active on the network.

### New Activity

The new *Activity* message is generated when an Ethernet/IP address pair has been seen for the first time within a six month (or more) period of time. This will be useful for tracking devices that for some reason have been out of service or disconnected from the network for quite a while, and now have been placed back in service or reattached to the network. In practice, however, this may not be a very meaningful message because of the duration of time. Rather, it would be better if the interval of time could be customized by the user to be shorter. However, in the current version of the tool, this feature isn't supported.

One of the more interesting capabilities of the tool includes the parsing of **tcpdump** output. Using the -r option, **arpwatch** will parse these specially formatted files, build a database, and report the history of the network with monitoring messages previously discussed. This may come in handy when **arpwatch** reports are needed, but for some reason **arpwatch** can't be executed in real-time to monitor the network.

## Ethereal Tool

### General Description

The **ethereal** command is a powerful Ethernet network monitoring solution that can be used to capture and analyze network traffic in real-time or off-line modes. This tool picks up where **tcpdump** ends by providing full packet-level protocol decoding that boasts support for many popular Network protocols and an easy-to-use packet capture interface. Additionally, **ethereal** supports many other commercial package capture formats, so you can continue to use your existing software and process these datafiles with **ethereal**.

This tool provides a robust GUI interface that streamlines the capturing of network data and subsequent browsing of network traffic. The main window contains a set of menu items, three panels, plus three status or input boxes on the bottom, as shown in Figure 5.1. Many of the menu items are self explanatory and won't be covered in detail. The first panel contains a summary of all the packets captured. This panel contains a packet number, timestamp, source, destination, protocol, and information fields. As you will see later in this section, these fields are customizable, and the user can remove or include additional packet field information.

![](img/f265c9d1f2610aca197c430cbfcd51f5_220_0.png)

- Progress Bar
- Display Filter
- Status Box
- Packet Summary Window
- Packet Detail Windows

Figure 5.1 Main ethereal window.

The next panel shows a hierarchical view (packet detail) that contains all the higher-layer protocols displayed in a tree format. The remaining panel includes a hexadecimal display of the entire packet. As the user moves through the second panel via the tree view, the bottom panel highlights where the cursor is positioned within the packet. A progress area on the left-hand side of the main window shows the status of tasks, and a filter text box has been provided to accept filtering of displayed packets within the first panel. Finally, an information box on the right-hand side of the main window indicates the name of the data file and the number of dropped packets.

The software supports a number of important command-line options that can be divided into two categories: display mode and function mode options. Display mode options can control such items as the size of individual display panels and the type and size of font used. Table 5.2 lists the display options.

Table 5.2 ethereal display options
| Option | Description |
|--------|-------------|
| -B | Controls the initial height of the bottom hexadecimal panel |
| -P | Controls the initial height of the packet summary panel |
| -T | Controls the initial height of the packet tree view panel |
| -b | Uses the specified bold font for packet field display |
| -m | Uses the specified font instead of default |
| -t | Sets the format of the packet timestamp when displayed in the summary packet panel |

The functional mode options control such items as which network interface will be used to read captured traffic, the maximum size of packets that should be read during a packet capture, etc. Table 5.3 lists these command options.

Table 5.3 ethereal functional options
| Option | Description |
|--------|-------------|
| -c | Capture the number of packets as specified with this option |
| -h | Show version and information |
| -i | Specifies the network interface to capture packets |
| -n | Disable hostname resolution and TCP/UDP port name mappings |
