# # File System Types

. Linux uses a large set of file systems on its storage devices, including

+   - ext2—The default Linux file system.
+   - ext3—Essentially ext2 with journaling (logging).
+   - iso9660—The CD-ROM file system.
+   - udf—The DVD file system.
+   - minix—Obsolete; it’s not present on all systems.
+   - vfat—A 32-bit file system (Windows FAT32).
+   - msdos—A 12- or 16-bit FAT file system.
+   - umsdos—An extended Linux version of msdos file system.
+   - proc—A virtualized file system that represents the kernel’s processes and structures.
+   - nfs—Nearly obsolete; it’s the OS/2 file system.
+   - sysv—System V file system that incorporates support for multiple Unix file systems.

+   - nts—The Network File System by Sun Microsystems, which is the default network file sharing protocol for all of Unix/Linux.
+   - smb—The Samba file system is Microsoft’s default file sharing protocol for network shares. It’s otherwise known as CIFS (Common Internet File System).

![](bbox=[0.06, 0.68, 0.19, 0.79])

> For a more extensive description of all the file systems available under Linux, use the man 5 fs command.
> 
> Very little mention is made of ReiserFS, JFS, and XFS on the exams. The only questions about these file systems seem to be to determine which file system is the easiest to upgrade to from an ext2 file system—that being ext3, without a doubt.

# ## Creating File Systems

When a proper partition exists for the file system to reside on, creating the file system takes a relatively short time, although the options available are extensive.