# Unmounting a Netatalk Volume

You unmount a Netatalk volume in the same way you unmount any other volume in MacOS: by dragging its icon to the trash. The Macintosh then tells Netatalk that the volume is no longer needed, and the connection is closed. If you unmount all volumes from a given server, you might need to reenter your username and password if you try to mount a volume again. Otherwise, the Macintosh remembers your username and password, so you can remount the volume a bit more easily.

Occasionally, a Macintosh program opens a file and doesn’t properly close the OS handle on the file. This makes it difficult to unmount the disk in Linux. If you’re accessing files on a hard disk, such an occurrence isn’t normally a problem, but it can be if you’re sharing removable media. In such cases, the solution is to either close the program that’s holding the file open unnecessarily or to unmount the share in MacOS. Occasionally the latter option may be the only choice. Sometimes you can simply wait a minute or two, and the program belatedly removes its lock on the file, allowing you to unmount the disk from Linux.

# Sharing Removable and Networked Media

You can export removable media and those that Linux has mounted from other servers. Figure 12.4 shows a Macintosh that has mounted several filesystems from a Linux Netatalk server:

+   - A Windows NT C: drive mounted using Samba’s smbmount utility
+   - A Joliet CD-ROM disc read by Linux
+   - A standard Linux home directory, rodsmith
+   - A Macintosh HFS Zip disk read by Linux

Whatever the source of the filesystems, the basic principles are the same as far as both Netatalk and MacOS are concerned. Chapter 9, "Basic Principles of File Sharing," discusses different methods of sharing removable media.

A few further comments are in order with respect to sharing Macintosh HFS media, including Macintosh CD-ROMs, Zip disks, and floppies:

+   - You should use the conv=netatalk and afp d options. The former option sets up Linux’s HFS driver to display the resource forks as Netatalk does, and the latter option refines this display to allow better read/write access to the media from Macintoshes.
+   - Standard PC hardware cannot read the low-level format of 400KB and 800KB floppies, so you can’t mount these media in Linux. PC hardware and Linux have no problems with 1.44MB Macintosh floppies, though.