
You may recall an earlier scenario in which a disabled interface caused a network problem. There are also situations when not disabling an interface can cause additional network problems. For example, during a broadcast storm or when a cracker is attempting to penetrate the network, shutting down a device or interface might be the only way to prevent the problem from spreading to other parts of the network. However, before resorting to turning off interfaces, watch out for the *set of no return* syndrome. Consider the sample network shown in Figure 8.1.

![](img/f265c9d1f2610aca197c430cbfcd51f5_467_0.png)

In this sample network, we have two routers, R1 and R2. Our only access to R2 is via router R1, using the serial 1 interface. From device Node A, we issue an snmpset command to disable the serial 0 interface from R2. This stops the broadcast storm but also causes a connectivity loss from the remote office. The problem is now: How do we enable the interface on R2 after the broadcast storm has been fixed? The set of no return means that the only means of access to the device has been cut off. Remote access to the router has been lost, unless some out-of-band management capability, such as dial-up can be used. In this case, the port must be enabled from the local side, which could require instructing someone to enable the port or reboot the device to reset the port.

The best way to avoid the *set of no return* is to disable the local *serial0* interface on **R1** or the remote *ethernet1* interface on **R2**. This way, the broadcast problem is contained, yet we still maintain access to the devices.

To disable a *serial0* interface on router **R1**, a modification of the *ifOperStatus* object must be made. This includes setting the *object to zero* (0) to disable the interface from an administrative perspective. Set this object using the following command:

```
# snmpset monset private interfaces.ifTable.ifEntry.ifAdminStatus.2 i 0\
interfaces.ifTable.ifEntry.ifAdminStatus.3 = 0
```

When executed, the command will disable the flow of traffic to and from this interface. With most agents, this change is not permanent, meaning that a system reboot will reset this object back to a default (enabled) value. However, without a system reset, the only other way to restore network connectivity will be to enable the interface using the *snmpset* command.

The *snmpset* command can alter other MIB objects within the agent. For example, consider the *sysContact* and *sysLocation* objects. Let’s assign new values to these objects using a single *snmpset* command:

```
# snmpset cisco-gw10 private system.sysContact.0 s "NCC Support"\
      system.sysLocation.0 s "3rd Floor Closet"
```

When the command has been executed, it returns the following:

```
system.sysContact.0 = "NCC Support" \
      system.sysLocation.0 = "3rd Floor Closet"
```

## Snmpstatus Tool

The *snmpstatus* command obtains important information from an SNMP network entity using the SNMP *get-request* operation. The syntax of the command is as follows:

```
snmpstatus host community
```

When the remote agent utilizes the generic community string of public, the string may be dropped from the SNMP commands because public is used by default. By the way, the use of the public community string is highly discouraged.

When the snmpstatus command is used against a device, it displays the following information:

- IP Address of the device
- sysDescr MIB object
- sysUpTime MIB object
- number of packets received and transmitted on all active interfaces (i.e., the sum of ifInCastPkts.* and ifInNUCastPkts.* objects)
- number of IP packets received and transmitted (i.e., ipInReceives.0 and ipOutRequests.0)
- number of active interfaces
- number of interfaces that have been disabled

Thus, running the command

```
# snmpstatus switch-2200 private
```

on a device called switch-2200 displays the output shown in Figure 8.2.

Using this command is a good way to obtain a quick snapshot of a network device without knowing a lot about the node or some of the specific MIB objects to poll. As you can see, the device is Linkswitch 2200 (made by 3Com), running version 7.1 of the switching software. The device has been running for 90 hours and 23 minutes. Notice that snmpstatus has detected eight interfaces that are down. This isn't a problem in this case because the device is an Ethernet switch where interfaces are attached to personal computers or workstations.

Some users reboot their systems more often and power down their systems when they leave the office each evening. This causes the switch ports to be marked as down, and explains why they show up in the snmpstatus output.

![](img/f265c9d1f2610aca197c430cbfcd51f5_470_0.png)

Figure 8.2 *Output of the snmpstatus command.*

This tool can do a quick inventory of a network by using the shell. For instance, consider the following command:

```
# foreach node (10.0.2.1 10.0.2.202 10.0.2.254 10.0.2.250) {
  foreach? snmpstatus $node public; echo
  foreach? end
}
```

This command generates the following output:

