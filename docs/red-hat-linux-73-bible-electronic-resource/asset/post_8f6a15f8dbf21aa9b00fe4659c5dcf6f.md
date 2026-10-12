
If after installation you decide to add or remove hardware from your computer, there is a tool that will allow you to reconfigure your hardware when the system boots up. See the sidebar describing kudzu for detecting and configuring new and changed hardware.

## Reconfiguring Hardware at Boot Time with kudzu

Sometimes as Red Hat Linux is booting up, you may want to make changes to the system configuration. You may have added a new piece of hardware (or removed one). You may want to turn off a particular system service because it is hanging during the boot. With kudzu, you can change hardware and service configurations as your computer is booting.

To enter kudzu while Red Hat Linux is booting, look for a message on the screen that says "Press 'l' to enter interactive startup." Press l and you will be prompted to enter interactive startup. The kudzu Hardware Discovery Utility will check for hardware that has been removed or added and allow you to add or remove configuration for the hardware or do nothing.

When all the new or changed hardware has been reconfigured, you are prompted to start service reconfiguration. Type Y and you will be stepped through each service that is configured to start at boot time. This is an excellent way to temporarily turn off a service that is hanging your system or that is no longer needed.

## Special Installation Procedures

If you don't want to, or can't, use the procedure to install Red Hat Linux from CD, the procedures in this section give you alternatives. The first procedure tells how to install Red Hat Linux from alternative media (using FTP, HTTP, NFS, or hard disk installs). The next procedure describes how to do kickstart installations.

### Installing from other media

Your CD-ROM drive may not be working, you may not have a CD-ROM drive, or maybe you just want to install a new version of Red Hat Linux that is available from another computer on the network. In any of these cases, Red Hat will let you install Linux from a Web server (HTTP), an FTP server, a shared NFS directory, or local hard disk.

**NOTE:** To use HTTP, FTP, or NFS installations, your computer must be connected to a LAN that can reach the computer containing the Red Hat Linux distribution. You cannot use a direct dial-up connection. For a local hard disk install, the distribution must have been copied to a local disk that is not being used for installation. See the section "Setting up an install server" for details on copying the distribution and making it available.

### Beginning installation

To begin any of these types of installation, you need to boot the installation process from a floppy disk. Refer to the section on creating boot disks later in this chapter. You also need to know the location of an install server — a Red Hat Linux system on your network that contains the Red Hat Linux distribution available.

With the appropriate boot disk in hand (bootnet.img and possibly drvnet.img for a network install, and boot.img for a hard disk install), start the installation for these types of installs as follows:

1. **Insert the floppy boot disk.**
2. **Reboot the computer.** You should see the "Welcome to Red Hat" boot screen.
3. **Press Enter.** You are prompted to select a language.
4. **Select the language.** You are prompted to choose a keyboard type.
5. **Select your keyboard type.** You are prompted to select an installation method.
6. **Choose install method.** Select any of the following installation methods: NFS Image, FTP, HTTP, or Hard disk.
7. **Configure Network Card.** For any of the network installs, you are asked to select your Ethernet card from the list shown. If your card is not on the list, you need to create a `drvnet.img` file, which will contain drivers for other network cards. (To use the `drvnet.img` file, press F2, insert the floppy containing that image into the floppy drive, and click OK. Choose your card from the list and click OK again.)
8. **Configure TCP/IP.** For any of the network install types (NFS, FTP, and HTTP), you are prompted to configure TCP/IP. (See the section on configuring networking earlier in this chapter for descriptions of information you need to add to these fields.)
9. **Identify location of Red Hat Linux distribution.** You need to identify the NFS server name, FTP site name, or Web site name that contains the Red Hat directory that holds the distribution. Or, if you are installing from hard disk, you must identify the partition containing the distribution and the directory that actually contains the Red Hat directory.
10. **Continue with installation.** If the distribution is found in the location you indicated, continue the installation as described in the previous section.

The next section describes how to set up your own server for installing Red Hat Linux.

### Setting up an install server

If you have a LAN connection from your computer to a computer that has a CD-ROM drive and about 2GB of disk space and offers NFS, FTP, or Web services, you can install Red Hat Linux from that server. Likewise, you can install from a spare disk partition by using a hard disk install. The following procedures let you set up a Linux install server.

Because there are three CDs in the Red Hat Linux distribution, you can't just identify the location of the mounted CD as you could with previous Red Hat Linux distributions. You must install the contents of all three CDs in the same directory structure on the server's hard disk. For example, you could do the following:

```bash
# mkdir /tmp/rh
# mount /mnt/cdrom                  With first CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom                  With second CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom                  With third CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
```

Just type "y" when it asks to overwrite some files. The distribution directory must contain at least the RPMS and base directories, which must include all necessary software packages. In this example, all files were copied. What you do next depends on the type of install server you are using.

#### NFS server

Add an entry to the `/etc/exports` file to share the distribution directory you created. This entry would make the directory available in read-only form to any computer:

```text
/tmp/rh (ro)
```

Next, restart NFS by typing the following as root user:

```bash
# /etc/init.d/nfs restart
```

To set the NFS service to be on permanently (it is off by default), type the following as root user:

```bash
# chkconfig nfs on
```

If your computer were named `pine`, the computer installing the distribution from your shared directory would identify it as `pine:/tmp/rh`.

#### Web server

If your computer is configured as a Web server, you need to simply make the distribution directory available. For example, after creating the distribution directory as described above, type the following:

```bash
# ln -s /tmp/rh /var/www/html/rh
```

If your computer were named `pine.handsonhistory.com`, you would identify the install server as `http://pine.handsonhistory.com/rh`.

#### FTP server

If your computer is configured as an FTP server, you need to make the distribution directory available in much the same way you did with the Web server. For example, after creating the distribution directory as described above, type the following:

```bash
# ln -s /tmp/rh /var/ftp/pub/rh
```

If your computer were named `pine.handsonhistory.com`, you would identify the install server as `ftp://pine.handsonhistory.com/pub/rh`.

#### Hard disk install

For a hard disk install, you can copy the ISO images of each CD. For example, with the first CD inserted into your CD drive, type the following as root user:

```bash
# cp /dev/cdrom /tmp/rh/cd1.iso
```

Repeat this step for each of the installation CDs, using `cd2.iso` and `cd3.iso` as the names of the next two CDs. If the ISO images existed in the `/tmp/rh` directory of the first partition of your IDE hard disk, you could identify the device as `/dev/hda1` and the directory holding the images as `/tmp/rh`.

## Performing a kickstart installation

If you are installing Red Hat Linux on multiple computers, you can save yourself some trouble by preconfiguring the answers to questions asked during installation. The method of automating the installation process is referred to as a kickstart installation.

> **CAUTION:** Based on the information you provide in your `ks.cfg` file, kickstart will silently go through and install Red Hat Linux without intervention. If this file is not correct, you could easily remove your master boot record and erase everything on your hard disk. Check the `ks.cfg` file carefully and test it on a noncritical computer before trying it on a computer holding critical data.

The general steps of performing a kickstart installation are as follows:

1. **Create a kickstart file.** The kickstart file, named `ks.cfg`, contains the responses to questions that are fed to the installation process.
2. **Install kickstart file.** You have to place the `ks.cfg` on a floppy disk, on a local hard disk, or in an accessible location on the network.
3. **Start kickstart installation.** When you boot the installation procedure, you need to identify the location of the `ks.cfg` file.

### Creating the kickstart file

A good way to begin creating your kickstart file is from a sample `ks.cfg` file. When you install Red Hat Linux, the installation process places a file called `anaconda-ks.cfg` into the
