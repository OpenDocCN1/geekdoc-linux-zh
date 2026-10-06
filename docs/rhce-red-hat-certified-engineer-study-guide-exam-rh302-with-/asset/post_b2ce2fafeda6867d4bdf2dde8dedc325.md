Before beginning the installation, have the following information handy:

- CPU: type and speed.
- Motherboard: bus types (ISA, EISA, VESA, PCI, MCA, and so on).
- Drive controllers: the type of interface and the chipset used.
- Drives: the make and model of each drive and its drive number or SCSI ID on the controller.
- System RAM: size.
- Network adapters: the make and model. For non-PCI cards, know the IRQ, DMA, and I/O ports used.
- Modems: the IRQ, DMA, and I/O ports used by an internal modem or the number of the serial port to which an external modem is connected.
- Sound cards: make and model, the IRQs, DMAs, and I/O ports used.
- Serial and parallel ports: the IRQs and I/O ports used.
- Mouse: type (serial, PS2, or bus) and number of buttons. For a serial mouse, know the number of the serial port to which it's connected.
- Video card: make, model, chipset, amount of RAM, and color depths supported.
- Monitor: make, model, horizontal sync range, and vertical sync range.

You should have similar information for any other hardware devices installed in the system.
If your system is attached to a network, you should have the following information available:

- Method of IP address assignment: static, DHCP, BOOTP.
- IP address
- Netmask
- Gateways
- Fully qualified domain name (FQDN)

For statically defined hosts, you should have the following information available:

In some circumstances, additional information will be needed. But, generally, this information will be enough to let you complete the installation procedure. Once the installation procedure is complete, you can configure special options as needed.

In addition to information on the hardware of the target system, you should have available the Red Hat Linux Installation Guide and other Linux documents, particularly the HOWTOs. If necessary, you can use any Linux system or a Microsoft Windows system to read documentation stored on the documentation CD-ROM or to access Web sites and newsgroups that provide pertinent information. Having this information available will help you complete the installation procedure; otherwise, you may find it necessary to terminate the installation procedure, obtain the needed information, and then restart the installation.

## Selecting the Installation User Interface

Red Hat Linux supports two installation types: Install and Upgrade. You should choose Install when installing Linux on a target system that doesn't currently host Red Hat. Choose Upgrade when the system already hosts an earlier version of Red Hat Linux. The Upgrade procedure saves the existing configuration files, rather than overwriting them. The existing files are renamed with the extension .rpmsave.

Red Hat Linux 6.1 introduced a graphical mode installation procedure based on X. The initial screen of the installation procedure lets you choose the graphical mode installation procedure or a text mode installation procedure. Beginners generally find the graphical mode installation procedure easier to use. However, you may prefer the text mode installation for the following reasons:

- The graphical mode installation procedure may fail if the target system has unusual video characteristics, such as an old or uncommon video adapter.
- The text mode installation procedure can recover from some errors—such as running out of disk space—that cause the graphical mode installation procedure to fail.
- The text mode installation will run better and faster than the graphical mode installation on computers having a slow processor or a small amount of RAM.
- The graphical mode installation supports only media mounted as a file system, such as an existing drive partition, a CD-ROM, or media available via NFS.

## Selecting the Installation Class

The Red Hat Linux installation procedure provides three default installation classes or configurations:

- GNOME Workstation
- KDE Workstation
- Server

The workstation classes are a quick way to get a Red Hat Linux system up and running. Both workstation classes install the most commonly used packages. In addition, the GNOME Workstation class installs the GNOME desktop manager, and the KDE Workstation class installs the KDE desktop manager.

The workstation classes are particularly useful for building a dual-boot system, because they disturb no non-Linux partitions as long as sufficient unallocated disk space is available. They do, however, delete all existing Linux (ext2) partitions. They establish three standard partitions:

- 64MB swap partition
- 16MB boot partition (/boot)
- A root partition (/) that uses the remaining free disk space

Both workstation classes require about 600MB of free disk space. In contrast to the workstation classes, the Server installation class deletes all existing partitions, including DOS/Windows partitions. The Server installation class requires about 1.6GB of disk space. By default, a Server installation lacks the following components, which are included in one or the other of the work-station installations:

- Author/Publishing
- DOS/Windows connectivity
- GNOME or KDE
- Graphics manipulation
- Multimedia support
- X Window system

However, a Server installation includes the following components, which are not included in one or the other of the workstation installations:

- Anonymous FTP server
- DNS name server
- IPX/NetWare connectivity
- NFS server
- Network management workstation
- News server
- Postgres (SQL) server
- SMB (Samba) server
- Web server

A Server installation creates a more elaborate partition structure, including:

- 64MB swap partition
- 16MB boot partition (/boot)
- 256MB root partition ( /)
- 256MB /var partition

Two further partitions split the remaining free disk space equally:

- /home
- /usr

If neither the workstation classes nor the Server installation class meets your needs, you can specify a Custom installation. The Custom installation class has no predefined characteristics. You can partition hard drives and install components and packages as you choose.

## Partitioning the Hard Disk

If you select either the workstation installation classes or the Server installation class, the installation procedure partitions your hard drive automatically. However, if you select the Custom installation class, you must partition the hard disk.

Partitions improve system data integrity and can improve system security. If a hard disk suffers damage, the damage is often confined to a single partition. Recovery of a single partition may be simpler and quicker than recovery of an entire drive. It's also possible to mount partitions as read only. By organizing data that need not to be changed as a partition and mounted as read only, data integrity and security can be improved. A partition that cannot be written is less vulnerable to corruption than one mounted for reading and writing.

In designing a partition structure, the following directories should be kept in a single partition:

- /
* /etc
* /lib
* /bin
* /dev

These directories—and their subdirectories—contain programs and files essential to proper system operation. They should always be present and therefore be of the so-called root partition, mounted as /.

The non-Custom installation classes create a 16MB boot partition, mounted as /boot. Generally, your design should include such a partition. By locating a boot partition within the 1024-cylinder region that is addressable by the system's BIOS, you ensure that the kernel will be accessible at boot time.

Generally, you should include one or more swap partitions. As a rule of thumb, the swap partitions should have a total size that is 2–3 times of the installed RAM. For example, a system having 16MB of RAM should have 32–48MB of swap space. No more than eight swap partitions can be defined; the total swap space cannot exceed 4GB.

Directories that are often made points of separate partitions include:

- /home
- /opt
- /tmp