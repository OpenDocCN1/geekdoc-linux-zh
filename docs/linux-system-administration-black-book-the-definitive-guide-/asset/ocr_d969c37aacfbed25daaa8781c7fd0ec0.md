system listing. The mount point for a permanently mounted item still has to exist on the root file system before you will be able to mount the device. For example, the /boot directory had to exist on the root file system before the /boot partition could be inserted at that location.

+   11. Determine the type of file system you are mounting. Usually, this file system type is ext2 for a permanently mounted device. The options listed in Table 3.11 earlier in the chapter are all available to you, and more.

> TIP: Type “man mount” for a full listing of file system types and mount options.

+   12. Choose the options you want the file system segment to be mounted with. Table 3.12 outlines a number of commonly used options. It is often a good idea to consider the “defaults” choice first. If you want to use more than one option, separate them with a comma and no spaces.

# Table 3.12 Mount options often used in /etc/fstab.

| Option | Purpose |
| :--- | :--- |
| async | Does all input and output to this segment of the file system independently of each another. |
| auto | Mounts this portion of the file system automatically at boot time. |
| defaults | Includes the following options: async, auto, dev, exec, nouser, rw, and suid. |
| dev | Utilizes both character and block special devices on this portion of the file system. |
| exec | Contains all the binaries on this portion of the file system to be executed. |
| noauto | Does not allow this portion of the file system to be mounted automatically. |
| nodev | Ignores both character and block special devices on this part of the file system. |
| noexec | Does not allow the binaries on this part of the file system to be executed. |
| nosuid | Does not accept SUID or SGID bits. |
| nouser | Excludes nonroot users from mounting this portion of the file system. |
| ro | Mounts the file system as a read-only device. |
| rw | Mounts the file system as a read-write device. |
| suid | Accepts SUID and SGID bits. |
| sync | Does all input and output to this segment of the file system as an orderly stream of data. |
| user | Allows nonroot users to mount the device onto the file system. Useful for floppy and CD-ROM devices if you want to allow users access to them. Includes the following options: nodev, noexec, and nosuid. |