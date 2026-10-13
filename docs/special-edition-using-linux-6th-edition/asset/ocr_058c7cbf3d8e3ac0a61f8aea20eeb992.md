> **Caution**
> 
> Hardware is available for 100MB and 1000MB networking if you are interested. Be careful about mixing bandwidths if you are using a hub, though; if you have 10Base-T or 10Base-2 (or 10Base-T/2) cards, do not purchase a 100Mb hub to connect them. Mixing bandwidths in this manner does not work without special, expensive switching hubs. If you plan on eventually moving to a 1000 network, it might be cheaper in the long run for you to simply go 100MB right from the start.

# ASSUMPTIONS

The following sample network consists of five computers: four PCs running various operating systems (including Windows NT and Linux) and one Mac. All are connected using 10Base-T/2 Ethernet cards through a small 10Base-T hub with twisted-pair cabling (see Table 30.1).

**Table 30.1 — Assumptions for Your Sample Network**

| Computer Name | IP Address | Type | O/S Used |
|---|---|---|---|
| rumble.fish.net | 192.168.1.1 | PC | Linux |
| geoffie.fish.net | 192.168.1.2 | PC | Windows 95 |
| go.fish.net | 192.168.1.3 | PC | Windows NT |
| silver.fish.net | 192.168.1.4 | Apple | System 7.5 |
| tuna.fish.net | 192.168.1.5 | PC | Linux |

*fish.net is being used as an example only. If your network is going to be connected to the Internet, please register your own domain and do not use fish.net. Of course, if fish.net is not taken...*

All systems are connected using TCP/IP, plus various other protocols that allow the connection of networked drives. For the sake of brevity, only the TCP/IP setup is addressed here. Also for the sake of brevity, it is assumed that the names of the Linux systems were assigned when the systems were installed. For the Windows and Mac systems, the assumption is made that they already have names as well.

Each system has the equivalent of a hosts file that contains all the preceding addresses plus the localhost address. A DNS server can work on this network as well, providing not only local resolution, but also Internet resolution and saving you the trouble of putting hosts files in each system. You could also assign a static IP to rumble.fish.net, configure a DHCP server on it, and let the other systems get their IP address through DHCP. Each additional step will require more initial effort on your part, but for larger networks, it is definitely worth the trouble.

The format of the hosts file is consistent across the various platforms. Each one will resemble Listing 30.1.