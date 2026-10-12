
![](img/27a85d56d393921ced6412ae6e8336bf_63_0.png)

Figure 2-1: Change software packages after Red Hat installation using the Add and Remove Software window.

**NOTE:** To use HTTP, FTP, or NFS installations, your computer must be connected to a LAN that can reach the computer containing the Red Hat Linux distribution. You cannot use a direct dial-up connection. For a local hard disk install, the distribution must have been copied to a local disk that is not being used for installation. See the section "Setting up an HTTP, FTP, or NFS install server" for details on copying the distribution and making it available.

## Beginning installation

To begin any of these types of installation, you need to boot the installation process from a floppy disk. Refer to the section on creating boot disks later in this chapter. You also need to know the location of an install server — a Red Hat Linux system on your network that has the Red Hat Linux distribution available.

With the boot disk in hand (`bootdisk.img` and possibly `drvnet.img` for network install, or `pcmsiadd.img` for a laptop install), start installation for these install types as follows:

**NOTE:** With this version of Red Hat Linux, you can also use CD #1 that comes with this book to start a network or hard disk install. Instead of using a floppy disk, as described below, you can insert Red Hat Linux installation CD #1, reboot the computer, then type `linux askmethod`. You can then proceed with the steps shown below.

1. Insert the floppy boot disk.
2. **Reboot the computer.** You should see the "Welcome to Red Hat" boot screen.
3. **Press Enter.** You are prompted to select a language.
4. **Select the language.** You are prompted to choose a keyboard type.
5. **Select your keyboard type.** You are prompted to select an installation method.
6. **Choose the installation method.** Select any of the following installation methods: NFS image, FTP, HTTP, or Hard drive.
7. **Configure the network card.** For any of the network installs, you are asked to select your Ethernet card from the list shown. (This may be detected automatically.) If your card is not on the list, you need to create a floppy from the `drvnet.img` file, containing drivers for other network cards. (To use the `drvnet.img` file, press F2, insert the floppy containing the image, and click OK. Choose your card from the list and click OK again.)
8. **Configure TCP/IP.** For any of the network install types (NFS, FTP, and HTTP), you are prompted to configure TCP/IP for your computer. (See the section on configuring networking earlier in this chapter for information on how to add to these fields.)
9. **Identify the location of the Red Hat Linux distribution.** You must identify the NFS server name, FTP site name, or Web site name that contains the Red Hat directory that holds the distribution. Or, if you are installing from hard disk, you must identify the partition containing the distribution and the directory that actually contains the Red Hat directory.

**NOTE:** For an FTP install, if you are not downloading from an anonymous FTP site, you must select "Use non-anonymous FTP" when you identify the server and directory. You will need a user name and password that has access to the shared directory.

10. **Do a checksum.** You are asked if you want to do a checksum on the first disk image (`.iso` file of the first installation CD) found in that directory. Select Test if you do. This will verify that the image is not corrupted before you begin. Repeat this for each disk image.
11. **Continue with installation.** If the distribution is found in the location you indicated, continue the installation as described in the previous section. The install is text-based.

The next section describes how to set up your own server for installing Red Hat Linux.

## Setting up an HTTP, FTP, or NFS install server

If you have a LAN connection from your computer to a computer that has about 2.5GB of disk space and offers NFS, FTP, or Web services, you can install Red Hat Linux from that server. Likewise, you can install from a spare disk partition by using a hard disk install. The following procedures let you set up a Linux install server by either copying all files from the three CDs or by copying images of the three CDs.

### Configuring an install server using files

To do an FTP or HTTP install, you must copy the files from the installation CDs to a directory that you make available to the network. Because there are three installation CDs in the Red Hat Linux distribution, you can't just identify the location of a mounted CD. You must install the contents of all three CDs in the same directory structure on the server's hard disk. For example, you could do the following:

```
# mkdir /tmp/rh
# mount /mnt/cdrom	With first CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	With second CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
# umount /mnt/cdrom ; eject /mnt/cdrom
# mount /mnt/cdrom	With third CD inserted
# cp -r /mnt/cdrom/* /tmp/rh/
```

Just type y when it asks to overwrite some files. The distribution directory must contain at least the RPMS and base directories, which must include all necessary software packages. In this example, all files were copied. Setting up an NFS install server requires copying CD images to the shared NFS directory.

### Configuring an install server using disk images

Instead of copying all files from the three installation CDs, you can copy the entire images of each of the three disks to your hard disk for NFS or hard disk installs. To do this, insert the first installation CD and type the following:

```
# mkdir /tmp/rh
# dd if=/dev/cdrom of=/tmp/rh/disk1.iso	With first CD inserted
# mount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk2.iso	With second CD inserted
# umount /mnt/cdrom ; eject /mnt/cdrom
# dd if=/dev/cdrom of=/tmp/rh/disk3.iso	With third CD inserted
# umount /mnt/cdrom ; eject /mnt/cdrom
```

### NFS server

Add an entry to the /etc/exports file to share the distribution directory you created. Remember, that for NFS installs, this directory must contain CD ISO images. The following entry would make the directory available in read-only form to any computer:

```
/tmp/rh	(ro)
```

Next, restart NFS by typing the following as root user:

```
# /etc/init.d/nfs restart
```

To set the NFS service to be on permanently (it is off by default), type the following as root:

```
# chkconfig nfs on
```

### Web server

If your computer is configured as a Web server, you need to simply make the distribution directory available. For example, after creating the distribution directory as described above, type the following:

```
# ln -s /tmp/rh /var/www/html/rh
```

If your computer were named `pine.hansonhistory.com`, you would identify the install server as `pine.hansonhistory.com` and the directory as `rh`.

### FTP server

If your computer is configured as an FTP server, you need to make the distribution directory available in much the same way you did with the Web server. For example, after creating the distribution directory as described above, type the following:

```
# ln -s /tmp/rh /var/ftp/pub/rh
```

If your computer were named `pine.hansonhistory.com`, you would identify the install server as `pine.hansonhistory.com` and the directory as `pub/rh`.

### Hard disk install

With the ISO images of each CD copied to a disk partition that is not being used for your Red Hat Linux install, you can use the hard disk install. If the ISO images exist in the `/tmp/rh` directory of the first partition of your IDE hard disk, you could identify the device as `/dev/hda1` and the directory holding the images as `/tmp/rh`.

## Performing a kickstart installation

If you are installing Red Hat Linux on multiple computers, you can save yourself some trouble by preconfiguring the answers to questions asked during installation. The method of automating the installation process is referred to as a *kickstart* installation.

> **CAUTION:** Based on the information you provide in your `ks.cfg` file, kickstart will silently go through and install Red Hat Linux without intervention. If this file is not correct, you could easily remove your master boot record and erase everything on your hard disk. Check the `ks.cfg` file carefully and test it on a noncritical computer before trying it on a computer holding critical data.

The general steps of performing a kickstart installation are as follows:

1. **Create a kickstart file.** The kickstart file, named `ks.cfg`, contains the responses to questions that are fed to the installation process.
2. **Install kickstart file.** You have to place the `ks.cfg` on a floppy disk, on a local hard disk, or in an accessible location on the network.
3. **Start kickstart installation.** When you boot the installation procedure, you need to identify the location of the `ks.cfg` file.
