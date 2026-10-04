
- Java VM (capability to develop Java applications)
- OS demo code
- Power Management GUI tools
- Online manual pages
- Solaris 1.x compatibility tools
- Kernel probing support (TNF)
- Extended language and partial locale support
- Programming tools and libraries
- Extended terminal support (terminfo)
- Extended X support (XGL, XIL, XCU4)
- Graphics header (for graphics application development)
- ISO 8859 required fonts

Entire distribution, 608MB. Contains the end-user and developer software plus the following:

- AnswerBook2 (online documentation)
- Full audio tools and demos
- Enhanced security
- UUCP networking (UNIX-to-UNIX copy)
- DHCP server (Dynamic Host Configuration Protocol)
- Additional language and partial locale support (Eastern European)
- Additional hardware support (Leo, SX/CG14, SunVideo, SunButtons, SunDials, TCX)
- Enhanced networking support (NIS server, point-to-point protocol)
- Solstice Launcher
- System recovery tools
- Additional X features (complete fonts, PEX)
- ISO 8859 optional fonts

Entire distribution plus OEM system support, 616MB. Contains the end-user, developer, and entire distribution software plus extended hardware support, which includes the following:

- Voyager drivers and modules
- sun4u (X server modules, VIS/XIL)
- SunFastEthernet/FastWide SCSI adapter drivers
- PCI drivers
- M64 graphics accelerator
- A-10 (PFU) and Fujitsu device drivers and system support

## Methods for Installing Solaris Software

You can use one of four methods to install the Solaris software: Interactive, Custom JumpStart, Web Start, and installation over the network.

### Interactive

The Solaris Interactive Installation program guides you step by step in installing the Solaris software. The Solaris Interactive Installation program does not enable you to install all of the software (Solaris software and co-packaged software) in your product box at once; it only installs the SunOS software. After you install the Solaris software, you have to install the other co-packaged software by using the co-packaged installation programs.

### Custom JumpStart

This method, formerly called Auto-Install, enables you to automatically—and identically—install many systems with the same configuration without having to configure each of them individually. JumpStart requires up-front setup of configuration files before the systems can be installed, but it's the most cost-effective way to automatically install Solaris software for a large installation.

All new SPARC-based systems have the JumpStart software (a pre-installed boot image) pre-installed on its boot disk. JumpStart enables you to install the Solaris software on a new SPARC-based system just by inserting the Solaris CD into the system and powering on the system. You can install the JumpStart software on existing systems by using the `re-preinstall` command.

> **NOTE.** On a new system shipped by Sun, the install software is specified by a default profile that is based on the system's model and the size of its disks; you don't have a choice of the software that gets installed. Make sure this JumpStart configuration is suited to your environment. The system loads the end-user distribution group and sets up minimal swap space. Partitions and their sizes are set up by using default parameters that might not be suitable for the applications you plan to install.

When might you want to use JumpStart? For example, suppose you need to install the Solaris software on 50 systems. Of these 50 systems to be installed, 25 are in engineering as standalone systems with the entire distribution software group and 25 are in the IS group with the developer distribution software group. JumpStart enables you to set up a configuration file for each department and install the OS identically on all the systems. The process facilitates the install by automating it and ensures consistency between systems.

### Web Start

Solaris Web Start is Sun's browser-based "virtual assistant" for installing software. Using Solaris Web Start and Sun's Web browser, you select either a default installation or a customize option to install only the software you want, including the Solaris software group, Solstice utilities, and other co-packaged software. From Sun's Web browser, an installation profile is created that is used by Solaris JumpStart to install the Solaris software and the other selected software products with minimal intervention. Web Start simplifies the creation of the JumpStart configuration file.

### Installing Over the Network

Because the Solaris software is distributed on a CD, a system has to have access to a CD-ROM drive to install it. However, if you don't have a local CD-ROM, you can set up the system to install from a remote CD or CD image on a remote disk drive. The remote Solaris CD image must be provided by an install server that has either the Solaris CD copied to its hard disk or the Solaris CD mounted from its CD-ROM drive. Installing the OS across the network is handy when a local CD-ROM is not available.

### The Solaris Installation Process

Solaris is installed by using the Solaris Install tool—a GUI that is friendly and easy to use. The installation brings up various menus and asks for your input. The tool enables you to go back to previous screens if you make a mistake, and it doesn't actually do anything to your system until the install program gets to the end and tells you it is about to start the loading process. During the installation, help is always available via the Help button.

> **CAUTION!** The following procedure reinstalls your operating system. This means it destroys all data on the target file systems.

If you're upgrading or installing Solaris on a new system, shut down the system. Then use the following steps to complete the installation:

1. Become root.
2. Issue the shutdown command. This command brings the system to a single-user state by halting the window system and leaving you with a single root prompt on the console. It takes about a minute.
3. Issue the halt command. This command puts you into the PROM. You'll know you're in the PROM when you receive either an ok or a > prompt.
4. Put the Solaris installation CD into the CD player and boot from the CD. The correct way to do this depends on your system type. If the screen displays the > prompt instead of the ok prompt, type n and press Enter.
5. At the ok prompt, type boot cdrom.

> NOTE. On Sun systems with older EEPROMs, the process of booting from CD is different. For your particular system, boot to the CD-ROM as follows:
For a Sun 4/1nu, 4/2nu, 4/3nu, or 4/4nu system, type b sd(0,0,0,1).
For a SPARCstation 1/4(60), 1+(4/65), SLC(4/20), or IPC(4/40) system, type boot sd(0,6,2).

The system boots from the CD-ROM. The process is slow, but the flashing light on the CD player shows activity. Eventually the system starts the GUI and presents you with the Solaris Installation program. Follow the instructions on the screen to install the software on the system. Have the following information available; the installation tool will ask for it:

- **Hostname**—The name for the system. Hostnames should be short, easy to spell, lowercase, and have no more than 64 characters. If the system is on a network, the hostname should be unique.
- **IP address**—This information must come from your site IP coordinator. 192.9.200 is one example of an IP address. IP addresses must be unique for every system on your network. For a large site, or a site that has a presence on the Internet, you should apply for a unique IP address from the NIC to ensure that no other network shares your address.
- **NIS or NIS+**—You'll need to specify which your system will be using.

When the installation program is finished gathering information, it asks you if it's okay to begin the installation. When the installation is complete, you are asked to supply a root password. Make sure you complete this step and supply a secure password.

This completes the installation of the Solaris operating system. Other chapters in this book will discuss post-installation procedures such as setting up print queues, adding users, and setting up a backup procedure.
