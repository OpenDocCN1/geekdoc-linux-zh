
You must remember that you need to run the lilo command every time you modify the configuration file and every time you change a kernel image file, whether you modify the configuration file or not. Even if you store a new kernel image in the same place as the old one, and with the same name, you must still run the lilo command to have the new kernel installed.

## 7.4 Kernel Build

The Linux kernels supplied with most software distributions are configured to support as wide a range of hardware as possible, so that they will work with as many machines as possible for Linux installation purposes. Once you have an installation running, it is a good idea to build a custom kernel specifically for your machine. In general, this will reduce the size of the kernel and thus increase the amount of memory you have available in which to work. If you only have a limited amount of memory fitted in your machine (4 Mb for example), then this can make a noticeable difference.

Assuming that you have installed the Linux kernel sources and the GNU C/C++ compiler as part of your Linux installation, then building a new kernel is very straightforward.

The first task is to check that your installation of the Linux sources has created two symbolic links in the directory /usr/include, as in the following example:

```
# cd /usr/include
# ls -l asm linux
lrwxrwxrwx 1 root root 26 Jul 4 17:27 asm -> /usr/src/linux/include/asm
lrwxrwxrwx 1 root root 28 Jul 4 17:27 linux -> /usr/src/linux/include/linux
```

If the symbolic links already exist then you must not perform the next step. If they do not exist then you will need to set them up manually, probably to replace a pair of directories of the same name. These things can be done as follows:

```
# cd /usr/include
# rm -fr asm linux
# ln -s /usr/src/linux/include/asm asm
# ln -s /usr/src/linux/include/linux linux
```

### 7.4.1 Configuration

The next step is to choose which facilities and hardware drivers you want to include in your new kernel; you do this with the following commands:

```
# cd /usr/src/linux
# make config
```

You will now be offered a yes/no question and answer session asking which things you wish to include in your new kernel and which you wish to leave out. After each question you will see either [y] or [n]. This is the default answer for the question if you just press Enter. When you have configured your system the answers you have given will be remembered and will become the defaults if you need to run make config again.

Most of the questions have reasonably obvious answers, though one or two deserve a mention here:

Kernel math emulation (CONFIG_MATH_EMULATION) [n]

If you have a system which does not have a floating point co-processor installed, then you will need to answer yes to this question so that a floating point co-processor emulator can be included into the kernel. If you do have a co-processor then you can answer no here and reduce your kernel size a little. Answering yes to this question with a co-processor fitted will cause no problems as the kernel will detect your co-processor and use it anyway.

Networking support (CONFIG_NET) [y]

You should probably include network support even if you do not have a network card, because many software packages make use of sockets which comprise the main network interprocess communication mechanism. The kernel can use a local loopback arrangement between processes on a single machine so that they can use sockets to talk to each other as though over a physical network.

Limit memory to low 16MB (CONFIG_MAX_16M) [y]

Unless you have more than 16 Mb of memory on your machine then you may as well answer yes to this question.

- TCP/IP networking (CONFIG_INET) [y]
- IP forwarding/gatewaying (CONFIG_IP_FORWARD) [y]
- IP multicasting (CONFIG_IP_MULTICAST) [y]
- IP firewalling (CONFIG_IP_FIREWALL) [y]
- IP accounting (CONFIG_IP_ACCT) [n]

The TCP/IP networking should probably be included, but the IP options that follow are only used if your machine is going to perform some serious network application such as acting as a secure gateway between networks.

- Standard (minix) fs support (CONFIG_MINIX_FS) [n]
- Extended fs support (CONFIG_EXT_FS) [n]
- Second extended fs support (CONFIG_EXT2_FS) [y]
- xiafs filesystem support (CONFIG_XIA_FS) [n]
- msdos fs support (CONFIG_MSDOS_FS) [y]
- umsdos: Unix like fs on top of MSDOS fs (CONFIG_UMSDOS_FS) [n]
- /proc filesystem support (CONFIG_PROC_FS) [y]
- NFS filesystem support (CONFIG_NFS_FS) [y]
- ISO9660 cdrom filesystem support (CONFIG_ISO9660_FS) [y]
- OS/2 HPFS filesystem support (read only) (CONFIG_HPFS_FS) [n]
- System V and Coherent filesystem support (CONFIG_SYSV_FS) [n]

