
The optional **xconfig** command can be used to configure your monitor and video card. If you use the **skipx** command instead (as shown in the following code sample), no X configuration is done. (After the system is installed, run **system-config-desktop** to set up your X configuration.) When you use the **xconfig** command, you can identify the type of X server to use based on your video card (`--card`) and monitor speed (`--hysync` and `--vsvync`). A handful of other options enable you to set the color depth in bits (`--depth`), the screen resolution (`--resolution`), whether the default desktop is GNOME or KDE (`--defaultdesktop`), whether the login screen is graphical (`--startx` or `--startkboot`), and the amount of RAM on your video card (`--videoram`). (All the information after **xconfig** should actually appear on one line.)

```bash
skipx
```

or

```bash
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072 \
--hysync=31.5-37.9 --vsvync=50-70 --resolution=800x600 \
--depth=16 --startkboot --defaultdesktop gnome
```

The optional **network** command lets you configure your Fedora or RHEL system's interface to your network. The example tells your computer to get its IP address and related network information from a DHCP server (`--bootproto dhcp`). If you want to assign a particular IP address, use the `--bootproto static` option. Then change the IP address (`--ip`), netmask (`--netmask`), IP address of the gateway (`--gateway`), and IP address of the DNS server (`--nameserver`) to suit your system. You can also add a hostname (`--hostname`).

> **NOTE:** Although the **network** values appear to be on three lines, all values must be on the same line.

```bash
network --device eth0 --bootproto dhcp
```

or

```bash
network --device=eth0 --bootproto static --ip=192.168.0.1 \
--netmask 255.255.255.0 --gateway 192.168.0.1 \
--nameserver 192.168.0.254 --hostname duc.example.com
```

The **roothpw** command sets the password to whatever word follows (in the following example, **passWord**). It is a security risk to leave this password hanging around, so you should change this password (with the **passwd** command) after Linux is installed. You also have the option of adding an encrypted password instead (`--iscrypted g.UJ.RQeOY3Bg --enablemd5`).

```bash
roothpw passWord
```

or

```bash
roothpw --iscrypted g.UJ.RQeOY3Bg --enablemd5
```

The **firewall** command lets you set the default firewall used by your Fedora or RHEL system. The default value is **enabled** (if the firewall is turned on). You can also set **firewall** to **disabled** (no firewall). (These values are described in the installation procedure earlier in this chapter.) As you can see in the example, you can optionally indicate that there be no restrictions from host computers on a particular interface (--trust eth0). You can also allow an individual service (--ssh) or a particular port:protocol pair (--port 1234:udp).

```bash
firewall --enabled --trust=eth0 --ssh --port=1234:udp
```

The required **authconfig** command sets the type of authentication used to protect your user passwords. The --enableshadow option enables the /etc/shadow file to store your passwords. The --enablemd5 option enables up to 256 character passwords. (You would typically use both.)

```bash
authconfig --enableshadow --enablemd5
```

The **selinux** command indicates whether or not Security Enhanced Linux is enabled. The following line shows it as enabled and enforcing:

```bash
selinux --enforcing
```

The **timezone** command sets the time zone for your Linux system. The default, shown here, is United States, New York (America/New_York). The -utc option indicates that the computer's hardware clock is set to UTC time. If you don't set a time zone, US/Eastern is used. Run the **timeconfig** command to see other valid time zones.

```bash
timezone --utc America/New_York
```

The **bootloader** command sets the location of the boot loader (GRUB, by default). For example, --location=mbr adds GRUB to the master boot record. (Use --location=none to not add GRUB.) The driverorder= option describes which hard disk to look on first for the master boot record. You can also add kernel options to be read at boot time using the append option (--append hdd=ide-scsi) or an optional password for GRUB (--password=GRUBpassword).

```bash
bootloader --location=mbr --driverorder=sda --append="rhgb quiet"
password=GRUBpassword
```

Partitioning is required for a new install, optional for an upgrade. The code that follows is from the sample ks.cfg file. The clearpart --linux value removes existing Linux partitions (or use --all to clear all partitions) on the first hard drive (--drives=sda). The part /boot, / and swap, sets the file system type (-fstype) and partition name (onpart) for each partition assignment. You can also set sizes of the partitions (--size) to however many megabytes you want. You can also create logical volume group (volgroup) and individual logical volume (logvol) entries for your partitioning.

