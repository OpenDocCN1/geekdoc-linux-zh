
Regardless of the super-server in use on a host, the TFTP service is usually disabled by default. Hence, even if you use the default /tftpboot directory, you need to modify the super-server’s configuration files to enable TFTP.

## Mounting a Root Filesystem on an NFS Server

As we explained in Chapter 2, although the bootloader and Linux kernel must be stored locally or retrieved to local storage through one of the methods shown earlier, the target’s kernel can subsequently mount its root filesystem from a remote NFS server. To this end, the NFS server must be properly installed and configured. Chapter 6 showed how to build your target’s root filesystem. If this filesystem is retrieved from an NFS server, the filesystem does not need any of the preparations described in Chapter 8.

The NFS server daemon is available in two flavors: as a standalone user application or as a part of the kernel. Besides being faster, the latter is also the standard configuration in most distributions. In addition to the NFS server itself, you need to have the NFS utilities installed. Usually, an nfs-utils package is part of your distribution. On an RPM-based distribution, use the following command to identify whether nfs-utils is installed:

```bash
$ rpm -q nfs-utils
nfs-utils-1.1.0-r6.fc8
```

With the nfs-utils package installed, you need to make sure that the appropriate configuration files are present and the corresponding services are started. The main file we need to configure for the NFS server is /etc/exports. Entries in this file describe the directories that each host or set of hosts can access. Here’s an example:

```bash
/data/root/virtex4 192.168.1.201(rw,no_root_squash)
```

This entry states that the machine with address 192.168.1.201 has read and write (rw) access to the /data/root/virtex4 directory, which is the path to a root filesystem similar to that which we built for the target in Chapter 6. In addition, the no_root_squash argument indicates that the server should allow the remote system to access the directory with its root privileges. There are very powerful rights that we are granting to the target. If we have total control over access to the device, as is the case in most development setups, there is obviously no security risk. If, however, the target’s location is less secure or if it is directly connected to the Internet (a configuration you really want to avoid with any NFS server), for example, you may prefer to use the default root_squash instead. Otherwise, it is trivial for others to forge access from the 192.168.1.201 address and trash, or otherwise compromise, your exported data. With root_squash in effect, the target will not be able to write to most of its own root filesystem, though it will still be able to read and write to all directories and files that are readable and writable by anybody. In practical terms, however, the target's operation will be very limited.

Because offering the NFS service also involves the risk of network abuse, it is often pertinent to use some minimal protection mechanisms to avoid intrusions. One simple way to do this is to customize the /etc/hosts.deny and /etc/hosts.allow files to restrict access to network services. The following is an example /etc/hosts.deny file:

```text
#
# hosts.deny
#

portmap: ALL
lockd: ALL
mountd: ALL
rquotad: ALL
statd: ALL
```

And an example /etc/hosts.allow file is:

```text
#
# hosts.allow
#

portmap: 192.168.1.201
lockd: 192.168.1.201
mountd: 192.168.1.201
rquotad: 192.168.1.201
statd: 192.168.1.201
```

The rules specified in these files restrict the access that users on remote systems have to the various file-sharing services. Together, these files indicate that only the machine with address 192.168.1.201 can use the NFS services. This is fine in the case of our sample setup, since we don't want to share the development workstation in these examples with anyone else just now. Even if you do not customize /etc/hosts.deny and /etc/hosts.allow, we still encourage you to take security issues to heart and use reasonable measures, such as backups, to protect your work.

Once the configuration files are created, you can start the portmapper service, which the NFS server requires:

```bash
# /etc/init.d/portmap start
```

Finally, you can start the NFS server itself:

```bash
# /etc/init.d/nfs start
```

If you would like more information on the configuration of remote boot using NFS, see the two Diskless root NFS HOWTOs on the issue at the LDP. Additionally, you may be interested in the NFS HOWTO, also at the LDP.

## Using the U-Boot Bootloader

