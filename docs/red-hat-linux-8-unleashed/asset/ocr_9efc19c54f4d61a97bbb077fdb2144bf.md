# CHAPTER 2 Preparing to Install Red Hat Linux

+   - Network File System (NFS)—You can install Red Hat Linux from a remotely mounted hard drive containing the Red Hat Linux software. To do this installation, you need to have an installed and supported network interface card, along with a boot floppy with network support. (You learn how to make boot floppies later in this section of the chapter).

+   - File Transfer Protocol (FTP)—As with an NFS install, installation via FTP requires that the Red Hat Linux software from CD-ROMs one and two be available on a public FTP server. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - Hypertext Transport Protocol (HTTP)—As with the FTP and NFS installs, installation via HTTP requires that the Red Hat Linux software from CD-ROM one and two be available on an accessible Web site. You also need an installed and supported network interface card, along with a boot floppy with network support.

+   - Installation over the Internet—If you have the bandwidth, it is also possible to install Red Hat Linux via the Internet; however, this method might not be as reliable as using a Local Area Network (LAN) because of availability and current use of Red Hat or other Red Hat mirrors.

+   - Hard drive partition—By copying the Red Hat Linux installation files from the first and second CD-ROMs, you can boot to an install using a boot disk or the DOS LOADLIN command.

> NOTE
oteric installations are possible using software via an omega zip drive, via the Parallel Internet Protocol (PLIP), and even a null-model cable supporting the Serial Line Internet Protocol (SLIP) or Point-to-Point Protocol (PPP). Browse to http://www.tldp.org and see Lamiral's PLIP Install HOWTO to see how to install Red Hat 7.0 using your PC's parallel port. Once installed, you can then upgrade to the latest Red Hat.

After booting and choosing to use either a graphical or text-based install interface, the installation procedure is nearly the same for each type of install. Chapter 3, “Installing Red Hat Linux,” walks you through a typical CD-ROM–based installation.

# Preparing to Install from a CD-ROM

Installing Red Hat Linux can be as simple as inserting the first Red Hat Linux CD-ROM into your computer's CD drive and rebooting the computer. But if you choose this method, you should first make sure that your system's BIOS is set to boot from CD-ROM.