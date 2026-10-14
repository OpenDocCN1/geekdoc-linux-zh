# The Installation Guide for Red Hat Linux 6.0

# New Boot Disks

There are now two boot disks for Red Hat Linux. One is for installing from local media (CD-ROM installs, hard drive installs) and the other is for network based installs (NFS, FTP, or HTTP). Additionally, the supplemental disk has been replaced by the PCMCIA support disk. All install methods now require only one disk, unless you need PCMCIA support during the install. If needed, you will be prompted for the PCMCIA support disk.

# Improved Package Selection Screen

Individual package selection has been improved, with collapsible and expandable tree menus to allow easy selection of packages during the installation process.

# New Authentication Configuration Screen

The Authentication Configuration screen gives you the option of enabling three different types of passwords:

+   - Enable NIS — allows you to run a group of computers in the same Network Information Service domain with a common password and group file. There are two options here to choose from:
+     - NIS Domain — this option allows you to specify which domain or group of computers your system will belong to.
+     - NIS Server — this option causes your computer to use a specific NIS server, rather than "broadcasting" a message to the local area network asking for any available server to host your system.
+   - Enable Shadow Passwords — provides a very secure method of retaining passwords for you.
+   - Enable MD5 Passwords — allows passwords up to 256 characters, rather than the standard eight.