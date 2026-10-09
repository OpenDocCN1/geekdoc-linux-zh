
## Using GRUB

GRUB is a multiboot boot loader, meaning that it can be used on a system to boot multiple operating systems. GRUB has features that make it an attractive choice as a boot loader. GRUB provides compliance with the Multiboot Specification (http://www.gnu.org/manual/grub-0.92/html_mono/multiboot.htm), a menu interface, a command-line interface, support for diskless systems, and others. More information about the general use of GRUB can be found at http://www.gnu.org/manual/grub/text/grub.txt.

### GRUB Device Names

You must be familiar with GRUB terminology to configure GRUB. GRUB terminology refers to devices with a specific syntax. For example, GRUB refers to the first hard drive on a computer system as `hd0` and to the first partition as `(hd0,0)`.

The syntax of GRUB device names is `(<device_type>,<BIOS_device_number>,<partition_number>)`. The parentheses `()` are mandatory. The `device_type` refers to a hard disk (`hd`) or a floppy drive (`fd`).

`BIOS_device_number` refers to the drive number of the device, starting with zero (0). For example, the first floppy drive would be `(fd0)`.

`partition_number` refers to the partition number of a hard drive. Partitions are numbered starting with zero (0). Extended partitions start with the number four (4). For example, the second hard drive and the second extended partition would be designated `(hd1,5)`.

## Removing a Program Installed from a tar File

As stated earlier in this chapter, tar does not automatically document where files have been installed. When installing a tar application you must document where the files were extracted and what application they go with.

To remove an application installed from a tar, delete the directory or file that was created during installation. For example, to remove the application installed in jsmith's `/home/jsmith/adom` directory, use the `rm -r /home/jsmith/adom` command.

## RPM FILES

The Red Hat Package Management (RPM) system is used to install or upgrade applications (programs) on your Linux operating system. Even though RPM is named after the Red Hat company, it is a shared specification and is widely used by most Linux distributions.

RPM is a tool to manage applications. RPM packages can be easily installed, updated, or removed and can be verified before installation.

The files associated with RPM are:

- **.rpm** Binary packages, precompiled, and platform specific. Usually a RPM package is named something like `squirrelmail-1.4.0-1.i386.rpm` indicating that the package name is `squirrelmail`, the version is `1.4.0`, the build is `1`, and the platform is a 386-type machine.
- **.src.rpm** Source code, not precompiled. These packages must be compiled (built) before installing.

Many options are available for RPM. The most commonly used options are:

- `-i` Install a package
- `-e` Erase a package
- `-U` Upgrade or install a package
- `-F` Freshen an existing package. Do an upgrade if the package exists.
- `-v` Verify an installed package
- `-q` Query an existing package
- `-h` Print 50 hash marks as the package is unpacked
- `-v` Print verbose information

## Installing an RPM Package

Installing a RPM package is a common task for a Linux administrator. RPM is the preferred method for most Linux installations. Most administrators use the command line for package management; but there is also a GUI front end for RPM, which we will look at in this section.

The basic syntax for installation is `rpm -options rpm_filename.rpm` where `rpm_filename.rpm` is the name of the package to install. To install a package named `tftp-server-0.32-4.i386.rpm` (Figure 6–4), use the following command:

```
rpm -ivh tftp-server-0.32-4.i386.rpm
```

The `-h` option causes `#` symbols to display. These symbols are used to visually show the progress of the installation.

> **NOTE**
GRUB does not distinguish between EIDE or SCSI drives. The drives are numbered starting from zero regardless of their type.

> **NOTE**
To specify the MBR (Master Boot Record) of a disk, just leave off the comma and partition. For example, `(hd0)` refers to the first drive.

To specify a file named `vmlinuz` on the first hard drive and on the first partition, you would use the statement `(hd0,0)/vmlinuz`.

### Installing GRUB

GRUB may have been installed during the Linux installation. Many Linux installations install GRUB by default. If this is not the case, installing GRUB manually is relatively easy.

Make sure the latest version of the GRUB package is available. The RPM package name is `grub` and can be queried with the `rpm -q grub` command (Figure 6–10).

![](img/37f079cee226b270f2e09b37a2e4a05d_153_0.png)

In this case the version is 0.93 and the build number is 4. If GRUB is not installed, it may be located on the Linux distribution disk or it can be downloaded from several Internet locations.

From the command prompt you can execute the command `grub-install <location>` where `<location>` is the location where grub should be installed. If grub needs to be installed on the MBR of the first hard drive, you would type the `grub-install /dev/hda` command:

> **NOTE**
The location of the grub-install program can be found with the rpm query program (`rpm -ql grub`).

If another boot loader is already installed, it does not have to be removed before installing GRUB. After GRUB is installed, reboot the computer to see the new GRUB boot loader.

## Booting an Operating System with GRUB

GRUB has two boot methods—load an operating system directly and chain-load another boot loader, which will then boot the operating system. Typically, GRUB will load an operating system directly, but GRUB doesn't support all operating systems, so the chain-load method is necessary.

GRUB is designed to boot multiboot-compliant kernels. Other operating systems require OS-specific commands.

GRUB stores information in a configuration file. GRUB has three interfaces that provide different levels of functionality. Each interface provides commands to boot operating systems.

The **menu** interface provides a menu of operating systems preconfigured with their own boot commands. The arrow keys can be used to select the operating system (OS) to boot. The default OS will boot after a preset timeout period.

The **menu entry editor** interface is displayed by pressing the character **e** while the menu interface is displayed. The menu entry editor allows command lines to be changed before booting the operating system.

The **command-line** interface is very basic, but it allows the most control of the boot process. Within the command line interface, any valid GRUB command can be executed.

When GRUB starts, it looks for its configuration file. When this file is found GRUB uses it to build the menu list of operating systems, then displays the menu interface. If the configuration file is not present, GRUB will load the command line interface to allow entering commands directly to start the operating system.

## GRUB Commands

GRUB provides several commands that can be used in its interfaces to start operating systems. A full list of commands is displayed by typing the `info grub` command. Some of the commands are:

- **boot**: Boots the operating system or chain loader specified. This command is entered after boot parameters are defined.
- **chainloader <filename>**: Loads the specified file as a chain loader. A + 1 can be entered to use the file at the first sector of the specified partition.
- **initrd <filename>**: Specify an initial RAM disk to use when booting.
- **kernel <kernel_filename> options**: Specifies the kernel file to load.
- **root <device_partition>**: Configures the root partition to be used and mounts the partition.

![](img/37f079cee226b270f2e09b37a2e4a05d_155_0.png)

```
# /etc/grub.conf generated by anaconda

# Note that you do not have to rerun grub after making changes to this file

# NOROOT: You have a /boot partition: This means that
# all kernel and initrd paths are relative to /boot/, eg.
# root (hd0,0)
# kernel /vmlinuz-version ro root=/dev/sda2
# initrd /initrd-version.img

#root=/dev/sda
default=0
timeout=10
splashimage=(hd0,0)/grub/splash.xpm.gz
title Red Hat Linux (2.4.20-8smp)
root (hd0,0)
kernel /vmlinuz-2.4.20-8smp ro root=/dev/sda2
initrd /initrd-2.4.20-8smp.img

title Red Hat Linux-up (2.4.20-8)
root (hd0,0)
kernel /vmlinuz-2.4.20-8 ro root=/dev/sda2
initrd /initrd-2.4.20-8.img
```

The following are special commands for the menu interface:

- **color = <foreground/background>** Allows the menu interface to display specific colors for menu items.
- **default = <#>** Determines which entry on the menu interface will be selected and loaded if the interface times out.
- **timeout = <#>** Sets the number of seconds GRUB will wait for menu selection. If timeout is reached, GRUB boots the indicated default operating system.
- **splashimage = <device_partition>/<filename>** Defines where the splash screen image can be located.
- **title <title_name>** Sets a title for the menu display.

In Figure 6–11 the default is set to 0. The value 0 indicates that the first title from the `menu.lst` file will be the default entry on the menu interface. The timeout is set to 10, indicating that a user has ten seconds before GRUB loads the default operating system. The splash image has a value of `(hd0,0)/grub/splash.xpm.gz`, indicating that the splash image is in directory `/grub`, has a name of `splash.xpm.gz`, and is on the first hard drive’s first partition. The title is `Red Hat Linux (2.4.20-8smp)`. This is the title that will be displayed on the menu interface.

Regardless of the interface, the commands to boot the system are the same.

To boot a multi boot operating system, follow these steps:

1. Set the GRUB root device to the drive in which the OS images are stored with the command **root**.
2. Use the **kernel** command to load the operating system kernel.
3. Execute the **boot** command to load the operating system.

To boot a GNU/Linux operating system, follow these steps:

1. Set the GRUB root device to the GNU/Linux drive. For example, **root (hd0,0)** selects the first partition on the first hard drive.
2. Load the kernel. For example, **kernel /vmlinuz-2.4.20-8smp ro root=/LABEL=** loads the `vmlinuz-2.4.20-8smp` kernel.
