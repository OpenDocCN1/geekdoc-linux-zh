If after installation you decide to add or remove hardware from your computer, there is a tool that will allow you to reconfigure your hardware when the system boots up. See the sidebar describing kudzu for detecting and configuring new and changed hardware.

# Reconfiguring Hardware at Boot Time with kudz u

Sometimes as Red Hat Linux is booting up, you may want to make changes to the system configuration. You may have added a new piece of hardware (or removed one). You may want to turn off a particular system service because it is hanging during the boot. With kudz u, you can change hardware and service configurations as your computer is booting.

To enter kudz u while Red Hat Linux is booting, look for a message on the screen that says "Press 'l' to enter interactive startup." Press l and you will be prompted to enter interactive startup. The kudz u Hardware Discovery Utility will check for hardware that has been removed or added and allow you to add or remove configuration for the hardware or do nothing.

When all the new or changed hardware has been reconfigured, you are prompted to start service reconfiguration. Type Y and you will be stepped through each service that is configured to start at boot time. This is an excellent way to temporarily turn off a service that is hanging your system or that is no longer needed.

# Special Installation Procedures

If you don't want to, or can't, use the procedure to install Red Hat Linux from CD, the procedures in this section give you alternatives. The first procedure tells how to install Red Hat Linux from alternative media (using FTP, HTTP, NFS, or hard disk installs). The next procedure describes how to do kickstart installations.

# Installing from other media

Your CD-ROM drive may not be working, you may not have a CD-ROM drive, or maybe you just want to install a new version of Red Hat Linux that is available from another computer on the network. In any of these cases, Red Hat will let you install Linux from a Web server (HTTP), an FTP server, a shared NFS directory, or local hard disk.

**NOTE:** To use HTTP, FTP, or NFS installations, your computer must be connected to a LAN that can reach the computer containing the Red Hat Linux distribution. You cannot use a direct dial-up connection. For a local hard disk install, the distribution must have been copied to a local disk that is not being used for installation. See the section "Setting up an install server" for details on copying the distribution and making it available.