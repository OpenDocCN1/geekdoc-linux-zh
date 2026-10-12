SLIP is the ancestor of PPP, and although 99.9% of all ISPs will only offer PPP connections, SLIP still has some viable uses. SLIP is an essential ingredient as an intermediary device in the diald demand dialer or to gain a network connection over a telnet session (using SLIRP).

# Amateur Radio and Wireless Support

Another low-cost Internet solution for impossible remote locations is the Amateur Radio Support. By encoding packets over short-wave radio, Linux systems have been used to provide as much as 64Kb of symmetric bandwidth over long distances. For examples of packet radio in action, see the Wireless Papers (http://www.ictp.trieste.it/~radionet/papers) or visit the Packet Radio home page (http://www.tapr.org/tapr/html/pkthome.html).

A related feature of interest to campus and rural development projects is the kernel support for Wireless LAN, AT&T WaveLAN, and DEC RoamAbout DS (see Documentation/networking/wavelan.txt). There is also support for the MosquitoNet (http://mosquitonet.stanford.edu) StarMode RadioIP systems used by many laptop owners.

# IrDA: Infrared Port Device Drivers

Infrared Data Associations protocols provide wireless infrared communications between laptops and PDAs at speeds up to 4Mbps, and the Linux driver makes supported devices transparent to the networking system. More information on this support, and on the utility programs for IrDA, can be found at the Linux Documentation Project (http://www.linuxdocs.org) or the Linux IrDA home page (http://www.cs.uiz.no/linux-irda/).

# ISDN Subsystem

To use ISDN, you must obtain the isdn4k-utils utility programs (ftp://ftp.franken.de/pub/isdn4linux). When the module is loaded, isdn.o can support up to 64 channels (you can add more by changing the isdn.h file directly). Each channel will be given read/write access to the D-Channel messages and iocli functions, with non-synchronized read/write to B-Channel and I28 tty-devices. Modem emulation provides a standard AT-style command set compatible with most dialup tools, such as minicom, pppd, and mgetty.

The second step in configuring for ISDN is to select your specific ISDN modem card. Some ISDN cards will require initialization before the vendor-independent setup. Details can be found in the appropriate README file under linux/Documentation/isdn.

![](bbox=[0.92, 0.29, 0.97, 0.46])