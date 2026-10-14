# Netware Emulation with MARSNWE

The Netware emulator MARSNWE can easily replace the file and print services of a Novell Netware 2.2 or 3.11 server. It can also be used in this manner as an IPX router. However, it does not offer the features of newer Netware versions, such as NDS (Netware Directory Services). Workstations running DOS or Windows already configured to access a Netware 2.2, 3.11, or 3.12 server can use the Linux server with the Netware emulator MARSNWE as a server without having to change the configuration much. Administration is best taken care of in Linux, because Novell system administration applications can only be utilized under certain conditions and have licensing issues as well.

# Starting the Netware Emulator MARSNWE

MARSNWE in SuSE Linux can be started immediately after installation, because it is already preconfigured for initial testing. The required IPX support on the part of the kernel is available as a loadable kernel module and is automatically loaded by the start script. The IPX interface is automatically set up by MARSNWE. At this point, the network number and the protocol to use will both be read from the extensively commented configuration file `/etc/nwserv.conf`. MARSNWE is started via the command `rcnwe start`. The done message to the right of the screen in green indicates that MARSNWE has been successfully started. Use `rcnwe status` to check whether the Netware emulator is running. Halt it with `rcnwe stop`.

# The Configuration File /etc/nwserv.conf

The configuration options are summarized in enumerated sections. Every configuration starts with the number of the corresponding section. Only sections 1 to 22 are relevant here. Not all numbers are used, however. Most of the time, the following sections are enough for the configuration:

+   1  Netware Volumes
+   2  Server Name
+   4  IPX Network
+   13 User Names
+   21 Printers

After modifying the configuration, MARSNWE must be restarted with the command `rcnwe restart`.
The configuration options in detail: