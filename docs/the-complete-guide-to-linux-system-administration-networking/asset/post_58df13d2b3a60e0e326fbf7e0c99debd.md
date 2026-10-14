
You can also use the lpstat command to see a quick summary of what each printer is doing.

## Tracking Print Jobs

To view the print jobs in the default print queue, enter the command lpq. The lpq utility lists each of the print jobs in a print queue with the following information:

- Status of the print job, such as active (currently printing), ready, or error
- Owner (the user who submitted the print job)
- Class of the print job (its priority; normally A, unless the -C option is used with the lpr command)
- Job number assigned by the print server
- Size of the file in bytes (characters)
- Time that the print job was submitted

Any user can view the current print jobs using lpq. A sample lpq command is shown here:

```
$ lpq -P hplj
```

If you are working on a server where the print queue contains many documents, you may either want to use the -s option, to display a shorter format for each print job, or add a job ID to the lpq command. The job ID refers to the print job number assigned by the print server and displayed under the Job field in the sample lpq output above. To see a list of all print jobs submitted by user alexv, enter this command:

```
$ lpq alexv
```

If you have previously used lpq to identify the job number of a large print job, use that number to query the status of the job, as in this example:

```
$ lpq 572
```

You can delete print jobs from any print queue. If you are logged in as root, you can delete anyone's print jobs, or move a print job to another print queue or to the top of a print queue so that it is printed next. The lprm command deletes a print job from a queue. You need a job ID from lpq before you can use lprm to delete a specific print job. For example, if you decide after viewing the output of lpq that print job number 491 should be deleted before it is printed, use this command to remove it from the hplj print queue:

```
$ lprm -P hplj 491
```

You can remove all of a user's print jobs by referring to a user name. Each user can remove his or her own print jobs in this way; root can remove anyone's print jobs:

```
# lprm nwells
```

You can also remove all of the print jobs in a queue by using the - (hyphen) parameter:

```
# lprm -P hplj -
```

When you are using CUPS, the cancel command works just like the lprm command.

## Using Graphical Print Management Utilities

Instead of lpc, lpq, and lprm, you can choose System Tools, then Print Manager on the GNOME main menu. When the main window of the Print Manager appears, double-click the print queue that you want to manage. A dialog box listing all print jobs currently in that print queue appears. (See Figure 12-18.)

![](img/43f64015de86d989e30eff5bb284fb96_583_0.png)

Within that dialog box, you can review information about each print job and cancel any print job that is causing problems.

KDE also includes graphical utilities to manage printing. If KDE is installed, you can start the KDE Control Center (enter kcontrol at a command line), then open the Peripherals item on the left side of the Control Center, choose Printers, then choose the Jobs tab on the right side of the Control Center. (See Figure 12-19.) You can also use this section of the Control Center to configure print queues.

![](img/43f64015de86d989e30eff5bb284fb96_584_0.png)

## Figure 12-19 Managing print jobs in the KDE Control Center

When you are using CUPS for printing, you can manage print jobs in the same interface where you create and modify printer definitions. After starting a browser with the localhost:631 address, choose the Jobs link to view print jobs. You can use the options on that page to control each print job as needed.

The design of CUPS allows you to manage print jobs on any networked system where you have been granted permissions in the cups.conf configuration file. Compare this to lpd, for which you must have a shell account with root access to a system in order to manage print jobs, and then can probably only do so using command-line utilities.

## CHAPTER SUMMARY

