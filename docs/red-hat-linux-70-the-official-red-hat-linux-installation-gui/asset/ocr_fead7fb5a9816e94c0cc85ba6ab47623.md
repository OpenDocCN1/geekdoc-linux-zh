# E.1.4 Trouble Booting from a Network Boot Disk?

If you are experiencing difficulties in getting the network boot disk you made to boot your system correctly, you may need an updated boot disk.

Check the online errata for updated diskette images and follow the instructions provided to make a new boot disk for your system.

# E.2 Trouble Beginning the Installation

# E.2.1 Trouble Using Options Needed with a PCMCIA Boot Disk?

If you booted using a PCMCIA boot disk and want to install via FTP (or NFS or HTTP), but do not see these installation options, you may have a problem with your network card.

If the network card is not initialized during the boot process, the Red Hat Linux installation program will *not* enable you to configure your system for networking (either at boot time or during the installation itself).

Check the hardware compatibility list (http://www.redhat.com/support/hardware) to see if your network card is compatible and/or supported. If your card is not listed, chances are it is not compatible with Red Hat Linux.

# E.3 Trouble During the Installation

# E.3.1 Trouble Getting the Automatic Partitioning Screen?

If the **Automatic Partitioning** screen does not appear during your installation, you probably do not have enough free space in which to install Red Hat Linux.

If you do not want to partition manually, you should exit out of the installation, which can be done by rebooting your system once you have removed any diskettes or CD-ROMs, and then you can reallocate space for your installation.

# E.3.2 Trouble Creating Partitions?

If you are having trouble creating a partition, for instance a root (\ /) partition, there are a couple of things you should be aware of.

Make sure you are setting it as a Linux Native partition type.