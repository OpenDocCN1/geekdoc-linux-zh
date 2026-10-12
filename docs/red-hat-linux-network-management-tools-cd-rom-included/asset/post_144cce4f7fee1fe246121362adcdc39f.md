
![](img/f265c9d1f2610aca197c430cbfcd51f5_502_0.png)

**Figure 9.4 MRTG weekly, monthly, and yearly reports.**

information is obtained for each of the monitored interfaces. You can customize this update interval (or refresh rate) as well.

## Basic Configuration of MRTG

MRTG uses a configuration file to specify which devices are to be monitored. The MRTG package doesn’t come with a predefined configuration because the devices listed wouldn’t likely match those at your site. Instead, the package includes a utility program called **cfgmaker**, which is used to build a basic configuration so you don’t have to create one from scratch. The purpose of this utility is to poll a network device for specific SNMP objects (e.g., interfaces table) and build a configuration file suitable for MRTG. The syntax of **cfgmaker** is as follows:

```
cfgmaker community@device
```

Two arguments are required: the device's community string and hostname (or IP address). Because **cfgmaker** writes to standard out, the output should be redirected to a file when you want to save the results. To illustrate the use of this utility, let's assume that we want to monitor a single router in a remote office. In this example, we have a Cisco 2500 series router, called remote-gw, with a community string of louvre. Thus the command:

```
# cfgmaker louvre@remote-gw > cisco.conf
```

probes the remote-gw device and builds the **MRTG** configuration file with the name of cisco.conf. Assuming the arguments provided to the **cfgmaker** are correct and the device responds to the SNMP requests, Listing 9.1 shows the configuration that would be generated (minus the comments added by **cfgmaker**) by the **cfgmaker** script:

### Listing 9.1 Sample cfgmaker configuration file

```
Target[10.0.2.75.1]: 1:public@10.0.2.75
MaxBytes[10.0.2.75.1]: 124994
Title[10.0.2.75.1]: remote-gw (No hostname defined for IP address): Ethernet0
PageTop[10.0.2.75.1]: <H1>Traffic Analysis for Ethernet0
</H1>
<TABLE>
    <TR><TD>System:</TD><TD>remote-gw in Graphics Lab 11-BK</TD></TR>
    <TR><TD>Maintainer:</TD><TD>Steve Maxwell</TD></TR>
    <TR><TD>Interface:</TD><TD>Ethernet0 (1)</TD></TR>
    <TR><TD>IP:</TD><TD>No hostname defined for IP address (161.135.59.129)</TD></TR>
    <TR><TD>Max Speed:</TD>
        <TD>1250.0 Kbytes/s (ethernetCsmacd)</TD></TR>
</TABLE>
# --------------------------------------------------
Target[10.0.2.75.2]: 2:public@10.0.2.75
MaxBytes[10.0.2.75.2]: 6982
Title[10.0.2.75.2]: remote-gw (No hostname defined for IP address): Serial0
PageTop[10.0.2.75.2]: <H1>Traffic Analysis for Serial0
</H1>
<TABLE>
    <TR><TD>System:</TD><TD>remote-gw in Graphics Lab 11-BK</TD></TR>
<TR><TD>MaxSpeed:</TD><TD>6982.0 Bytes/s (rfc877x25)</TD></TR>
</TABLE>
#
```

