TABLE 5.2 Important Filesystem Options for the mount Command (continued)
| Option | Supported Filesystems | Description |
|---|---|---|
| gid=value | Most filesystems that don't support Unix-style permissions, such as vfat, hpfs, ntfs, and hfs | Works like uid=value, but sets the group of all files on the filesystem. You can find group IDs in the /etc/group file. |
| umask=value | Most filesystems that don't support Unix-style permissions, such as vfat, hpfs, ntfs, and hfs | Sets the umask for the permissions on files. value is interpreted in binary as bits to be removed from permissions on files. For instance, umask=027 yields permissions of 750, or-rwxr-x---. Used in conjunction with uid=value and gid=value, this option lets you control who can access files on FAT, HPFS, and many other foreign filesystems. |
| conv=code | Most filesystems used on Microsoft and Apple OSs: msdos, umsdos, vfat, hpfs, hfs | If code is b or binary, Linux doesn't modify the files' contents. If code is t or text, Linux auto-converts files between Linux-style and DOS- or Macintosh-style end-of-line characters. If code is a or auto, Linux applies the conversion unless the file is a known binary file format. It's usually best to leave this at its default value of binary because file conversions can cause serious problems for some applications and file types. |
| norock | iso9660 | Disables Rock Ridge extensions for ISO-9660 CD-ROMs. |
| nojoliet | iso9660 | Disables Joliet extensions for ISO-9660 CD-ROMs. |

Some filesystems support additional options that aren't described here. The man page for mount covers some of these, but you may need to look to the filesystem's documentation for some file-systems and options. This documentation may appear in /usr/src/linux/Documentation/filesystems or /usr/src/linux/fs/fname, where fname is the name of the filesystem.

# Unmounting a Filesystem

Sometimes you don't want to leave a filesystem mounted permanently. This is most often the case for removable media, but if you need to perform maintenance or alter your partition layout, you need to unmount even a filesystem that's normally mounted. In either case, the tool to use is umount:

```
```
# umount /home2
```
```