Linux is capable of supporting many filesystem types, though there are probably only a few that you will need to include. The second extended filesystem support is essential if you built your Linux native disk partitions using it (as we did in our example installation). Being able to mount DOS hard disk partitions and floppy disks is also very useful. You will almost certainly need the /proc filesystem as versions of many day-to-day Linux commands are configured to use it (like ps). The NFS filesystem allows disk partitions on one machine to be mounted over a network into another machine's directory hierarchy. The ISO9660 filesystem is required if you want to operate a CD-ROM drive.

You should edit /usr/src/linux/Makefile after running make config to make sure that the definition of the symbol ROOT_DEV is correct. If the disk partition you want to use as your root filesystem is the same as the one which is currently in use in your running system then the symbol should be set as:

```
ROOT_DEV = CURRENT
```

Otherwise the disk partition name corresponding to the required root filesystem should be assigned to ROOT_DEV instead. For example:

```
ROOT_DEV = /dev/hda3
```

### 7.4.2 Compilation

Once the configuration is complete, which might initially take two or three attempts to get it how you want it, you can move on to the next stage – preparing and compiling the source tree.

You should start this with the commands:

```
# make dep
# make clean
```

The first of these will configure up all the makefiles for you, to match your particular installation and kernel configuration choices. The second will make sure that there are no old binary files lying about in the source tree to interfere with the compilation of your chosen kernel configuration.

When these have completed successfully, which may take a minute or two, you should go on to start the compilation proper:

```
# make zImage
```

Having entered this command you should now go and take a break because, depending on your processor speed and the amount of memory you have on your system, it could take quite a while to run. A 486DX2/66 with 16 Mb of memory takes about 20 minutes, a 386SX/16 with 4 Mb takes several hours.

Once completed, the system will have generated a ready to install, compressed kernel image in the file:

```
/usr/src/linux/arch/i386/boot/zImage
```

### 7.4.3 Installation

In order to test the new kernel you should make a bootable floppy disk from it, using the procedure you saw in Section 7.3.4 to configure the root filesystem partition name into it first.

If all goes well when you boot the machine from the new floppy disk then you can consider setting up the new kernel to boot from the hard disk, if you wish. Probably the easiest and safest way to do this is to set up an extra kernel in your lilo.conf file and re-run lilo.

The lilo.conf file can be modified as follows:

```
# LILO configuration file
# Global section
boot = /dev/hda
delay = 50

# DOS bootable partition section
other = /dev/hda1
    label = dos
    table = /dev/hda

# New Linux bootable partition section
image = /vmlinuz
    root = /dev/hda3
    label = linux
    read-only

# Old Linux bootable partition section
image = /.vmlinuz
root = /dev/hda3
label = linux.old
read-only
```

Notice that there are two bootable Linux kernel sections, one for the new kernel you just created and one for the original kernel so that you can always fall back on the old kernel if any problems show up with the new one.

In order to use the new lilo.conf file, you would need to execute the following command sequence:

```
# mv /vmlinuz /.vmlinuz
# cp /usr/src/linux/arch/i386/boot/zImage /vmlinuz
# lilo
```

The first command saves the current kernel image under a new (and invisible) name, the second command places a copy of the new kernel into the place specified in the lilo.conf file and the final line performs the lilo installation.

Now, when you re-boot your system, you have three choices at the boot: prompt. You can type dos to boot the DOS operating system, linux to boot the new Linux kernel or linux.old to boot the original kernel.

### 7.4.4 loadlin

The lilo package is only one of the Linux boot loaders available. Another possibility is a package to run under DOS called loadlin.

The main difference as far as users are concerned is that lilo allows you to make the choice of operating system or kernel at boot time, whereas loadlin users need to boot into DOS first, and only when they are there do they then make the choice to stay in DOS or use loadlin to boot Linux.

In order to use loadlin you must copy it and your Linux kernel file into your DOS partition. The easiest way to do this is to have the DOS partition mounted under Linux and then just use the Linux cp command.

Some Linux distributions, including Slackware, offer you the opportunity during the installation procedure of configuring a DOS partition to be mounted into the Linux directory hierarchy automatically during the boot sequence. If your distribution does not offer this opportunity, or if you opted not to take it, then the DOS partition will have to be mounted manually.

The command used to mount the top level directory of one filesystem underneath a leaf level directory in another filesystem is called mount. The general format of the mount command is:

```
mount -t type device directory
```
