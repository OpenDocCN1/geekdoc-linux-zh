# Pass Mode

Pass mode generally is not used for backups. The destination must be a directory on a mounted file system, which means that pass mode cannot be used to transfer files to tape. However, you can use pass mode within cpio to copy files from one directory to another. The advantage of using cpio over cp is that original modification times and ownership are preserved. Specify pass mode by using the -p option in cpio. The following example copies all files from /users to /bkup:

```
cd /users
mkdir /bkup
ls * | cpio -pdu mv bkup
```

Files will be listed to the screen as they are copied.

# pax

Included since Solaris 2.5 is the pax command, a POSIX-conformant archive utility that can read and write tar and cpio archives. It is available on all UNIX systems that are POSIX-compliant, including IBM's AIX, Hewlett-Packard's HP-UX, and Linux.

pax can read, write, and list the members of an archive file, and copy directory hierarchies. The pax utility supports a wide variety of archive formats, including tar and cpio.

If pax finds an archive that is damaged or corrupted while it is processing, pax attempts to recover from media defects. It searches the archive to locate and process the largest possible number of archive members.

The action to be taken depends on the presence of the -r and -w options, which are referred to as the four modes of operation: list, read, write, and copy (described in Table 11.6). The syntax for the pax command is as follows:

```
pax <mode> <options>
```