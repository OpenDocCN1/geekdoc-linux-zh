
```
label = win
table = /dev/hda

image = /boot/vmlinuz
root = /dev/hda6
label = linux
other = /dev/hda1
label = win2
table = /dev/hda
```

The first option is the boot option, which tells LILO where to install itself. In this case, it's /dev/hda, which tells LILO to install itself on the Master Boot Record of the hard disk. If you use /dev/hda1, LILO will install itself on the boot sector of that partition.

The second option, compact, makes LILO load more quickly. (But this does not work on all systems.) This is useful when LILO is installed on a floppy disk, but if you are installing on a hard disk, the speed difference is not significant.

The vga option tells LILO which screen mode to start with. You can set the resolution of the screen in text mode using this option. Setting it to normal is recommended because it works on all systems. To have LILO give you a list of the available modes at boot up, enter vga=ask.

The read-only option is kernel-specific. It tells the kernel to mount the root filesystem as read-only. Later, as the system boots up, it will be mounted as read-writeable.

The prompt option tells LILO to wait for you to make a choice. This option works with the timeout option. If you have a prompt and don't have a value for timeout, then it will wait forever. This is not recommended because you will never be able to remotely reboot your system since it will stop at the LILO prompt waiting for input.

The timeout option is the number of tenths of a second that LILO should wait before timing out on any keyboard input operations, including the prompt operation.

The next section defines the boot configurations that LILO will handle. Every configuration has to start with either image or other. Use other if you will boot a different operating system or a different installation of Linux. Use image if you want to boot another kernel. Other takes the partition to boot as a parameter, while image takes the path to the kernel to boot as a parameter.

The label option receives the name of the configuration as a parameter. This is the name you would enter to boot this configuration.

The table option comes with the other option. It tells LILO on which device this partition is located. For example, if the partition is /dev/hda1, then the device is /dev/hda.

The root option comes with the image option. This takes the partition to boot as a parameter. This is usually the partition on which your SuSE Linux is installed.

In summary, if you want to create a boot configuration for booting Windows 98 on /dev/hda1 and you want to call it win98, it would look like this in lilo.conf:

```
other = /dev/hda1
label = win98
table = /dev/hda
```

Now all you have to do is save lilo.conf and run /sbin/lilo to apply the changes. When you use YaST, it runs /sbin/lilo for you—that's why when you manually manipulate lilo.conf, you have to run /sbin/lilo yourself.

Other options of interest that you can include the password option. This is a particularly useful option when it comes to security. You can use it to put a password on either LILO as a whole or just on a boot configuration. This way you can block unauthorized people from accessing your whole PC or just from booting a specific operating system.

To put a password on LILO as a whole, just put the option somewhere in the global section like this:

```
password=mypc
```

This will set the word mypc as a password to LILO as a whole. If you want to set a password for a particular boot configuration, just put it with the parameters for that configuration—for example:

```
other = /dev/hda1
label = win98
table = /dev/hda
password=runwin
```

Now, whenever you run the boot configuration win98, you will be prompted to enter a password. You have to take care of something, though. If you are going to use the password option, you have to set lilo.conf to be readable only by root. This is for security because the password is in plain text.

Another option of interest that belongs in the global section is the message option. The message option takes a path to a file as a parameter. LILO will display the contents of this file when booting up, so you can put any message you want in here and it will show up when LILO loads. You have a maximum of 64 KB for this file. You will have to run /sbin/lilo to apply that change.

LILO has a lot of other options that you can use. You can find information about them by reading the man page for lilo.conf.

## Uninstalling and Reinstalling LILO

If LILO has been installed on your master boot record (MBR), situations might arise in which you need to remove it or even reinstall it.

If you install or reinstall Windows 9x, it will overwrite your MBR and thus remove your current installation of LILO. The only way to fix this is to boot your installed Linux system from either your SuSE installation CD or a boot disk, reconfigure your LILO, and then reinstall it. If you don't need to reconfigure LILO to boot the newly installed MS Windows 9x, for example, then you just need to run /sbin/lilo to reinstall LILO on the MBR.

If you need to remove LILO, you need to overwrite your MBR. This can be done using Microsoft's fdisk utility. Either create an MS-DOS boot disk and copy fdisk.exe on it, or boot into Windows 9x and run fdisk from it. The command to remove LILO is as follows:

```
C:\> fdisk /mbr
```

This will replace your MBR with a DOS-based MBR and LILO will be removed.

## LILO Error Interpretation

This section deals with interpreting the errors generated by LILO. LILO does not generate errors in the form of messages because of space limitations. Error messages require space and LILO is limited to just the boot sector. Thus, the error messages that LILO generates are in the word LILO itself. When you start your PC and you see the word LILO, you might think that LILO writes it all at once. What actually happens is that LILO writes it letter by letter after each boot stage is accomplished. The following are the various ways in which LILO gives you an error message:

- **Nothing appears when you start your system**—LILO isn't installed on the system or it isn't written on the boot sector. You might want to reinstall it again.
- **The letter L appears**—LILO is installed, but it cannot continue functioning. It's probably a media failure or incorrect geometry specified in the configuration file.
- **The letters LI appear**—Either the same as the preceding or the file /boot/boot.b does not exist. This error message might also occur if you have an old BIOS in which the boot directory exceeds the 1024-cylinder boundary. However, this situation is very unlikely nowadays.
- **The letters LIL appear**—Probably a geometry mismatch or media failure.
- **The letters LIL? appear**—It's likely the same problems as when LI appears.
- **The letters LIL- appear**—This is a case of geometry mismatch or the file /boot/map not existing.
- **The letters LILO appear**—You're not facing a problem with starting LILO. It should be starting up.

Reconfiguring LILO solves all these problems. If you run into any of these problems, all you have to do is reconfigure LILO to use the correct settings.

Another problem you might face is when you type in the OS you want to load but it doesn't load. If LILO complains about the OS not existing or problems of this kind, you should set up LILO one more time because this indicates that you didn't specify a correct partition.

## init and Runlevels

Recall how you learned that the booting process has two major parts—the first being LILO loading the kernel? Now you get to discover the second phase of the boot up process—init and runlevels.

When Linux boots, control is transferred to the kernel. The kernel boots, initializes the system, installs device drivers for the various hardware you have, and so on. When the kernel is finished, it executes init. init is a program responsible for creating the operating environment. What is meant by operating environment? Let's explain that. When the kernel loads, it prepares the machine to run programs by managing the various resources for them.

init starts a series of other programs that together make up the working environment for the user. These programs include filesystem-checking utilities, network initialization, login prompts, and so on.

### init Scripts

But how does init know what to run? init initializes your whole system using scripts that are called init scripts. These scripts are executed by init one by one; each of them is responsible for preparing a part of the system. For example, the network script handles initializing the network for the system.

init scripts are found under /sbin/init.d/. This directory holds all the scripts that initialize the system. The following are the most common scripts:

| Script | Description |
|---|---|
| boot | This is the first script that init executes. It checks your filesystems for errors, cleans up the system, and so on. |
| boot.local | This script gets called from within boot. It has nothing in it by default. If you want something to be executed when boot is being run, put it in here. |
| apache | This script starts the Apache Web Server. |
| cron | This script starts the cron scheduler daemon. |
| dhclient | This script initializes your network using DHCP. |
| firewall | This script puts up your firewall. |
| gpm | This script sets up mouse control in the console. |
| halt | This script gets called when you halt the system. |