To support comments in the MRTG configuration file, use the hash (#) character at the beginning of each line. The file ignores blank lines. The configuration file includes one or more polling instances that contain tokens and associated values. These tokens collectively represent a single monitored element. Each element represents a polled entity that includes the SNMP objects to query from the device being monitored and additional display formatting for the resulting information. Each element is separated by a single hash (#) followed by a series of “...” characters (as shown in the last line of Listing 9.1). This particular router contains only a few network entries, and the keyword target corresponds to each router interface. This is a key observation: any data that is going to be monitored and displayed by MRTG requires a target entry.

This particular router contains three interfaces—one Ethernet and two serial—but cfgmaker only reports two interfaces. Because the third interface is administratively down, cfgmaker skipped this interface. Either this interface was not configured within the router or it was disabled for some other reason. In any event, cfgmaker includes the first two interfaces but inserts a comment character in front of the third interface in the cisco.conf file so that it will not be polled with the MRTG software, as shown in Listing 9.2.

### Listing 9.2
Commented interface entry

```
##
# This interface is one of the following
# - administratively not UP
# - it is in test mode
# - it is a softwareloopback interface
# - has a unrealistic speed setting
# It is commented out for this reason.
##
```

```
# Target[10.0.2.75.3]: 3:public@10.0.2.75
# MaxBytes[10.0.2.75.3]: 193000
# Title[10.0.2.75.3]: remote-gw (No hostname defined for IP address): Serial1
# PageTop[10.0.2.75.3]: <H1>Traffic Analysis for Serial1
# <BR></H1>
# <TABLE>
# <TR><TD>System:</TD><TD>remote-gw in </TD></TR>
# <TR><TD>Maintainer:</TD><TD></TD></TR>
# <TR><TD>Interface:</TD><TD>Serial1 (3)</TD></TR>
# <TR><TD>IP:</TD><TD> ()</TD></TR>
# <TR><TD>Max Speed:</TD>
# <TD>193.0 kBytes/s (propPointToPointSerial)</TD></TR>
# </TABLE>
# ---------------------------------------------------------------
```

Disabling the interface is a good idea because it is not reasonable to have MRTG poll nonactive interfaces when there is no traffic, thus producing empty graphs. Also, if the interface is enabled and put into service at some future date, it is a simple matter to "uncomment" the interface entry, thus permitting MRTG to monitor the port. The MRTG configuration file uses the HTML formatting language and, in particular, builds a table to format the device information, as denoted by the <TABLE> and </TABLE> tags. The configuration also includes one or more keywords that control which devices are monitored and how data is graphed. Each keyword contains the following syntax:

```
Command [label] args
```

where **Command** is one of the commands shown next, followed by a label enclosed with brackets and one or more arguments or command options.

Each monitored element or interface within the configuration file usually contains the following keywords:

- Target
- MaxBytes
- Title
- PageTop

The **target** keyword indicates to MRTG what it should monitor. The basic format is as follows

```
Target[label]: port:community@device
```

The *label* is used as an identifier, so that MRTG can display a group of keywords on one HTML page. The *label* is a combination of the device IP address and interface number. The *port* is the interface number as defined in the *device* that MRTG should poll with the SNMP *community string* of *community*. The port or interface number must be a valid interface on the device being polled. You can determine the valid interfaces on a given device with the MRTG cfgmaker program. By using this program, you will cause all defined interfaces within a given device to be discovered automatically. Alternatively, using a MIB browser, you can peruse the MIB tree of the device and examine the interface table to discover the interfaces manually. However, if you already know which interfaces you want to monitor, specifying them manually might be the simplest approach. Using the configuration example above, consider the following **Target** command:

```
Target[10.0.2.75.1]: 1:public@10.0.2.75
```

This command will define the *label* 10.0.2.75.1 and instruct MRTG to monitor traffic from the first interface of the device with the IP address of 10.0.2.75 using the *community string* of public. By default, *MRTG polls the MIB objects* ifInOctets *and* ifOutOctets *from the specified device and graphs this data over time.*

The **MaxBytes** keyword defines the upper limit for any monitored traffic statistics and determines the y-axis range for unscaled graphs. For any interface, the **MaxBytes** keyword is normally specified in bytes per second, which can be calculated by dividing the maximum bandwidth of the interface by eight. For example, because 10M Ethernet has a maximum bandwidth of 10Mbps, dividing this by eight (8), we get 1250000 (10,000,000 / 8 = 1,250,000). Setting this value correctly is very important because this will ensure that the graphs display realistic information. For example, in Listing 9.2, the command

```
MaxBytes[10.0.2.75.1]: 1250000
```
