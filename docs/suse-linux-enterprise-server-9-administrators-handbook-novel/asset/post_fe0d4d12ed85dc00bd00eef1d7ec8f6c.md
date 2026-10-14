
## Printer Configuration

Before information can be printed, the system must be made aware of devices available to produce the required output. When a system knows of the existence of a valid output device, it can make that device available to applications. Printers can be divided into two main categories depending on how they are made available to the system: local and network. The following two sections look at each.

### Local Printers

Local printers are dependent on physical hardware present within the server. Typical hardware-specific interfaces include parallel, serial, infrared (IrDA), and USB.

Each interface type has a corresponding device file in the /dev directory through which it is accessed. Table 9.1 lists the different interface types and their corresponding device files.

**TABLE 9.1**  
Printer Interface Types and Their Device Files

| INTERFACE TYPE | DEVICE |
|---|---|
| Parallel | `/dev/lp0` |
| Serial | `/dev/ttyS0, /dev/ttyS1` |
| IrDA | `/dev/irlpt0 through /dev/irlpt3` |
| USB | `/dev/usb/lp0 through /dev/usb/lp15` |

Because the interface hardware is resident within the server, the number of local devices that can attach to a single server is limited. An average server comes preconfigured with two serial ports, a single parallel port, and two USB busses spread over four ports. Expansion beyond this requires the purchase of additional hardware.

All these technologies restrict the location of the printing device. The physical length of cable supported by the various protocols forces the printing device to be located within a few yards of the server. Though it is possible to trade off baud rate for distance in the case of serial protocols, this trade-off has serious performance implications. Newer, high-speed printers do not receive data fast enough to maintain their printing speed if they are at the end of a long, low baud rate cable.

The other drawback to co-locating printers with the server is access. In a normal data center environment, users do not have access to the room hosting the server. Access to short-range protocol printers is therefore not possible.

The solution to many of these drawbacks is to push the printer interface hardware outside the data center. This converts the short-range printer technologies discussed here into network-aware solutions.

### Network Printers

Network printers, as their name suggests, are accessible only through the network. Such printers are attached through various mechanisms to remote print servers. CUPS supports a number of different network protocols for accessing such printers.

A CUPS server can be configured in either a client or a server role. As a server, it can present a number of local print queues to the network for access by various clients. When configured as a client, CUPS listens to service broadcasts on the network and acquires a list of valid printer destinations.

A Linux server running CUPS also understands LPD, SMB, and IPX network protocols. In such cases, a local printer definition can be made to point to a network server’s printer using the appropriate network transport protocols. LPD can be used for accessing queues on non–CUPS-compatible Unix systems as well as a number of commercial print server appliances. The SMB protocol is used to access Samba or Windows server environments, while IPX is used by older Novell networks. In the case of SMB and IPX printing, the local configuration may require a username and password for accessing the remote queues.

### Adding a Local Printer

You can add printers to a server using either command-line tools or YaST. The following example shows how to add a local parallel printer to a server using YaST. In YaST, the printer configuration icon can be found under the Hardware menu option. After you select this icon, you are presented with the window displayed in Figure 9.1.

In Figure 9.1, you can see that no printers are currently defined on the server. To create a new printer definition, ensure that the Other (Not Detected) option is highlighted and click the Configure button. This brings you to the next window, as shown in Figure 9.2, where you can choose the type of printer you want to configure. In the current example, add a Canon Bubble Jet 200 to the configuration as a label printer. This device requires a parallel port connection to the host. The local interfaces are shown at the top of the list, and the network-aware protocols are grouped in the lower portion.

Because you are configuring a parallel printer, select the appropriate option shown in Figure 9.2 and click the Next button. In the next window, you can select which parallel port the printer is connected to. Because a typical server has only one parallel port, /dev/lp0, highlight that option and click Next. In the case of a serial, IrDA, or USB printer, you would have to choose the appropriate device.

FIGURE 9.1
YaST Printer Configuration screen.

![](img/ae8469257d2662b469f2360b3bbbe322_327_0.png)

FIGURE 9.2
Printer type definitions.

![](img/ae8469257d2662b469f2360b3bbbe322_327_1.png)

Figure 9.3 displays an example of the next screen that will appear. On this screen, you define the name users will select to gain access to the queue. The use of a good naming standard will prevent a number of lost or misdirected print jobs. This is especially important when some printers are used with special forms such as shipping labels or multipart forms.

FIGURE 9.3
Defining the print queue name and description.

![](img/ae8469257d2662b469f2360b3bbbe322_328_0.png)

After defining the human-visible characteristics of the printer, you must identify to the server what type of printer is present on the selected port. A sample of this window is shown in Figure 9.4. Each printer has specific capabilities and limitations. Selecting the appropriate printer model will ensure that CUPS can properly translate the user document into a format that can be rendered by the printer.

In Figure 9.4, a large list of manufacturers is shown in the left column. Selecting the appropriate manufacturer presents, in the right column, a list of supported models for that manufacturer. When you select the printer, you are letting CUPS know what your printer is capable of doing. Using this information, CUPS can translate various types of documents into a format compatible with your printer.

FIGURE 9.4
Defining the printer model.

![](img/ae8469257d2662b469f2360b3bbbe322_329_0.png)

After you choose the appropriate printer model, you are presented with the configuration summary page, shown in Figure 9.5. At this point, clicking the OK button saves the defined configuration into the various files used by CUPS. After the configuration is saved, the printer will become available to all the system's users. We explore the fine-tuning of queue restrictions later in this chapter. First, though, let's look at how defining a network-based printer is different.

### Adding a Network Printer

In YaST, adding a queue definition on a local server for a network printer is almost identical to setting up a local printer. The main difference encountered in selecting a network-based printer in Figure 9.2 is that the local interface selection option is replaced with a network configuration screen. For an SMB queue, you are presented with a window similar to that shown in Figure 9.6.

> **NOTE**
>
> A workgroup is a collection of machines in a Windows/Samba environment. When a system is configured, it can be placed within a specific workgroup. When you are searching the network for computers, only systems in the same workgroup will be discovered. This permits the segregation of machines based on function.

The drawback to this classification is that, unlike a domain, usernames and passwords are machine specific. Users needing access to multiple machines have to maintain their passwords separately on each.

FIGURE 9.5
The YaST edit printer configuration window.

![](img/ae8469257d2662b469f2360b3bbbe322_330_0.png)

In this configuration screen, the environment and access rights for the target queue must be defined. If required, a username and password must also be included. Because you do not want a queue access to terminate should a particular employee leave, you should configure an appropriately hardened service account in the target environment to allow printer-only access from specific hosts.

An additional consideration that must be factored in when configuring remote network printing is access for the appropriate ports through firewalls.

The remainder of the configuration for a network-attached printer is identical to that of local printers.
