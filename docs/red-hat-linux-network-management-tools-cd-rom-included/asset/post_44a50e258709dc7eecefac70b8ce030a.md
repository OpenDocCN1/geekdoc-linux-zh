
![](img/f265c9d1f2610aca197c430cbfcd51f5_494_0.png)

Figure 8.10 Community string dialog window.

terminated. Therefore, any values altered will need to be changed every time the application is started.

## Web-enabled Tools

As the previous chapter discusses network management tools and utilities for the UNIX command line and some specialized GUIs, this chapter focuses on network management tools that can be used from a Web browser. No one can discount the significant impact the Web has had on application development, common interfaces, and ease-of-use, specifically in the area of network management.
Because of the immense popularity of Web-based computing, it is reasonable to include some tools that can be used via common Web browsers.

![](img/f265c9d1f2610aca197c430cbfcd51f5_496_0.png)

These tools include both SNMP-based and non-SNMP-based software. Non-SNMP tools have been selected for those sites that have yet to implement SNMP functionality or just need a system tool that can be implemented without a lot of fuss. For those who already use SNMP, the tools in this section will be a welcome addition to any existing suite of software.

This chapter discusses the MRTG and NTOP tools.

## MRTG Tool

### General Description

The Multi-router Traffic Grapher (MRTG) tool can monitor and graph network traffic obtained from networking devices that use SNMP. As the name implies, it displays traffic utilization and other statistical information gathered from routers and other networking devices. It generates HTML pages and GIF images, providing a visual representation of network performance via a Web browser. Network performance is one of the most important aspects of network management. This tool will make it easy to pinpoint both device and network performance problems.

For example, given the network topology shown in Figure 9.1, MRTG can monitor the network from the remote router called remote-gw and other important devices, such as the backbone switch/router and workgroup switch. Because this network is critical, it is important to monitor the network traffic going to and from the router. Specifically, it is important to monitor the serial interface and both Ethernet interfaces to ensure they do not become overloaded. Further, the backbone network and any attached subnetworks should also be monitored to ensure smooth operations.

Because MRTG can monitor any device that supports SNMP, it can be put to use monitoring both edge and backbone routers as well as other critical devices. An edge router (or other device) is closer to user workstations and servers, while the backbone devices are those at the heart or core of the network. The point here is that MRTG can be used to collect vital information from many devices on the network to gain a better performance picture.

The primary method MRTG uses to collect information is the snmpget command, which was discussed previously. However, you can customize MRTG to display information derived through other means as well. For example, MRTG can display UNIX system load and disk space utilization. Further, because MRTG can poll any SNMP MIB object, many additional performance metrics and MIB objects can be retrieved. As a result of these capabilities, there are many practical uses for MRTG, including, but not limited to, the following:

- displaying network utilization on LAN and WAN links
- displaying system CPU load on networking devices
- displaying system memory utilization on network devices
- displaying modem usage on remote access servers

Conceptually, MRTG polls specific performance MIB objects from devices and displays the values in a graphical format using HTML. Figure 9.2 shows the high-level flow of MRTG. The basic operation includes collecting data from external devices and creating associated log files to store the data. Once the log files are created, HTML reports can be generated. Also, MRTG must have a configuration file that tells the program which devices to monitor and controls specific operating and formatting parameters. Unfortunately, each network is different, and the user must build this configuration file. Luckily, MRTG provides an automated tool that accomplishes much of the work needed to build a configuration specific to each network.

![](img/f265c9d1f2610aca197c430cbfcd51f5_498_0.png)

**Figure 9.1** *Sample office network.*

### Web Page Overview

By default, MRTG displays the results of network polls in a series of graphs, along with additional device information for each monitored interface. A total of four graphs is provided, showing bytes transmitted and received per second in daily, weekly, monthly, and yearly averages.

![](img/f265c9d1f2610aca197c430cbfcd51f5_499_0.png)

**Figure 9.2** *Basic operation of MRTG.*

This report includes information that was obtained via SNMP from the MIB-II *system* and *interfaces* groups from the device *remote-gw*. Consult Chapter 6, “Overview of MIB-II,” for additional information regarding these MIB groups. The *System* field is derived from the *sysName* and *sysLocation* objects, while the *Maintainer* field is obtained from the *sysContact* object. The *Interface* string represents the physical hardware interface contained within the device, and the number (1) indicates that this is the first interface. Notice in Figure 9.3 that the interface is labeled *Ethernet0*, which means that this is the first Ethernet interface on the device. It is labeled this way because Cisco routers always number their interfaces starting at zero. Figure 9.3 also shows only a partial MRTG report containing some device information plus the daily usage graph.

![](img/f265c9d1f2610aca197c430cbfcd51f5_500_0.png)

**Figure 9.3** *MRTG Web report.*

The IP string indicates that no associated hostname was found for the IP address of this device. This is not really a problem, because, some of the time, access to many networking devices is via the IP address, not the hostname. To correct this, enter the valid hostname in the local `/etc/hosts` file, or, if running DNS, add the entry in the DNS server configuration file.

The Max Speed field is calculated from the `ifSpeed` object that was divided by eight. This represents the maximum number of bytes per second that the interface can theoretically support. The value of eight was selected because there are eight bits in a single byte. The Max Speed field also confirms that this interface is Ethernet by displaying the type as `ethernetCsmacd`, which is derived from the `ifType` object contained within the MIB-2 store. The report also displays the date and time that the report was updated and how long the device has been running since it was last booted or since the network management component of the device was last reset.

The daily graph shows bytes per second over an approximate 36-hour period using a five-minute average. This average is the difference between each successive poll of bytes transmitted or received, not cumulative totals or raw counts. In other words, the displayed value is the difference between the current and previous values and is divided by the time elapsed between these readings. The horizontal axis (x-axis) shows time in two-hour increments, while the vertical axis (y-axis) shows bytes that range from zero to a given maximum value. The graph displays bytes transmitted in and out of the interface, obtained from `ifOutOctets` and `ifInOctets` MIB objects, respectively.

The bottom of the report shows the legend; in this case, incoming traffic is displayed in green, while outgoing traffic is displayed in blue. However, because this book is in black and white, the green in the graph appears gray and the blue appears black. Later on, the section called “Customizing MRTG Reports” will show how to change the colors used in the graphs. Also, the bottom of the graph contains a short summary that lists the maximum, average, and current incoming and outgoing bytes per second. This can help you spot trouble quickly. Using the customization options available with MRTG, these colors, as well as many other report and graph attributes, may be changed.

An MRTG report also contains additional graphs for weekly, monthly, and yearly totals. The weekly graph contains weekly averages for the past seven days, with the current day displayed to the left of the graph by default. The monthly report shows the last five weeks, with the current week on the left and the previous weeks to the right. The data in this graph has been averaged over a two-hour period. The yearly graph spans the previous 12 months, with the current month shown on the left, and shows the data as a daily average. Figure 9.4 shows these three graphs.

As you can see, all the graphs grow from the left, which is the default. The graphs can be made to grow from the right by enabling one on the **MRTG** command options. Also, by default, the report pages are updated automatically every five minutes when new
