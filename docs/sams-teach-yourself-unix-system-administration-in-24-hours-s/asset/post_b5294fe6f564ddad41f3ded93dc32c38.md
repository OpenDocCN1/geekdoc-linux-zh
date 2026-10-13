
Disk /dev/sda: 255 heads, 63 sectors, 522 cylinders
Units = cylinders of 16065 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/sda1 | * | 1 | 6 | 48163+ | 83 | Linux |
| /dev/sda2 |  | 7 | 490 | 3887730 | 83 | Linux |
| /dev/sda3 |  | 491 | 522 | 257040 | 82 | Linux swap |

To add an additional operating system, we would need to have a configuration that included additional partitions—they're all in use already in the above output, as you can see by comparing the disk statistics with the start and end values of the specific devices.

Given that we've consumed the entire disk with this set of partitions, the bad news is that we need to repartition the disk, destroying the /dev/sda2 partition, then reinstall Linux. Or we need to buy, format, and install a new disk.

2. The resultant partition table for a reorganized disk might look like this:

Disk /dev/sda: 255 heads, 63 sectors, 522 cylinders
Units = cylinders of 16065 * 512 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/sda1 | * | 1 | 6 | 48163+ | 83 | Linux |
| /dev/sda2 |  | 7 | 245 | 1943865 | 83 | Linux |
| /dev/sda3 |  | 246 | 490 | 1943865 | b | Win95 FAT32 |
| /dev/sda4 |  | 491 | 522 | 257040 | 82 | Linux swap |

There are other ways to partition your disk too, and many Linux experts recommend that you start with Windows, using the Windows installer to partition the disk into the four partitions needed.

If you're going to dual-boot, it's wise to read this section before you begin any installation on your disk. You could also opt for another solution that's less destructive, such as VMware, covered later in this hour.

## Dual-Boot Configurations with LILO

When you have more than one operating system installed on your system, you can select your favorite at boot-time by using either LILO or GRUB. LILO is the Linux Loader, and it's surprisingly straightforward to configure.

### Task 11.2: Configuring LILO

Though it has an important task in the boot sequence, LILO itself is a very simple program. The configuration file isn't too complex, but there are some nuances that are critical to understand.

- 1. To start, here's a lilo.conf file for a system that can dual-boot Red Hat Linux or Windows 2000. There are three possible boot options here: a regular RHL boot, a RHL boot into single-user mode (see Hour 13, “Changing System State”), and a boot into Windows 2000 Professional, if the user feels the need to see how the other half lives!

```
# cat /etc/lilo.conf
boot=/dev/sda
default=RHL
prompt
timeout=300
image=/boot/vmlinuz-2.4.7-10
  label=RHL
  root=/dev/sda2
  read-only
image=/boot/vmlinuz-2.4.7-10
  label="RHL -s"
  root=/dev/sda2
  append=-s
  read-only
other=/dev/sda3
  label=Windows2000
  table=/dev/sda
```

The boot= line specifies where the master-boot record should be written, default specifies the default image (OS) to boot, and prompt forces LILO to give you a chance to enter your preferred OS at boot-time.

The timeout setting specifies how long before the system automatically picks the boot option specified, but it's in tenths of a second, so timeout=300 is 30 seconds, not 5 minutes. It's very important to keep this value large while you're experimenting!

![](img/5ced0c78d748bd190e9027e5549a3622_237_0.png)

> Once, a friend and I were experimenting with the settings in the lilo.conf file and accidentally set timeout=10 rather than timeout=100. It wouldn't have been too bad except the default OS to boot into was Windows, so we couldn't get to the Linux OS to fix the configuration file. It was quite comical to watch us try and type the appropriate entry to the LILO prompt at just the right moment!

For LILO-friendly operating systems (most Linux and PC-Unix systems), you can then specify the kernel file image name, the label for LILO to display at the prompt, and the root= line, indicating where the partition containing the kernel image is located.

You can see that we specify that the system should be mounted read-only, which might seem a bit weird, but we want to have the disk read-only so that fsck can check it without causing too much trouble (recall that running fsck on a mounted disk is very bad juju!). As the boot sequence proceeds, the disk is automatically unmounted and remounted as read-write.

The second boot option takes advantage of the append= option to force the kernel to boot with the -s flag, which forces single-user mode. You should rarely need something like this in day-to-day operation.

Finally, partition 3 of /dev/sda contains a separate Windows boot environment, so it's denoted by specifying the partition of the disk upon which the OS is installed, here other=/dev/sda3, and then the disk that the OS itself is found as table=/dev/sda.

There are a few other options to the lilo.conf file, and because they change from version to version (albeit subtly), your best bet is to check the LILO man page for exact details on what your version supports.

- 2. After you have your configuration file written, you need to install or update LILO in the master-boot record (MBR). Before you do that, however, it's critical to always test the configuration file first, by specifying -t:

