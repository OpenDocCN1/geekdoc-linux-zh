# Installing from other media

Once the installation process has booted from DVD, CD or as described in the previous section), Fedora will let you get the actual packages that are to be installed from a Web server (HTTP), an FTP server, a shared NFS directory, or local hard disk.

> **NOTE:** To use HTTP, FTP, or NFS installations, your computer must be connected to a LAN that can reach the computer containing the Fedora distribution. You cannot use a direct dial-up connection. For a local hard disk install, the distribution must have been copied to a local disk that is not being used for installation. See the section “Setting up an HTTP, FTP, or NFS install server” for details on copying the distribution and making it available.

# Beginning installation

You can use the DVD that comes with this book (or an alternative method described in the previous section) to start a network or hard disk install.

> **NOTE:** For earlier Red Hat and Fedora Core distributions, you could use a floppy disk to boot the install process. Because the 2.6 kernel is too large to fit on a floppy disk, however, this method of starting installation is not supported for Fedora Core 2 or later versions.

+   1.  Insert the Fedora installation DVD into the DVD drive.
+   2.  Reboot the computer. You should see the Fedora boot screen.
+   3.  Start askmethod. Type the following at the boot prompt:
+       
+       `boot: linux askmethod`
+       
+       You are prompted to select a language.
+   4.  Select the language. You are prompted to choose a keyboard type.
+   5.  Select your keyboard type. You are prompted to select an installation method.
+   6.  Choose the installation method. Select any of the following installation methods: Local CDROM, NFS image, FTP, HTTP, or hard drive.
+   7.  Configure the network card. For any of the network installs, you are asked to select your Ethernet card from the list shown. (This may be detected automatically.) If your card is not on the list, you need to obtain a driver disk that contains the driver needed by your network card.

> **NOTE:** The Fedora project does not currently offer a driver disk, so you need to obtain the appropriate driver on your own.

+   8.  Configure TCP/IP. For any of the network install types (NFS, FTP, and HTTP), you are prompted to configure TCP/IP for your computer. (See the section on configuring networking earlier in this chapter for information on how to add to these fields.)