```bash
# The following is the partition information you requested
# Note that any partitions you deleted are not expressed
# here so unless you clear all partitions first, this is
# not guaranteed to work
#clearpart --linux --drives=sda
```

```bash
#part /boot --fstype ext3 --size=100 --ondisk=sda
#part / --fstype ext3 --size=700 --grow --ondisk=sda
#part swap --size=128 --grow --maxsize=256 --ondisk=sda
```

To indicate which packages to install, begin a section with the `$packages` command. (A few examples follow.) Designate whole installation groups, individual groups, or individual packages. On the `$packages` line, you can indicate whether or not to resolve dependencies by installing those packages needed by the ones you selected (`--resolvedeps`). After `$packages`, start an entry with an `@` sign for a group of packages, and add each individual package by placing its name on a line by itself. Here is an example:

> **TIP**: You can find a listing of package groups and individual packages on the Fedora installation DVD. Find the comps file in the Fedora/base directory. However, if you start with the `anaconda-ks.cfg` file that resulted from installing Fedora or RHEL, you might already have a set of packages that you want to install.

```bash
$packages --resolvedeps
@base
@editors
@games
@graphical-internet
@kde-desktop
@office
@sound-and-video
...
```

> **NOTE**: The `$packages` command is not supported for upgrades. To install everything, you can remove the package names shown. Then, after the `$packages` line, you can add an `@everything` line.

The `$post` command starts the post-installation section. After it, you can add any shell commands you want to run after installation is completed. A useful thing to do is to add `useradd` commands for users you want to add during installation. You can also use the `usermod` command to add the user’s password. (See Chapter 22 for information on creating an encrypted password.)

```bash
$post
/usr/sbin/useradd jake
chfn -f 'John W. Jones' jake
/usr/sbin/usermod -p 'S1kQUMyPb0H?9wBCxnPUaH.' jake
```

At this point you should have a working `ks.cfg` file.

# Installing the kickstart file

Once the `ks.cfg` file is created, you need to put it somewhere accessible to the computer doing the installation. Typically, you will place the file on a floppy disk. However, you can also put the file on a computer that is reachable on the network or on a hard disk.

To copy the file to a floppy disk, create a DOS floppy and copy the file as follows:

```bash
# mcopy ks.cfg a:
```

When you do the Fedora kickstart installation, have this floppy disk with you. As an alternative, you can copy the `ks.cfg` file to a hard disk partition, Web server, or NFS share.

Being able to place the `ks.cfg` file on a computer on the network requires a bit more configuration. The network must have a DHCP or a BOOTP server configured that is set up to provide network information to the new install computer. The NFS server containing the `ks.cfg` file must export the file so that it is accessible to the computer installing Linux. To use a `ks.cfg` file from the local hard disk, you can place the file on any partition that is a Windows (VFAT) or Linux (ext3) partition.

# Booting a kickstart installation

If the kickstart file (`ks.cfg`) has been created and installed in an accessible location, you can start the kickstart installation. Here is an example of how you can do a kickstart installation using the Fedora DVD and a floppy containing a `ks.cfg` file:

1.  Insert the Fedora or RHEL disc and restart the computer.
2.  When you see the boot screen, insert the floppy containing the `ks.cfg` file, highlight the first boot entry and press the Tab key. When the boot command line appears, modify it to add the following text:
    
    ```bash
    ks=floppy
    ```
    
    You should see messages about formatting the file system and reading the package list. The packages should install without any intervention. Next you should see a post-install message. Finally, you should see the Complete message.
3.  Remove the floppy; then press the Spacebar to restart your computer (the DVD should eject automatically).

> **TIP:** You can install using kickstart over NFS (`ks=nfs:server:path/ks.cfg`), from Web server (`ks=http://server/path/ks.cfg`), or from your hard drive (`ks=hd:device/ks.cfg`).

# Special Installation Topics

Some things that you run into during installation merit whole discussions by themselves. Rather than bog down the procedures with details that not everyone needs, I have included
