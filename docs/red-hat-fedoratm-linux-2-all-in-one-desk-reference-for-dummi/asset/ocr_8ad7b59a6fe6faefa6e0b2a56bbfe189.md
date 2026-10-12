# File systems and sharing

The whole organization of directories and files is called the *file system*. You can, of course, manage the file system using Fedora Core. When you browse the files from the GNOME or KDE graphical desktop, you work with the familiar folder icons.

![](bbox=[0.12, 0.26, 0.22, 0.34])

A key task in caring for a file system is to back up important files. In Fedora Core you can use the `tar` program to archive one or more directories on a floppy or a Zip drive. You can even back up files on a tape (if you have a tape drive). If you have a CD burner, you can also burn a CD with the files you want to back up or save for posterity.

Fedora Core can also share parts of the file system with other systems on a network. For example, you can use the Network File System (NFS) to share files with other systems on the network. To a user on the system, the remote system’s files appear to be in a directory on the local system.

Fedora Core also comes with the Samba package, which supports file sharing with Microsoft Windows systems. Samba makes a Fedora Core system work just like a Windows file or print server.

# Network

Now that most PCs are either in a local area network or connected to the Internet, you need to manage the network as well. Fedora Core comes with a Network Configuration tool to set up the local area network. For connecting to the Internet using a modem, you use the Internet Configuration Wizard (choose Main Menu±System Tools±Internet Configuration Wizard).

If you connect to the Internet using DSL (that’s the fast Internet connection from the phone company) or cable modem, you need a PC with an Ethernet card that connects to the cable or DSL. It also means you have to set up a local area network and configure the Ethernet card. But fortunately, these steps are typically a part of Fedora Core installation. If you want to do the configurations later, you can — by using the Network Configuration tool (choose Main Menu±System Settings±Network).

Fedora Core also includes tools for configuring a *firewall*, a protective buffer that helps keep your system relatively secure from anyone trying to snoop over your Internet connection. You can configure the firewall by running the Firewall Configuration tool (choose Main Menu±System Settings±Security Level from the graphical desktop).