- Linux networking hardware differs from other devices—they are not available until an appropriate kernel module is installed in the kernel and configures the physical networking device.
- Each Ethernet card includes a unique MAC address. This address is used by the Address Resolution Protocol to permit a computer to locate other computers and routers on the same part of the network.
- The ifconfig command is used to configure a networking interface in the Linux kernel. Other scripts are also used to start or stop network devices when sufficient details are included in system configuration files. These scripts include ifup, ifdown, and the network script in /etc/rc.d/init.d.
- The *route* command modifies the internal routing table, which instructs the Linux kernel how to process packets that a computer receives that are not intended for that system. IP forwarding must be enabled for Linux to route packets between two network interfaces (and thus between two networks).
- Each Ethernet card can be assigned multiple IP addresses for purposes such as hosting multiple Web sites on one system. This is called IP aliasing and can be done manually using configuration files or graphically using system-config-network or other utilities.
- The system-config-network utility is one example of the graphical tools provided in each version of Linux to help you easily configure networking devices.
- The DNS resolver is configured using */etc/resolv.conf*. Resolution of names is also controlled by */etc/hosts.conf* and */etc/nsswitch.conf*, which determine where the resolver looks for name resolution, either the local */etc/hosts* file, a configured DNS server, or other modes such as NIS+.
- The *route* command provides static routing. Routing protocols are also supported by Linux in order to provide dynamically changing routing information for large, complex networks. RIP, OSPF, and BGP and three examples of routing protocols. All are supported in Linux by the *routed* or *gated* daemons.
- Setting up a DHCP server on Linux requires configuring the */etc/dhcpd.conf* file with IP addresses that can be assigned and a few other basic parameters. Having a Windows system use Linux as its DHCP server requires an additional *route* command to compensate for Windows’ nonstandard DHCP.
- Linux printing relies on printer definitions, usually called print queues. Print jobs are submitted to these queues and are stored in directories until a print server sends the print job to a physical printer. In UNIX printing, multiple users can print to multiple printers either locally or across a network.
- Traditionally, UNIX used a printing system called LPRng and a print server daemon called *lpd*. This system uses commands such as *lpr, lpc, lprm,* and *lpq* to manage printing.
- A newer UNIX printing system called CUPS permits much easier network-wide management of both printers and print jobs without having separate user accounts on many systems. CUPS uses a Web browser interface to manage printing.
- Red Hat Linux and Fedora support both LPRng and CUPS printing using an alternatives printing system. Standard printing commands use symbolic links to refer to either LPRng or CUPS underlying commands based on the configuration tools used to set up printing.
- Printing in UNIX relies on print filters and printer description files to simplify the task of supporting thousands of diverse printer models. Manufacturers are just starting to provide strong support for Linux printing.
- Print jobs can be managed using the command line, with utilities such as *lpc, lpstat, lpq,* and *lprm*. Graphical utilities are also very useful. These include the GNOME Print Manager and the KDE Control Center.

## COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| alternatives | Configure or view symbolic links to select among alternative printing or mail server systems | alternatives --config print |
| arp | Displays the internal cache of MAC-to-IP address mappings that was creating using the Address Resolution Protocol | arp |
| cancel | Removes (deletes) a pending print job from a print queue when using CUPS printing | cancel -P hpj 491 |
| cupsd | Daemon that controls printing in the CUPS printing system; similar to the lpd daemon in LPRng printing | cupsd |
| gated | Gateway daemon used for complex routing; Supports the OSPF and BGP routing protocols (as well as the older RIP protocol) | gated |
| ifconfig | Displays currently configured network interfaces or configures new network interfaces | ifconfig |
| ifdown | Script used to stop a named network interface. Located in /etc/sysconfig/network-scripts | ifdown eth0 |
| ifup | Script used to start a named network interface; Located in /etc/sysconfig/network-scripts | ifup eth0 |
| lpc | Manages LPRng-based printing, showing status, permitting or stopping queue submission and physical printing, and performing other printing-related tasks; Table 12-1 shows lpc options | lpc status |
| lpq | Displays the print jobs in one or more print queues; the status of a single print job number, of all jobs submitted by a named user, or all print jobs in one or all print queues can be displayed | lpq -P hpj |
| lprm | Removes (deletes) a pending print job from a print queue; a single print job number, all jobs from a named user, or all print jobs in a named print queue can be deleted | lprm -P hpj 491 |
| lpstat | Displays the current status of a print queue | lpstat |
