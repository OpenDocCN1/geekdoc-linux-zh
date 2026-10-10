+   *   **Fedora Desktop Live CD (GNOME)** — From this single, 700MB live CD you can run a GNOME desktop Fedora 12 system. An install icon on the desktop then lets you install that desktop system to your hard disk. (This CD is included with this book.)
+   *   **Fedora Desktop Live CD (KDE)** — Fedora is showing KDE some love by offering a KDE desktop live/install CD of Fedora 12. As with the GNOME desktop, you can select the install icon to install the KDE desktop and installation to your hard disk.

The official Fedora 12 GNOME desktop CD and Installation DVD included with this book are for standard 32-bit PCs (i386). If you need media to install Fedora on PowerPC (PPC) or 64-bit PC (X86_64) computer architectures, you can download ISO images for those media either using either Bittorrent (http://spins.fedoraproject.org) or an official Fedora public mirror site (http://mirrors.fedoraproject.org). Refer to Chapter 2 for information on using and installing Fedora from these different media.

Unofficial custom spins are also available from Fedora. The term spin means a compilation of software from the Fedora software repository, combined into the form of one or more bootable images, typically to fit on a CD or DVD, that lets you either run live or install that set of software or both. There are already Fedora Live Developer, Games, Art, Xfce Desktop, Education, and Electronic Lab spins. One example is the Fedora Art Studio spin (http://fedoraproject.org/wiki/Artwork/ArtTeamProjects/FedoraArtStudio).

# Creating your own spins

The same tools that the Fedora Project uses to build packages and create live CDs and installation CDs are themselves distributed with Fedora. That means that anyone can use those tools to create their own installation package sets, and then turn those package sets into their own repositories. Using those repositories, you could then create your own CD or DVD images to later install or run live.

The Pungi project (http://fedorahosted.org/pungi) was created for Fedora to build the Fedora system itself. The pungi package contains the pungi command and related configuration files. You can use the pungi command to fashion your own installation trees that result in installable ISO images.

The Fedora Live CD project (http://fedoraproject.org/wiki/FedoraLiveCD) has produced tools for building your own live CDs from Fedora software repositories. The primary tool for creating those live CDs is called lived-cd-creator. Refer to the Live CD HOWTO (http://fedoraproject.org/wiki/FedoraLiveCD/LiveCDHowTo) for information on using lived-cd-creator.

A nice recent addition to lived-cd-creator for Fedora is that you can create kickstart files (described in Chapter 2) to direct the creation of live CDs. This means that the same format you use to automate installs with anaconda can be used to save the package list and other settings you use to create your live CDs.