```
[10.0.2.1]->[Cisco Internetwork Operating System Software
IOS (tm) GS Software (RSP-JV-M), Version 11.1(16)CA, EARLY
DEPLOYMENT RELEASE SOFTWARE (fc1)
Synced to mainline version: 11.1(16)
Copyright (c) 1986-1997 by cisco Systems, Inc.
Compiled Sat 20-Dec-97 04:21 by jlp: Up: 168 days, 3:23:39
Interfaces: 23, Recv/Trans packets: -1270803594/-666101155 | IP:
-15165/5442/102937871
9 interfaces are down!

[10.0.2.202]->[Cisco Systems WS-C5000] Up: 167 days, 15:31:32
Interfaces: 100, Recv/Trans packets: 258062534/866645 | IP:
22222133/0
32 interfaces are down!

[10.0.2.254]->[Fibre Channel Switch.] Up: 1 day, 8:35:11
Interfaces: 2, Recv/Trans packets: 43996343/16638 | IP:
20002011/7886

[10.0.2.250]->[AXON LANservant - Ethernet (4.16)] Up: 9:45:21
Interfaces: 3, Recv/Trans packets: 4027/1135 | IP: 0/0
```

Using the **foreach** built-in command of the csh, a list of IP addresses is assigned between the parentheses. When **foreach** is executed, it calls the **snmpstatus** command and replaces each of the IP addresses with the variable $\mathit{node}$. In the output above, it is obvious that it is very easy to use this tool to probe the network. In practice, it would be more reasonable to build a shell script to inventory these devices on a more continued basis, rather than interactively from the command line. Also, the output could be placed in a text file for later review.

## Snmptable Tool

The **snmptable** command probes an agent and displays an MIB table using the SNMP $\textit{getnext}$-request operation. The syntax of the command is as follows:

```
snmptable [ common options ] [additional options] host community tableID
```

The minimum required arguments include host, community, and tableID. The tableID must be a real SNMP table, such as $\mathit{interfaces.ifTable}$. The ifTable table contains a series of MIB objects that contain performance information and other characteristics of the interfaces within a device. Within MIB-II, which is described in Chapter 6, “Overview of MIB-II,” the following tables are defined and can be displayed with this command:

- interface table ($\mathit{interfaces.ifTable}$)
- IP address table ($\mathit{ip.ipAddrTable}$)
- IP routing table ($\mathit{ip.ipRouteTable}$)
- IP net media table ($\mathit{ip.ipNetToMediaTable}$)
- TCP connection table ($\mathit{tcp.tcpConnTable}$)
- UDP listener table ($\mathit{udp.udpTable}$)

Note that Chapter 6 describes the MIB-II tree. The basic purpose of this command is to give the user the ability to display SNMP tables and import the data into other programs for additional reporting and manipulation. For example, to display the TCP connection table, $\textit{tcpConnTable}$, use the following command:

```
# snmptable 10.0.2.240 public tcp.tcpConnTable
SNMP table: tcp.tcpConnTable
tcpConnState tcpConnLocalAddress tcpConnLocalPort tcpConnRemAddress
    tcpConnRemPort
listen    0.0.0.0      23          0.0.0.0     0
listen    0.0.0.0     111         0.0.0.0     0
listen    0.0.0.0     513         0.0.0.0     0
established 10.0.2.240  23          10.0.2.75   33441
```

If a non-table object is supplied, an error will be generated. Thus, the command

```
# snmptable 10.0.2.240 public system.sysContact.0
```

will return

```
Was that a table? system.sysContact.0.1.1
```

Here we provide the MIB object, *system.sysContact.0* (which is definitely not a MIB table), with the *snmptable* command. As you can see, an appropriate error is displayed that includes what should be the first element within the table (i.e., .1.1).

The *snmptable* command supports a few additional command-line arguments that can control the formatting of the output. Table 8.7 lists these additional options.

## Table 8.7 *Additional snmptable command-line options*

| Option | Description |
|:-------|:------------|
| -b | Displays a brief heading |
| -f | Specifies a character separator |
| -h | Prevents display of heading information |
| -H | Displays only table heading information |
| -w | Specifies the width of the table being displayed |
| -x | Adds the MIB index to the beginning of each entry listed |

One of the most useful options is -f, which is used to specify an alternative column separator character. Thus, to use the colon (:)
