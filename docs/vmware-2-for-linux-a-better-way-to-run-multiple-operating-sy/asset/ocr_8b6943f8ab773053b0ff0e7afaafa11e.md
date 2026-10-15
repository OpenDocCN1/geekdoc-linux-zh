+   - The host Linux OS needs free disk space equal to the current size of the virtual disk you want to shrink. Ironic, isn’t it? After all, you’ll probably start thinking about shrinking your virtual disks when your Linux PC starts to run out of room. But unfortunately, the shrink process needs a buffer as big as the virtual disk it will optimize to work. Prevention is the best medicine, after all.
+   - The virtual machine cannot have any raw or plain disks connected to it when you start the shrink process. Trying to shrink a raw or plain disk would have undesirable results (because they don’t work like virtual disks), so VMware decided that discretion was the better part of valor and it will not let you access the Shrink command if you have raw or plain disks attached to your virtual machine. You can always temporarily remove them from the VMware configuration, boot up just to shrink the disk, and then re-attach them when the shrink process is complete.
+   - The virtual disk needs to be in persistent mode. There is no point to shrinking a nonpersistent or undoable disk, so VMware doesn’t let you.
+   - Shrinking a virtual disk that is very full, or has never been very full, is not beneficial. If the virtual disk truly is full, there’s nothing VMware can do: Shrinking is not a disk-compression routine. And if the virtual disk has never contained much data, there is little dead space to eliminate. Ideally, you should shrink disks after you have deleted a large number of files.

# Shrinking Virtual Disks

Shrinking virtual disks is a two-stage process. The first stage takes place inside the Windows virtual machine, when you select which drive you want to shrink and VMware Tools does some preparation work. Then, VMware itself takes over, temporarily freezing the virtual machine while the shrinking operation takes place.

Assuming your setup is in line with the guidelines listed earlier, you are ready to begin:

+   1. Double-click the VMware Tools icon in the system tray.
+   2. Click the Shrink tab, shown in Figure 8.7.
+   3. VMware automatically lists the disks it can shrink. On a typical VMware setup (with one virtual disk, one floppy, and one CD-ROM drive), the virtual disk C:, appears in the supported list, and floppy drive A: and CD-ROM drive D: show up in the Unsupported Partitions tab (see Figure 8.8).
+   4. Put a checkmark next to the supported drive you want to shrink. (If there is only one, it is selected by default.)
+   5. Click Prepare to shrink. VMware Tools works on the drive for a while—if you have a particularly sluggish or overloaded machine, or the virtual disk is particularly cluttered, the shrinking procedure may take the better part of an hour. A progress bar, shown in Figure 8.9, will keep you informed.