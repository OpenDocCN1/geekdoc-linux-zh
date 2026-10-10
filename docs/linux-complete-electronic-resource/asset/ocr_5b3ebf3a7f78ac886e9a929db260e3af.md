# DECNat

Support for DECNet is currently being worked on. You should expect it to appear in a late 2.1.* kernel.

# FDDI

FDDI device names are `"fddi0"`, `"fddi1"`, `"fddi2,"` etc. The first card detected by the kernel is assigned `"fddi0,"` and the rest are assigned sequentially in the order they are detected.

Larry Stefanici \ <stefani@ultranet.com> has developed a driver for the Digital Equipment Corporation FDDI EISA and PCI cards.

# Kernel Compile Options:

+   Network device support \----
+   \[*] FDDI driver support
+   \[*] Digital DEFA and DEFA adapter support

When you have your kernel built to support the FDDI driver and installed, configuration of the FDDI interface is almost identical to that of an Ethernet interface. You just specify the appropriate FDDI interface name in the ifconfig and route commands.

# Frame Relay

The Frame Relay device names are `"dlci00"`, `"dlci01,"` etc. for the DLCI encapsulation devices, and `"sdlao,"` `"sdla1,"` etc. for the FRAD(s).

Frame Relay is a new networking technology that is designed to suit data communications traffic that is of a "bursty" or intermittent nature. You connect to a Frame Relay network using a Frame Relay Access Device (FRAD). The Linux Frame Relay supports IP over Frame Relay as described in RFC-1490.

# Kernel Compile Options:

+   Network device support \----
+   <> Frame relay DLCI support (EXPERIMENTAL)
+   (24) Max open DLCI
+   (8) Max DLCI per device
+   <> SDLA (Sangoma S502/S508) support

Mike McLagan <mike.mc.lagan@linux.org> developed the Frame Relay support and configuration tools.