
# Chapter 13 ✦ Running Gentoo Linux 393

Then type h to display a list of commands. (See Chapter 7 for information on using fdisk to partition your hard disk.)

Repartitions your disk destroys existing data on your hard disk. Back up any data before you start this procedure. Be sure not to delete or change any partitions that have data on them you want to keep.

```
# fdisk /dev/hda
```

8. **Make file systems.** To create the appropriate file systems on your disk partitions, use the mkfs and mkswap commands. For example, with an IDE drive that has the first partition as the boot partition (/dev/hda1), the second as swap (/dev/hda2), and the root (/dev/hda3), you can type the following:

```
# mkfs /dev/hda1
# mkswap /dev/hda2
# mkextfs /dev/hda3
```

9. **Turn on swap.** Use the swap command to turn on your swap partition. For our example (with hda2 being the swap partition), type:

```
# swapon /dev/hda2
```

10. **Mount root (/).** You need to mount the root (/) partition temporarily to begin installing Gentoo to it. In this example (with the root file system as /dev/hda3), type:

```
# mount /dev/hda3 /mnt/gentoo
```

11. **Mount /boot partition.** Next, mount the boot partition so you can install boot files to that partition:

```
# mkdir /mnt/gentoo/boot
# mount /dev/hda1 /mnt/gentoo
```

12. **Get the stage1 tarball.** Assuming that you have the minimal Gent installation CD, you need to download the stage1 tarball. Find a mirror site near you (as described earlier). Make a directory on your hard disk to copy it and download the tarball using a tool as wget. For an example:

> If you are using the universal CD, the stage1 tarball is available there. Instead of downloading it, jump to the next step and extract the tarball from /mnt/cdrom/stages/stage1*.tar.bz2.

```
# mkdir /mnt/gentoo/tmp2
# cd /mnt/gentoo
# wget -c http://gentoo.osu.org/releases/x86/2005.1/stages/stage1-x86-2005.1.tar.bz2
```

The wget command, which appears on multiple lines here, should be typed on one line. (There's no space between the slash at the end of the first line and the word "" at the beginning of the next.) If the download should stop in the middle, you can restart it by running the same command in the same directory.

## 13. Extract the stage 1 tarball. Use the following commands:

```
# cd /mnt/gentoo
# tar -xvjpf /mnt/gentoo/tmp2/stage1-*.tar.bz2
```

You can remove the stage1 tarball once you have untarred.

14. Select mirror site. Use the mirrorselect command to search for a Gentoo mirror from which you can efficiently download the files you need to install. Run the following command to select an efficient mirror and add it to your make.conf file (it will take a while to download speed from more than 150 servers):

```
# mirrorselect -a s4 -o | grep Gentoo_MIRrors >> /mnt/gentoo/etc/make.conf
```

When you emerge commands in this procedure, you may see messages that files are not found from any of the other sites, you might need to add other mirror sites to the make.conf file.

15. Mount file systems. Mount the /proc file system as follows:

```
# mount -t proc /mnt/gentoo/proc
```

16. Change root directory. Use the chroot command to change /mnt/gentoo to be your root directory, but first copy the resolve.conf file so you can edit from here:

```
# cp /etc/resol.conf /mnt/gentoo/etc/resolve.conf
# chroot /mnt/gentoo /bin/bash
```

17. Update environment. Read in environment variables as follows:

```
# env-update: source /etc/profile
```

18. Update Portage tree. Use the following command to have the latest package information installed to your /usr/portage directory:

```
# emerge --sync
```

19. Modify make.conf. Use the nano editor to change the make.conf file that is used to build your Gentoo system. Here's how:

```
# nano -w /etc/make.conf
```

If you don't know what to change, refer to the /etc/make.conf.example file for information on the settings you want to change before continuing. If you don't know which processor your computer has, type /proc/cpuinfo.

20. Bootstrap Gentoo. Run bootstrap.sh to bootstrap Gentoo as follows:

```
# cd /usr/portage/scripts/bootstrap.sh
```

21. Install Gentoo. Run the following emerge command to install:

```
# emerge -e system
```

It takes a long time for emerge -e system command to complete. If it fails it is finished, check that the settings in your make.conf file are correct.

## Chapter 13 ✦ Running Gentoo Linux 395

22. Set time zone. Use the symlink command:

```bash
# ln -sf /usr/share/zoneinfo/UTC /etc/localtime
```

23. Create file system table. Edit /etc/fstab:

| Device | Mount Point | File Type | Options | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | /boot | ext3 | defaults | 0 | 1 |
| /dev/hda2 | swap | swap | sw | 0 | 0 |
| /dev/hda3 | / | ext3 | defaults | 0 | 1 |
| /proc | /proc | proc | defaults | 0 | 0 |

24. Build kernel. Either install a kernel or build yourself.

```
# emerge genkernel
```

Next, use the following command to have the kernel use menuconfig:

```bash
# genkernel --menuconfig-all
```

After you have made changes, select Yes to save. Refer to the Gentoo Handbook, "Configuring the Kernel," for information. After kernel is complete, note the names of the boot loader.

25. Add coldplug. Type the following to enable hardware detected:

```bash
# emerge coldplug
# rc-update add coldplug default
```

## Part III Choosing and Installing a Distribution

26. Configure system services. Install your system services — system logger, cron service, hotplug, and reiser service — and set the domain name. Then turn on each of these services:

```
# emerge syslog-ng
# rc-update add syslog-ng default
# emerge vixie-cron
# rc-update add vixie-cron default
# emerge hotplug
# rc-update add hotplug default
# emerge reisersprogs
# rc-update add domainname default
```

27. Add special driver support. There may be particular kernel modules required by your computer at this point. For example, if you have a special Ethernet adapter or a special type of video card, use the emerge to install kernel modules.

```
# emerge nvidia-kernel
# emerge nforce-audio
# emerge e100
# emerge e1000
# emerge iau10k
# emerge ati-drivers
```

These command lines are used only if you have special hardware associated with the kernel drivers. respectively, these commands load drivers for accelerated Nvidia video cards, audio for Nvidia Nforce-boards. Intel e100 Fast Ethernet cards, Intel e1000 Gigabit Ethernet cards, Sound Blast/Audiochemy for 2.4 kernel, and ATI Radeon+/FireGL graphics cards.

28. Add user and information. Add a password for the root user, a regular account name of your choosing (chris in this example), a machine name, and a domain. If you like, you can also edit the /etc/hosts and /etc/rc.conf files to add IP addresses or change the basic startup script.

```
# passwd
# useradd chris -G users,wheel,audio -s /bin/bash
# echo myname > /etc/hostname
# echo mydomain.com > /etc/dnsdomainname
# nano -w /etc/hosts
# nano -w /etc/rc.conf
```

29. Set up networking. Edit the net file, and then run rc-update to add the eth0 interface as the default (Uncomment the line interface eth0="dhcp" to have the network use DHCP to start automatically.)

```bash
# nano -w /etc/config.d/net
# rc-update add net.eth0 default
```
