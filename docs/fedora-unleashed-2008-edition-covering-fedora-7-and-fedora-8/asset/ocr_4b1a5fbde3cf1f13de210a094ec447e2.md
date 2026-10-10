For **iso9660** file systems, the interesting option is *unhide*, which shows hidden and associated files.

The **fstab** man pages contain an in-depth description of **fstab** and its options.

The fifth field of `//etc/fstab` is used by **dump** (a traditional Unix backup program) to determine whether the file system should be *dumped* (backed up); 1 is yes, and 0 is no. Default values are set for you during the initial installation. They are of concern only if you actually use **dump**; then you would set the value to 1 for the file systems you wanted to back up.

The sixth field is used by **fsck** to determine how *fsck* needs to interact with the file system—0 means that **fsck** is never run on the file system (a FAT32 file system, for example); 1 means that **fsck** can be run on the drive at a predetermined time, 2 is recommended for nonroot file systems so that **fsck** is not run on them as frequently.

Here is a simple `//etc/fstab` file from a system with a RAID0 **ext3** root partition and dual-booted with MS Windows:

```
LABEL=/12      /                ext3      defaults       1 1
none            /etc/pts         devpts    gid=5,mode=620 0 0
none            /proc            proc      defaults       0 0
none            /dev/shm         tmpfs     defaults       0 0
/dev/hda1       swap             swap      defaults       0 0
//mnt/cdrom     /mnt/cdrom      iso9660   noauto,owner,kudzu,ro 0 0
/dev/fd0        /mnt/floppy      auto      noauto,owner,kudzu     0 0
/dev/hda1       /mnt/win_c       vfat      auto,quiet,exec 0 0
```

Notice the two entries marked with the **kudzu** option. This is the result of the actions of **upd fstab**, which keeps **fstab** synchronized with the state of any removable devices on the system such as CD-ROMs. The **quiet** option shown for the Windows partition suppresses error messages and is recommended if you use the **Wine** application.

# NOTE

Device labels can be very useful. You can use the label in `//etc/fstab`, and if you have many devices, their labels might be easier for you to remember and track than would be their device names. You can also shuffle around partitions without editing **fstab**, just by changing their labels. The **e2label** command is easier to remember than the analogous **tune2fs** command.

The command **e2label** can display or change a device's label. (You also can change a device label with **tune2fs** –L.) For example, to change the label of `//dev/hda4` to *archives*, use:

```
# e2label /dev/hda4 archives
```

As mentioned earlier, you record mounting preferences in `//etc/fstab` during installation. You need to modify `//etc/fstab` only if you make changes to your mounts or desire to change the default settings to address the specific needs of your system.