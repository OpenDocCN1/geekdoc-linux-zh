# #4 I'm having problems with Windows

Go on, own up, some of you also use Windows, or have a "friend" who does. Rescapp also has options for repairing Windows systems, from resetting passwords to making users into administrators and other user management. It also has an option to restore the Windows MBR. The section on repairing Grub only applies if you still have at least one Linux distro installed. If you want to remove all Linux partitions from a drive, you will need to remove Grub from its boot sector and reinstall the Windows bootloader. Rescapp does this with the Restore Windows MBR button. Choose a disk, as with the Grub restore, and it will set up your hard disk to use the Windows bootloader.

# #5 It's complicated

So far, we have looked at solutions to standard problems that can be deal with by a couple of mouse clicks. If things get more complicated. Rescatux contains much of the other software found on rescue discs, and you can just open a terminal and use it, but it will come as no surprise that you can also use more advanced tools from the Expert Tools section of Rescapp. These tools include:

+   - **Gparted** – for (re)partitioning your hard disk.
- **Testdisk** – to find partitions and filesystem on disks with a damaged partition table.
- **PhotoRec** – to recover deleted or otherwise lost files from a disk, and not only photos.
- **OS Uninstaller** – for removing extra distros from a multi-boot system

It is worth noting that the Expert Tools buttons still open a help page first, but this is generic help for Rescatux, not help for the individual programs.

Apart from those single-use programs, there is also Boot Repair which opens a window containing many options for altering the boot process.

This covers a number of operations, especially if you enable the Advanced options. It allows you to back up your partition tables and log files to a USB device, a wise step before you start changing things. Most of the other options in here let you tweak how the bootloader works. You can reinstall, as with the separate button covered elsewhere,

GPT for the newer GPT variant, the other choices are rather specialist. Removable drives occasionally use the None option, but usually have a single partition with an MBR partition table. Select Analyse to scan the disk's partition table and then Deeper Scan to search for lost partitions. If you find what you are looking for, Write will hopefully restore your lost settings. Although it is not mentioned in all the menus, pressing Q usually takes you back to the previous menu. Testdisk is a very low-level tool, and its effects may not be reversible, where possible use dd to make a backup of your disk before proceeding.

If you deleted files rather than partitions, the tool you want is PhotoRec. Photorec scans the disk for evidence of files and then attempts to reconstruct them – you will need another disk attached for saving these files to. Photorec can only find the contents of files, metadata such as ownerships, permissions and even the file name is not available to it.

So you end up with a lot of files with numeric names, although PhotoRec does give them a suitable extension based on the contents of the file. If the files are digital camera photos (PhotoRec was originally written to recover files from an erased memory card) or music files, you should find that any EXIF or ID3 tagging is preserved, making identification of the files relatively simple. Otherwise, you may have to spend some time trawling through the files to identify them, but that is better than losing your data altogether.

Forget your password? Rescapp lets you reset the password of any Linux or Windows users, including root, with a couple of mouse clicks.

![](bbox=[0.23, 0.47, 0.56, 0.64])

# Boot an ISO from Grub

Rescue discs are great, as long as you can find the thing when you really need it. You can copy an ISO image to a USB drive with dd

```
dd if=/lxfdvd/downloads/rescatux_cdrom_usb_hybrid_i386_amd64-486_0.32b1.iso of=/dev/sdX bs=4k
```

where sdX is your USB drive. That is more convenient, but Murphy's Law states that you won't be able to find the drive when you need it, so there is a more convenient option. To save you going through your pile of LXF DVDs to find the one with Rescatux on it, here is how to boot it from your hard drive.

You need a working Grub2, so it is not an option in all cases, but if Grub and your boot partition are working it is more convenient, and faster. Put the ISO image into your /boot

directory, then add the following to the bottom of the file /etc/grub.d/40_custom (do not modify the existing lines.)

```
submenu "Rescatux 0.32" {
  set isofile=/Rescatux/rescatux_cdrom_usb_hybrid_i386_amd64-486_0.32b1.iso
  loopback loop $isofile
  menuentry "Rescatux 0.32 - 64 bit" {
    linux (loop)/live/vmlinuz1 findiso=$isofile
    boot=live config quiet splash
    initrd (loop)/live/initrd1.img
  }
  menuentry "Rescatux 0.32 - 32 bit" {
    linux (loop)/live/vmlinuz2 findiso=$isofile
    boot=live config quiet splash
    initrd (loop)/live/initrd2.img
  }
}
```

```
initrd (loop)/live/initrd2.img
}
```

Now run update-grub or grub-mkconfig, or use the Update Grub Menus option in Rescapp, to update your menu. Then, when you reboot your system, you will have an option to boot into Rescatux.

```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

If trying to boot from it gives an error that the ISO file could not be found, add this below the submenu line

```
set root='(hd0,1)'
```

where hd0,1 refers to the first partition on the first disk (for some reason Grub counts disks from zero and partitions from one. Adjust to suit your system.