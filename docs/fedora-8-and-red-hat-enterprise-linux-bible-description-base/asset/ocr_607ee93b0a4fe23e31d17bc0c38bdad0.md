# Booting installation using PXE

Another method to begin Fedora installation is to use Pre-eXecution Environment (PXE). With PXE, the installation process begins by setting the BIOS of your computer to look on the network for a PXE server to boot from. For information on how to do a PXE install, refer to `/usr/share/doc/syslinux-*/pxelinux.doc`. For the PXE install server, you can use the kernel and initrd images from the `images/pxeboot` directory on the Fedora DVD. You need to be able to set up a DHCP server and Tftp server to complete this procedure. Then you can get the Fedora installation files from any of the media types described in the next section.

# Installing from other media

Once the installation process has booted (from DVD, as described in the previous section), Fedora will let you get the actual packages that are to be installed from a Web server (HTTP), an FTP server, a shared NFS directory, or local hard disk.

> **NOTE:** To use HTTP, FTP, or NFS installations, your computer must be connected via an Ethernet connection to a network that can reach the computer containing the Fedora distribution. You cannot use a direct dial-up connection. For a local hard disk install, the distribution must have been copied to a local disk (or separate disk partition) that is not being used for installation. See the section “Setting up an HTTP, FTP, or NFS install server” for details on copying the distribution and making it available.

# Beginning installation

You can use the DVD that comes with this book (or an alternative method described in the previous section) to start a network or hard disk install.

> **NOTE:** For earlier Red Hat and Fedora distributions, you could use a floppy disk to boot the install process. Because the 2.6 kernel is too large to fit on a floppy disk, however, this method of starting installation is not supported for Fedora Core 2 or later versions.

+   1. **Insert the Fedora installation DVD into the drive.**
+   2. **Reboot the computer.** You should see the Fedora boot screen.
+   3. **Start askmethod.** Press Tab with the first entry on the boot screen highlighted and add the following to the end of the boot prompt:
+   
+   ```asmethd```
+   
+   You are prompted to select a language.
+   4. **Select the language.** You are prompted to choose a keyboard type.
+   5. **Select your keyboard type.** You are prompted to select an installation method.
+   6. **Choose the installation method.** Select any of the following installation methods: Local CDROM, NFS image, FTP, HTTP, or Hard drive.