A growing majority of embedded Linux devices is now using Das U-Boot (also informally known as “U-boot,” “u-boot,” and “uboot”) to handle system bringup, initial development, and debugging, as well as the bootloader needs of the finished system. U-Boot is a richly documented bootloader. Not only does it come with extensive documentation detailing its use and development on a wide variety of systems, but the website also houses an extensive wiki (http://www.denx.de/wiki/UBoot) that is maintained by many contributors to the project. In addition to the official versions, documentation, mailing lists, and so forth, the website has pointers to “custodian” source code development trees that contributors have made to specific parts of U-Boot. These are often where support for new boards is first added, before appearing in the official releases.

The `README` file included with U-Boot covers the use of U-Boot extensively. Among other things, it discusses the *package’s* source code layout, the available build options, U-Boot’s command set, and the typical environment variables used in U-Boot. The following discussion will cover the essential aspects of U-Boot and provide practical examples of its use. An in-depth discussion of U-Boot would, however, require a book of its own. For this reason, we encourage you to print a copy of the `documentation` file provided with U-Boot and spend some time reading through the wiki at your leisure.

## Compiling and Installing

Start by downloading and extracting the latest version of U-Boot from the project website, either a snapshot release or (if you will be performing development of your own) the project’s `GIT` source code repository. As of this writing, the latest U-Boot version is `1.3.3`. Here’s how to retrieve the latest `GIT` development repository sources using the `git` command (you may need to install the `git` utility on your host system):

```bash
$ git clone git://git.denx.de/u-boot.git
```

### OpenMoko (GTA01) Hardware

The following sections are based on the OpenMoko revision 1 hardware (GTA01 “neo1973”) platform, as was mentioned at the end of Chapter 2. The board runs on a Samsung S3C442 B54 ARM-based SoC at 400MHz, has 256 MB of NAND flash (for the bootloader, kernel, and root filesystem), and 128 MB of RAM. The U-Boot configuration file specifies the Physical Memory Map, where the RAM is mapped from the physical address 0x30000000 to address 0x38000000 (128 MB), and the NAND flash is accessed via commands issued to the interface at physical address 0x4e000000. The documentation provided with U-Boot explains how it uses the physical memory on targets.

In this book, we have occasionally used the OpenMoko hardware as a reference, in part because a fully functional emulator (based on the QEMU sources) exists that is also capable of running U-Boot. Therefore, you can experiment with the information contained within this chapter even if you don't own one of these devices. On this book's website (<http://www.embeddedlinuxbook.org>), you will find a snapshot of the emulator and U-Boot sources used for this book, and some scripts that will assist you in experimenting with U-Boot "upgrades" on emulated hardware. You will also find some additional documentation. Please do visit the book's website for further information.

You can find further information about running U-Boot on the GTA01 at the OpenMoko website (the wiki is at <http://openmoko.org/wiki/Bootloader>). There you will find detailed instructions as well as references to the available Toolchains needed to build U-Boot and other applications software for the OpenMoko reference hardware. These will save you much time and effort.

Before you can build U-Boot, you need to configure it for your target. The package includes a number of preset configurations for quite a few boards, so a configuration may very well exist for your target already. Check the README file to see whether your board is supported. For each supported board, U-Boot's *Makefile* typically includes a `boardname_config` target, which is used to configure U-Boot's build for the designated board. (If you don't see one for your board, refer to the wiki and to the custodian trees to see whether there is a work in progress that you can help test on your development system.) The configuration target for the GTA01 board we use in this chapter, for example, is `gta01_config`. Once you have determined the proper *Makefile* target to use, configure U-Boot's build process:

```bash
$ make gta01_config
```

Now build U-Boot by following the build process covered in the U-Boot documentation:

```bash
$ make ARCH=arm CROSS_COMPILE=arm-angstrom-linux-gnueabi- u-boot.ubfu
```

As you can see, in this case, the OpenMoko development board is ARM-based and requires the use of a cross-compiler. The `arm-angstrom-linux-gnueabi-` reference refers to the ARM cross-compiler released by the OpenMoko project, while the `.ubfu` extension on the U-Boot binary target instructs the build process to produce a binary in a special format known as "USB Device Firmware Update." This binary format can also be used for field upgrades to the version of U-Boot running on an OpenMoko device, using the existing U-Boot as a bootstrap. Further information about the precise mechanics of using U-Boot on the OpenMoko reference hardware is provided at the project website referenced previously.

In addition to generating bootloader images, the build process will compile a few tools to be used on the host for conditioning binary images before downloading them off to the target to a running U-Boot. Table 9-1 lists the files generated during an example of U-Boot's compilation. (These can vary depending upon the target in question and the image formats supported.)
