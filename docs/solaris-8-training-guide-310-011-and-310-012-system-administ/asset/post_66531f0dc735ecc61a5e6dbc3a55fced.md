
- Backups made by cpio are smaller than those created with tar because the header is smaller.
- cpio can span multiple tapes; tar is limited to a single tape.

Because of its flexibility, cpio has more options, and is perceived as a more complex command than tar.

The cpio program operates in one of three modes: copy-out (cpio -o), copy-in (cpio -i), or pass (cpio -p). Use copy-out when creating a backup tape and copy-in when restoring or listing files from a tape. The pass mode is generally used to copy files from one location to another on disk. You must always specify one of these three modes. The command syntax for the cpio command is as follows:

```
cpio <mode> <option>
```

in which mode is -i, -o, or -p, and option is an option from Table 11.5.

## TABLE 11.5

### COMMAND OPTIONS FOR cpio

| Option | Description |
| --- | --- |
| -c | Writes header information in ASCII format for portability. |
| -d | Creates as many directories as needed. |
| -B | Specifies that the input has a blocking factor of 5120-byte records instead of the default 512-byte records. You must use the same blocking factor when you retrieve or copy files from the tape to the hard disk as you did when you copied files from the hard disk to the tape. You must use this option whenever you copy files or file systems to and from a tape drive. |
| -v | Verbose. Reports the names of the files as they are processed. |
| -u | Copies unconditionally. Without this option, an older file will not replace a newer file that has the same name. |
| -m | Retains the previous file modification time. This option is ineffective on directories that are being copied. |

## cpio Examples

The following example shows how to copy the directory /work and its subdirectories to a tape drive with the device name /dev/rmt/0. The -o option specifies copy-out mode, -c will output the header information in ASCII format, and I'm using the -B option to increase the blocking factor to 5120 bytes to improve the speed.

```
cd /work
ls -R | cpio -ocB > /dev/rmt/0
```

The next example shows how to copy the files located on a tape back into the directory named /work on a hard disk:

```
cd /work
cpio -icvdB < /dev/rmt/0
```

The -i option specifies copy-in mode, -d will create directories as needed to restore the data to the original location, and -v will display all the output.

## Backing Up Files with Copy-Out Mode

To use copy-out mode to make backups, you send a list of files to the cpio command via the standard input of cpio. In practice, you'll use the UNIX find command to generate the list of files to be backed up. Copy-out mode is specified by using the -o option on the cpio command line. In the next example, a file named "list" contains a short list of files to be backed up to tape:

```
cpio -ovB list > /dev/rmt/1
```

Normally, as indicated in Table 11.5, cpio writes files to the standard output in 512-byte records. By specifying the -B option, you increase the record size to 5120 bytes to significantly speed up the transfer rate, as shown in the previous example. You can use UNIX commands to generate a list of files for cpio to back up in a number of other ways, as shown in the following examples.

You can back up files by entering filenames via the keyboard. Press Ctrl+D when you have finished typing filenames. Type the following:

```
cpio -o > /dev/rmt/1
File1.txt
File2.txt
```

You can use the ls command to generate the list of files to be backed up by cpio. Type the following:

```
cd /home/bcalkins
ls * | cpio -o >/dev/rmt/1
```

Use the find command to generate a list of files that the user bcalkins created and modified in the past five days. This is the list of files to be backed up:

```
find . -user bcalkins -mtime -5 -print | cpio -o > /dev/rmt/1
```

If the current tape fills up, the cpio program prompts you for another tape. You see a message that says the following:

```
If you want to go on, type device/file name when ready
```

You should then change the tape and enter the name of the backup device (for example, /dev/rmt/1).

## Restoring Files with Copy-In Mode

Use the copy-in mode of cpio to restore files from tape to disk. The following examples describe methods used to restore files from a cpio archive.

This first example restores all files and directories from tape to disk. The cpio options specified will restore files unconditionally (-u) to the /users directory, and will retain previous file modification times (-m). Type the following:

```
cd /users
cpio -icvumB < /dev/rmt/1
```

The next example selectively restores files that begin with “database.” The -d option will create directories as needed. Type the following:

```
cpio -icvdumB 'database*' < /dev/rmt/1
```

> NOTE Single quotes must be used to pass the wildcard argument (*) to cpio.

To obtain a list of files that are on tape, follow the next example:

```
cpio -ictB < /dev/rmt/1
```

The list of files on /dev/rmt/1 will appear onscreen.

## Pass Mode

Pass mode generally is not used for backups. The destination must be a directory on a mounted file system, which means that pass mode cannot be used to transfer files to tape. However, you can use pass mode within cpio to copy files from one directory to another. The advantage of using cpio over cp is that original modification times and ownership are preserved. Specify pass mode by using the -p option in cpio. The following example copies all files from /users to /bkup:

```
cd /users
mkdir /bkup
ls * | cpio -pdu bkup
```

Files will be listed to the screen as they are copied.

## pax

Included since Solaris 2.5 is the pax command, a POSIX-conformant archive utility that can read and write tar and cpio archives. It is available on all UNIX systems that are POSIX-compliant, including IBM's AIX, Hewlett-Packard's HP-UX, and Linux.

pax can read, write, and list the members of an archive file, and copy directory hierarchies. The pax utility supports a wide variety of archive formats, including tar and cpio.

If pax finds an archive that is damaged or corrupted while it is processing, pax attempts to recover from media defects. It searches the archive to locate and process the largest possible number of archive members.

The action to be taken depends on the presence of the -r and -w options, which are referred to as the four modes of operation: list, read, write, and copy (described in Table 11.6). The syntax for the pax command is as follows:

```
pax <mode> <options>
```

## TABLE 11.6

### Four Modes of Operation for pax

| Option | Operation Mode | Description |
|---|---|---|
| -r | Read mode | When -r is specified but -w is not. pax extracts the filenames and directories found in the archive file. The archive file is read from disk or tape. If an extracted file is a directory, the file hierarchy is extracted as well. The extracted files are created relative to the current file hierarchy. |
| None | List mode | When neither -r nor -w is specified. pax displays the filenames or directories found in the archive file. The archive file is read from disk, tape, or the standard input. The list is written to the standard output. |
| -w | Write mode | When -w is specified, but -r is not. pax writes the contents of the file to the standard output in an archive format specified by the -x option. If no files are specified, a list of files to copy (one per line) is read from the standard input. A directory includes all the files in the file hierarchy rooted at the file. |
| -rw | Copy mode | When both -r and -w are specified. pax copies the specified files to the destination directory. |

In addition to selecting a mode of operation, you can select one or more options from Table 11.7.

## TABLE 11.7

### COMMAND OPTIONS FOR pax

| Option | Description |
|---|---|
| -r | Reads an archive file from standard input and extracts the specified files. If any intermediate directories are needed to extract an archive member, these directories are created. |
| -w | Writes files to the standard output in the specified archive format. When no file operands are specified, standard input is read for a list of pathnames—one per line, without leading or trailing blanks. |
