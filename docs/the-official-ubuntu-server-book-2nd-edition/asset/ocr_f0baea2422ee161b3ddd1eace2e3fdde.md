+   - **Choose a different root file system**  
+     This option is pretty self-explanatory. If you happened to choose the wrong root file system, this option will let you change it.
+   
+   - **Reboot the system**  
+     Here is another self-explanatory option. Once you are finished with your system recovery, choose this option to reboot.

> > **NOTE**  
> > When you are within either of the shell environments you can type `exit` to return to the rescue operations menu.

# Recover GRUB

I have already mentioned the “Reinstall GRUB boot loader” option from the rescue operations menu. This will reinstall GRUB to the disk or partition of your choice, but sometimes GRUB itself is installed but its configuration file is missing or corrupted. When this happens, instead of a GRUB menu at boot time, you may not see anything at all. To fix this problem, choose the menu option to execute a shell within your root partition. Once there, run

```
```bash
# update-grub
```
```

This option will create a new /boot/grub/grub.cfg file based on your available kernels. Once it completes, you can type `exit` to return to the main menu and reboot the system.

# Repair the Root File System

Typically the recovery CD will attempt to mount the root file system if possible. If it can mount the root file system, then you will not be able to unmount it and run any tools such as fsck on it. Of course, if the rescue CD were able to mount the file system, you wouldn’t need to fsck it now, would you? If the root file system is corrupted and the rescue CD can’t mount it, then drop to the installer shell and run

```
```bash
# fsck -y /dev/sda1
```
```