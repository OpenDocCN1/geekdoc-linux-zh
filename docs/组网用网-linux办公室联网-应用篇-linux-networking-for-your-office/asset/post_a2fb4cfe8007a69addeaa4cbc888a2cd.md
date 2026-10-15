
![](img/5d4d3092919d1d16884788127447cc6d_150_0.png)

## FIGURE 5.10

LILO presents a lot of options across six linuxconf entries, but you won’t use most of these in practice.

You can configure LILO by using just a few items in the linuxconf setup. Here are some of the highlights:

- LILO defaults, Base options, Install boot sector on—This is where LILO installs itself. To use LILO as a primary boot loader, it needs to be on /dev/hda or /dev/sda. As a secondary loader, it needs to be on your Linux partition (such as /dev/hda2 in Figure 5.10).
- LILO defaults, Base options, Prompt timeout in seconds—This option controls how long the LILO boot: prompt remains on the screen before LILO boots the default option.
- LILO linux configurations—This screen controls the Linux boot configurations. There should be one of these configurations on your installation, created by the Red Hat installer. Click it, and a new tab appears for controlling it. You can create new configurations, say for testing a new kernel.
- LILO linux configurations, Linux boot configuration, Label—The label is what you type to boot this configuration.
- LILO linux configurations, Linux boot configuration, Kernel image file—You must tell LILO where the kernel is located in order to boot Linux.
- LILO linux configurations, Linux boot configuration, root partition—You must tell LILO what partition is the root of your filesystem hierarchy. The kernel looks there for additional configuration files.
- LILO other OS configurations—You can add non-Linux OSs using this portion of the linuxconf LILO area.
- Default boot configuration—Here you can select any of the Linux or other OS configurations to be the default.
- A new kernel—You can use this item to quickly install a new kernel image in LILO. You must specify the kernel file, give it a label, and so on.
- A new kernel you have compiled—If the utility can spot a freshly compiled kernel, linuxconf can add the new kernel to LILO quite easily when you click this tab.

## Configuring LILO with Text Files

If you want to configure LILO the old-fashioned way, you can load the /etc/lilo.conf file into your favorite text editor. Here’s a sample lilo.conf file that demonstrates booting from either of two Linux kernels:

```
boot=/dev/hda2
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
image=/boot/zImage-2.2.8
    label=228
    root=/dev/hda8
    read-only
image=/boot/zImage-2.2.9
    label=229
    root=/dev/hda8
    read-only
```

The first line (boot=/dev/hda2) specifies where to place LILO itself. This location is normally /dev/hda or /dev/sda for a primary loader, or a specific partition, such as /dev/hda2, for a secondary loader. The next three lines set standard options, and shouldn’t be changed. The timeout line specifies the time the prompt remains on the screen, in tenths of a second. Each of the lines that begins with image specifies a separate Linux boot image, and each image specification includes several subsidiary lines. The image line itself identifies the Linux kernel. The label and root lines specify the boot label and the root filesystem, respectively. The read-only line indicates that the filesystem is to be mounted in read-only mode initially, which is normal; later in the boot process, Linux remounts the filesystem in full read/write mode. Unless otherwise specified, the first system specification in the file becomes the default.

You can learn more about the format of the lilo.conf file by typing man lilo.conf at a Linux command prompt.

When you edit your /etc/lilo.conf file, you must be sure to reinstall LILO so that the changes take effect. LILO is really two things: The code that goes in the boot sector and a program for creating that code and putting it there, based on the contents of the /etc/lilo.conf file. The latter task is handled by a program called lilo, located in the /sbin directory, so to install LILO the boot loader, you type /sbin/lilo, or just lilo if /sbin is on your search path. You’ll see messages to the effect that each system specification in the file has been added. If there’s an error in the process, you’ll see an error message, and none of your changes will take effect.

## Setting Up User Accounts

Linux is designed as a multiuser operating system. As such, the concept of different accounts for different users is common throughout the OS—from the need to log in, to ownership and permissions on files. Because file and printer sharing operations interact closely with the security needs of Linux, you’ll need to be quite familiar with operations relating to account creation and maintenance, file permissions, and so on. This section therefore covers some of this material.

## The Importance of User Accounts

The use of separate user accounts provides several key benefits to Linux, just as it does to other UNIX-like operating systems:

- User privacy—On most operating systems designed for desktop use, there’s no concept of user accounts, and anybody who sits down to use the system can access all the files on the system. If you want to share such a computer with another person, the only way to ensure that the other user can’t read your files is to encrypt them, and that’s awkward for you. User accounts let you keep prying eyes away from your data.
- Multiuser access—Several people can use a single Linux computer simultaneously, by using terminals or other networked computers. Keeping separate accounts helps keep the separate actions of these individuals from interfering with one another.
- Access control—User accounts allow a computer to be placed in a public location without fear that it will be used by unauthorized individuals. (This applies both to physical location and to access via a network.) Of course, even a single-user OS such as DOS can be outfitted with a password-protection scheme, but without implementing at least a minimal system of user accounts, there’s no way to track just who used the computer when.
- System protection—An OS with differing levels of permissions for different users, such as Linux implements, allows the OS to protect itself from both user error and malicious actions. For instance, it’s notoriously easy for a user of most traditional desktop OSs to wipe out the entire OS, just by deleting a critical directory. Although this is possible in
