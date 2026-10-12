
## Enabling Authentication

In most situations, you will enable shadow passwords and MD5 passwords (as selected by default) to authenticate users who log in to your computer from local `passwd` and `shadow` password files. To change that behavior, you can select the Use Network Login button during the User Account setup during Fedora Setup Agent (`firstboot`).

The shadow password file prevents access to encrypted passwords. MD5 is an algorithm used to encrypt passwords in Linux and other UNIX systems. It replaces an algorithm called crypt, which was used with early UNIX systems. When you enable MD5 passwords, your users can have longer passwords that are harder to break than those encrypted with crypt.

If you are on a network that supports one of several different forms of network-wide authentication, you may choose one of the following features:

- **Configure NIS.** Select this button and type the NIS Domain name and NIS server location if your network is configured to use the Network Information System (NIS). Instead of selecting an NIS Server, you can click the check box to broadcast to find the server on your network. For more information on NIS, see Chapter 23.
- **Configure LDAP.** If your organization gathers information about users, you can click this button to search for authentication information in an LDAP server. You can enter the LDAP Server name and optionally an LDAP distinguished name to look up the user information your system needs.
- **Configure Hesiod.** If your organization uses Hesiod for holding user and group information in DNS, you can add the LHS (domain prefix) and RHS (Hesiod default domain) to use for doing Hesiod queries.
- **Configure Kerberos Support.** Click this button to enable network authentication services available through Kerberos. After enabling Kerberos, you can add information about a Kerberos Realm (a group of Kerberos servers and clients), KDC (a computer that issues Kerberos tickets), and Admin server (a server running the Kerberos kadmind daemon).
- **Configure SMB.** Click this tab to configure your computer to use Samba for file and print sharing with Windows systems. If you enable SMB authentication, you can enter the name of the SMB server for your LAN and indicate the Workgroup you want your computer to belong to.
- **Install Additional Software** — If you have a Fedora CD other than the four installation CDs or the DVD that comes with this book, you can install it now. Insert the CD you want to install and clicking the appropriate button.

The Fedora Setup Agent is complete. Click Finish to continue. See Chapter 3 for a description of how to log in to Fedora and start learning how to use Linux.

When Fedora starts up the next time, it will boot up normally to a login prompt. A graphical boot screen is displayed (instead of a scrolling list of services starting up). If you miss the old scrolling list, you can view it by clicking the Details button or by pressing Ctrl+Alt+F1. Then go back again by pressing Ctrl+Alt+F8.

## Installing More Fedora Packages

Unless you did an Everything install, as you go through this book you will probably find that you want to add some Fedora software packages later. To do that, you can use rpm (described in Chapter 5), a general-purpose command for installing any software packages in RPM format. Or you can use the Package Management window (system-config-packages), which provides the same interface for installing packages that was used in the original installation procedure.

To open the Package Management window, select System Settings → Add/Remove Applications from the main menu on the desktop (or type `system-config-packages` from a Terminal window). The window appears, as shown in Figure 2-1.

![](img/b22364e57409c2481ba806e4e6b9309c_63_0.png)

Scroll through the major package groups using the scroll bar. After the name and description of each group there is a set of numbers in brackets that shows how many packages are in the group and how many of those are actually installed. Click Details to see the listing of all packages in the group.

The details of each group shows the standard packages in each group (ones that are required if the group is installed at all) and ones that are extra. To add or remove packages from your system, click the check box next to the package so that it is on or off, respectively. Repeat this for each package group, and close the details window.

When you have made all your add or delete selections, click Update on the main Add and Remove Software window. Insert the DVD or CD as it is requested. Packages will be added or removed, as you requested.

## Special Installation Procedures

If you don't want to, or can't, use the procedure to install Fedora Core from DVD, the procedures in the following sections give you alternatives. The first subsection describes alternate ways of booting the installation, such as PXE (if your computer doesn't have a bootable DVD or CD drive).

After the install procedure boots, use the “Installing from other media” section that follows to learn how to install Fedora from media other than DVD or CD-ROM (using FTP, HTTP, NFS, or hard disk installs). If you want to have the installation screens appear on another computer as you install, refer to the “Starting a VNC install” section. The subsection following that describes how to do kickstart installations.

### Alternatives for starting installation

Your computer may not have a DVD or CD drive or may have one that is unbootable, so, you need to find an alternative way to boot the install process. Although booting installation from 1.44 floppy disks is no longer supported (the 2.6 kernel won't fit on one), you have a few other alternatives:

- Boot installation from hard disk
- Boot from a USB pen drive or other USB device
- Do a PXE install

Procedures for starting installation in those two ways are described in the following sections.

### Booting installation from hard disk

Booting the install process is similar to booting a regular Linux system. To start an install from your hard disk all you really need to do is:

- Put the files needed to boot installation on your hard disk.
- Configure your boot loader to tell your computer’s master boot record about those installation files.

This procedure presumes that there is already a Fedora or Red Hat Linux system running on the system (so you are doing an upgrade or a fresh install of Fedora). It also presumes that you can find a way to get those files on to the hard disk (I’ll describe how to do that from a DVD or CD that can be mounted even if it can’t be booted).

> **NOTE:** See the section earlier in this chapter on setting up install servers, since presumably you need the contents of the Fedora installation DVD accessible from somewhere other than the DVD itself.

1. Insert the Fedora Core 3 DVD into the DVD drive while Fedora or Red Hat Linux is running.

2. If the DVD isn’t automatically mounted, as root user type the following to mount it:
    ```bash
    # mount /media/cdrecorder
    ```

3. Copy the vmlinuz and initrd files from the installation DVD to your boot directory:
    ```bash
    # cd /media/cdrecorder/isolinux
    # cp initrd.img /boot/initrd-boot.img
    # cp vmlinuz /boot/vmlinuz-boot
    ```

> **NOTE:** If you are not able to mount a DVD or CD on the machine, you could copy the files from another machine on the network using scp. Or you could download those files to your /boot directory from a Fedora FTP site that contains the Fedora distribution.

4. Change your local `/boot/grub/grub.conf` file to include an entry for the vmlinuz and initrd files you just added to your boot directory. For example:
    ```text
    title Fedora Core 3 installation
    root (hd0,0)
    kernel /vmlinuz-boot
    initrd /initrd-boot.img
    ```
    This example assumes that your /boot partition exists on the first partition of your first IDE hard drive (hd0,0 which is /dev/hda1). You could type `df` to see where your /boot partition is located.

5. Reboot your computer.

6. When the GRUB boot screen appears, press the down arrow key to move to the entry that you titled “Fedora Core 3 installation” and press Enter. From here you should be able to start installation normally.