```
# /sbin/lilo -t
Adding RHL *
Added RHL-s
Added Windows2000
```

After the configuration file can be read without any errors, really install it by omitting -t:

```
# /sbin/lilo
Added RHL *
Added RHL-s
Added Windows2000
```

Not very exciting output, but because it didn't generate any errors, all is well.

![](img/5ced0c78d748bd190e9027e5549a3622_238_0.png)

> Note that if you forget to test the configuration and a real install fails part-way with an error, you must fix it and reinstall before you reboot! If you don’t, your MBR will be corrupt and you will not be able to boot properly.

3. Rebooting the system now produces the standard PC bootup output messages, then clears the screen and prompts:

```
LILO boot:
```

At this point, you can just wait—and after 30 seconds the default entry in the lilo.conf file will be booted (in this case, the one with the RHL label). If you'd rather see your options, type either ? or TAB and you'll see all your choices:

```
LILO boot: ?
RHL      RHL-s    Windows2000
boot:
```

You can type the operating system you desire, or, again, you can just let the system timeout.

```
boot: RHL
the long, involved Unix boot sequence begins.
```

There are many fans of LILO in the Unix world, and for good reason. LILO has been reliably booting Unix and Linux systems for many years with few problems or hiccups. However, in the past few years GRUB has grown in popularity because of its flexibility and more attractive appearance. That's why Red Hat Linux installs with GRUB as the default boot loader, not LILO.

> In any case, a good rule of thumb before you try anything discussed in this hour is to ensure that you have a boot disk available for your OS, just in case. Oftentimes that can be the install CD-ROM, but most Unixes also let you create explicit boot disks. Check the Unix install documentation if you need help.

## Dual-Boot Configurations with GRUB

GRUB is the GRand Unified Boot loader, originally written by Erich Boleyn in part to sidestep the oft-confusing LILO configuration files. The most popular thing about GRUB is that it's a graphical, menu-based loader (though it does have a simple line-oriented command mode a la LILO).

### Task 11.3: Configuring GRUB

Working with GRUB is a little bit easier than LILO, but you still need to be careful and keep in mind the core functionality of a boot loader. You shouldn't have to change this configuration file too often, but if you do experiment, beware that you might cause lots of trouble, so always make sure you have a copy of the original GRUB configuration for your system as one of the boot-time options.

All the GRUB files, including the graphic used as the background image, live in /boot/grub.

- 1. Here's what's in /boot/grub:

```
# ls -l /boot/grub
total 239
-rw-r--r-- 1 root root 82 Jan 11 15:45 device.map
-rw-r--r-- 1 root root 10848 Jan 11 15:45 e2fs_stage1_5
-rw-r--r-- 1 root root 9744 Jan 11 15:45 fat_stage1_5
-rw-r--r-- 1 root root 8864 Jan 11 15:45 ffs_stage1_5
-rw-r----- 1 root root 543 Jan 11 15:45 grub.conf
lrwxrwxrwx 1 root root 11 Jan 11 15:45 menu.lst -> ../grub.conf
-rw-r--r-- 1 root root 9248 Jan 11 15:45 minix_stage1_5
-rw-r--r-- 1 root root 12512 Jan 11 15:45 reiserfs_stage1_5
-rw-r--r-- 1 root root 54044 Sep 5 13:10 splash.xpm.gz
-rw-r--r-- 1 root root 512 Jan 11 15:45 stage1
-rw-r--r-- 1 root root 120000 Jan 11 15:45 stage2
-rw-r--r-- 1 root root 8512 Jan 11 15:45 vstafs_stage1_5
```

Although you should never touch most of this material without protective clothing (just kidding, but you really do want to be an expert before you fiddle with this!), it's worth highlighting both the GRUB configuration file, grub.conf, and the graphic used as the background image in menu mode, splash.xpm.gz.

![](img/5ced0c78d748bd190e9027e5549a3622_240_0.png)

> Some versions of GRUB look for the configuration in menu.lst rather than grub.conf. Check the man page for the preferences in your own version of Unix, as needed. Notice in the example that menu.lst is a symbolic link to grub.conf.

If you want to have your own custom splash screen, use a program such as xfig to open splash.xpm.gz (after unzipping it, if of course), then duplicate its size, depth (number of colors used) and image format. Then gzip the file and give it the same name, or update the splashimage value in the grub.conf file (see the following).

- 2. More likely, though, you'll want to modify the configuration file, and here's how it looks inside:

```
# cat grub.conf
# grub.conf generated by anaconda
#
# Note that you do not have to rerun grub after making changes to this file
# NOTICE: You have a /boot partition. This means that
# all kernel and initrd paths are relative to /boot/, eg.
# root (hd0,0)
#
```
