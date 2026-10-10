quickly recover a system. Many modern notebooks have internal hard drives with more than enough storage to hold the contents of a dozen or more CD-ROMs. For some mobile Linux users, there's some degree of comfort in knowing that a fresh installation can be performed in a matter of minutes, or that additional software can be quickly installed from the main distribution tree. Keeping a simple DOS partition with your distribution's contents can be handy, especially if you don't install everything included on your distribution's CD-ROM.

# # Network Installation

If your notebook does not have an internal CD-ROM, but you have access to a LAN, you can install Linux over the network in a variety of ways. You'll need to use the PCMCIA boot disk unless your notebook has an internal Ethernet port, in which case you can try to use the BOOTNET.IMG floppy to boot to your installation. Create your boot disk, make sure your notebook is attached to a LAN, and reboot. Page through the initial Red Hat dialog boxes until you come to the Installation Method dialog box, shown in Figure 4.5.

Scroll through the list of types of installation, and then use the spacebar to choose an install to match your NFS-exported, FTP-mounted, or HTTP-available Linux install distribution. When finished, press Enter to start the install process.

![](bbox=[0.19, 0.63, 0.91, 0.89])

**Figure 4.5** When installing Linux using a network, choose the type of installation, and then press Enter.