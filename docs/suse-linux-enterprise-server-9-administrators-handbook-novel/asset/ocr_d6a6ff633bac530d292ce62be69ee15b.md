The solution to many of these drawbacks is to push the printer interface hardware outside the data center. This converts the short-range printer technologies discussed here into network-aware solutions.

# ## Network Printers

Network printers, as their name suggests, are accessible only through the network. Such printers are attached through various mechanisms to remote print servers. CUPS supports a number of different network protocols for accessing such printers.

A CUPS server can be configured in either a client or a server role. As a server, it can present a number of local print queues to the network for access by various clients. When configured as a client, CUPS listens to service broadcasts on the network and acquires a list of valid printer destinations.

A Linux server running CUPS also understands LPD, SMB, and IPX network protocols. In such cases, a local printer definition can be made to point to a network server’s printer using the appropriate network transport protocols. LPD can be used for accessing queues on non–CUPS-compatible Unix systems as well as a number of commercial print server appliances. The SMB protocol is used to access Samba or Windows server environments, while IPX is used by older Novell networks. In the case of SMB and IPX printing, the local configuration may require a username and password for accessing the remote queues.

# ## Adding a Local Printer

You can add printers to a server using either command-line tools or YaST. The following example shows how to add a local parallel printer to a server using YaST. In YaST, the printer configuration icon can be found under the Hardware menu option. After you select this icon, you are presented with the window displayed in Figure 9.1.

In Figure 9.1, you can see that no printers are currently defined on the server. To create a new printer definition, ensure that the Other (Not Detected) option is highlighted and click the Configure button. This brings you to the next window, as shown in Figure 9.2, where you can choose the type of printer you want to configure. In the current example, add a Canon Bubble Jet 200 to the configuration as a label printer. This device requires a parallel port connection to the host. The local interfaces are shown at the top of the list, and the network-aware protocols are grouped in the lower portion.

Because you are configuring a parallel printer, select the appropriate option shown in Figure 9.2 and click the Next button. In the next window, you can select which parallel port the printer is connected to. Because a typical server