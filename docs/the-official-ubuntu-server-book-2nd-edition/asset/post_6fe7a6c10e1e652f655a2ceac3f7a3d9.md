
![](img/304f637afcecc491b152ee8ac5afadee_485_0.png)

## Figure 12-2 Recovery operations menu

- Execute a shell in the installer environment

The bulk of your recovery work will likely occur from this option. Choose this and you will drop to a BusyBox shell on the install CD itself. The root file system will be mounted under /target so you could potentially edit configuration files from this mode. The advantage to this mode is that it exists outside of the actual root file system, so you can do things such as run fsck on the root partition—something that wouldn’t be allowed if you had booted into the system itself.

- Reinstall GRUB boot loader

One of the most common reasons why you might boot into a rescue CD is that GRUB is broken. Without GRUB you can’t boot into the system without some serious Linux kung fu. Choose this option and an automated script will reinstall GRUB onto the disk or partition of your choice. Most people tend to install GRUB on the master boot record, so when you are prompted for a location to install GRUB you will probably choose (hd0). Note that if the rescue CD can’t locate the grub configuration files under /boot/grub, this won’t appear.

- Choose a different root file system
This option is pretty self-explanatory. If you happened to choose the wrong root file system, this option will let you change it.

- Reboot the system
Here is another self-explanatory option. Once you are finished with your system recovery, choose this option to reboot.

> **NOTE**
> When you are within either of the shell environments you can type `exit` to return to the rescue operations menu.

## Recover GRUB

I have already mentioned the “Reinstall GRUB boot loader” option from the rescue operations menu. This will reinstall GRUB to the disk or partition of your choice, but sometimes GRUB itself is installed but its configuration file is missing or corrupted. When this happens, instead of a GRUB menu at boot time, you may not see anything at all. To fix this problem, choose the menu option to execute a shell within your root partition. Once there, run

```bash
# update-grub
```

This option will create a new /boot/grub/grub.cfg file based on your available kernels. Once it completes, you can type `exit` to return to the main menu and reboot the system.

## Repair the Root File System

Typically the recovery CD will attempt to mount the root file system if possible. If it can mount the root file system, then you will not be able to unmount it and run any tools such as fsck on it. Of course, if the rescue CD were able to mount the file system, you wouldn’t need to fsck it now, would you? If the root file system is corrupted and the rescue CD can’t mount it, then drop to the installer shell and run

```bash
# fsck -y /dev/sda1
```

Replace /dev/sda1 with the path to your root partition. If fsck complains about a bad superblock, follow the steps in the File System Corruption section above under Ubuntu Recovery Mode. Otherwise, depending on how damaged your file system is, you might see fsck output the errors that it finds as it attempts to repair them.

In addition to the specific rescue steps I listed above, you should be able to perform all of the recovery steps from the GRUB recovery mode. Just choose the "Execute a shell in /dev/ubuntu/root" (it will replace /dev/ubuntu/root with the root partition you selected) from the recovery operations menu and follow the same steps.

## Ubuntu Desktop Live CD

There are certain system rescues you need to perform that require you to boot outside of the server itself. Any system imaging, root partition fsck commands, or any other time that / needs to be unmounted you will need some sort of rescue disc. While I have already mentioned how you can use the Ubuntu Server install CD as a rescue disc, unfortunately you are limited by the tools present on that CD. There are a number of different live CDs available that provide the same set of tools, such as Knoppix and DSL, but since I assume it's more likely you will have an Ubuntu Desktop install CD around and it doubles as a live CD, I discuss some more advanced recovery techniques you can perform from the CD.

## Boot the Live CD

The first step is to boot the live CD into the standard GNOME desktop. Don't worry if your server doesn't have a sophisticated video card since basically everything I describe can be done from the command line.

## Add the Universe Repository

Once the live CD boots into the desktop, you need to add the universe repository to its list of package repositories. All of the tools I use here come from packages in the universe repository, so either click System_Administration_Software Sources and make sure that the Community-maintained Open Source software (universe) option is checked, or open a terminal
