| **Table 21.1. Solaris 8 Software Groups (continued)** | |
|---|---|
| **Software Group** | **Contents** |
| Entire Distribution Plus OEM System Support | Includes modules and drivers for optional hardware components. Consists of the Entire Distribution software group plus:<br>PCI drivers<br>SunFastEthernet and FastWide SCSI adapter drivers |

# # Over-the-Network Installation

Typically, Solaris is installed directly from the Solaris distribution CD, which requires that each system be equipped with a CD-ROM drive. However, another approach is available: Solaris can be installed over the network by using a remote server that has the Solaris distribution CD in its CD-ROM drive or a copy of the files from the Solaris distribution CD on its hard disk.

The over-the-network installation can be used with the two interactive installation methods (SunInstall or Web Start, covered in Chapter 3) or the two automatic installation methods (JumpStart and Custom JumpStart).

To perform over-the-network installation, you must set up one or more network servers, consisting of an install server and possibly a boot server. In addition, you must add information about the install clients in the local NIS or NIS+ name service or in the /etc files of the appropriate install servers.

# # Install Server

An *install server* is a system that provides the distribution files needed to install the Solaris operating system on an install client during an over-the-network installation. The files can be provided directly from the Solaris distribution CD mounted in a local CD-ROM drive or from a local hard disk.

If you copy the distribution files to a local hard disk, a single install server can be used to provide the files for multiple releases (Solaris 8, Solaris 7, Solaris 2.6, and so on) and/or for multiple platforms (SPARC and Intel x86). In addition, a local hard disk typically provides faster access to the distribution files than a local CD-ROM drive.

To set up a system as an install server, mount the Solaris 8 Software (1 of 2) distribution CD in the local CD-ROM drive. Then use the **setup_install_server** command, under the Solaris_8/Tools directory on the Solaris distribution CD, to copy the distribution files to the install server’s