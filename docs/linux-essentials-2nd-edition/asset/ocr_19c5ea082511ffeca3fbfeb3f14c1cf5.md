# Managing Displays

![](bbox=[0.052, 0.096, 0.676, 0.473])

FIGURE 5.3 Linux file managers enable you to unmount removable media.

Most removable disks are unpartitioned or have a single partition. They frequently use FAT, which is a good choice for cross-platform compatibility. If you need, you can partition USB flash drives and most other removable media.
Optical discs are unusual in that they require their own special filesystems (ISO-9660 or UDF). Although you can mount and unmount these discs just like other disks, you can only read them, not write to them. If you want to create an optical disc filesystem on blank media, you must use special software, such as the text-mode mkisofs, cdrecord, or growsofs, or the GUI K3b or X-CD-Roast. These tools create an ISO-9660 filesystem from the files you specify and then burn it to the blank disc. Thereafter, you can mount the disc in the usual way.

# Managing Displays

Linux provides two display modes: text-mode and GUI. A text-mode display is fairly straightforward and requires little or no management. GUI displays, on the other hand, are more complex. In Linux, the X Window System (or X for

Certification Objective