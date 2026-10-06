# Chapter 9 - Configuring the System with YaST

XML files allow for a very high degree of detailed control over the installation of the particular machine: Different machines can have different specific XML control files. Essentially, the XML file contains an answer to every question that the installer asks the user in an interactive installation.

# Mode of Operation

The machine that is being installed has to be booted seamlessly. The possibilities are to boot it from a floppy disk, from a bootable CD-ROM, or by PXE network booting.

+   - SUSE uses a GRUB boot floppy for starting an installation that is capable of network booting in conjunction with a Trivial FTP (TFTP) or Dynamic Host Protocol (DHCP) server.
- Alternatively, the system can be booted from an installation CD, but can be given a boot parameter as `install-https://192.168.1.1/install/`. If a DHCP server is available, the machine obtains an IP address and finds the installation files from the information given at boot time. This information can also be placed in an file held on a floppy disk to be read at the start of the installation.
- The most elegant method, if it is available, is PXE booting (supported by most modern hardware). In this case, little more is needed on the installation server: You need to run a DHCP server and a TFTP server together with the special files (from the package pxe) required to start the boot process. The DHCP server offers an IP address based on the client's hardware address; the TFTP server then gives a file based on the IP address, which references the XML installation control file on the server.

In any of these cases, when the installer has booted and opened the relevant XML file, the XML file controls the rest of the installation as if a human interacts with the installer.

The installation server can offer the installation files by HTTP, NFS, or FTP. In the case of SUSE Professional, it is sufficient that the contents of the installation CDs and DVD (or a mirror of the installation set on the FTP site) be available by one of these methods.

# YaST Autoinstallation Module

The purpose of this module is to help you create the AutoYaST XML control file. You can start the module with:

```
# yast2 autostart
```

or by selecting the icon in the YaST Misc section (the one with the wonderful pineapple icon). When you start the module you will see a screen like Figure 9-38.