
## 27.1.1 Listing the Contents of a DOS Disk

Use mdir to get a directory listing of a DOS disk. Give as an argument the "drive letter" of the disk to read, as used by DOS; for example, to specify the primary floppy drive, use `A:` as the drive to read, and use `B:` to specify the secondary floppy drive.

- To get a directory listing of the DOS disk currently in the primary floppy drive, type:

```
$ mdir a: RET
```

## 27.1.2 Copying Files to and from a DOS Disk

Use mcopy to copy files to and from a DOS disk.

To copy a file to a DOS disk, give as arguments the name of the source file to copy and the "drive letter" of the disk to copy it to.

- To copy the file `readme.txt` to the DOS disk in the primary floppy drive, type:

```
$ mcopy readme.txt a: RET
```

To copy a file from a DOS disk, give the "drive letter" of the disk to copy from, followed by the file name to copy, and no other arguments; mcopy will copy the specified file to the current directory.

- To copy the file `resume.doc` from the DOS disk in the secondary floppy drive to the current directory, type:

```
$ mcopy b:resume.doc RET
```

To copy all files from a DOS disk, just give the "drive letter" without any file names.

- To copy all of the files and directories from the DOS disk in the primary floppy drive to the current directory, type:

```
$ mcopy a: RET
```

## 27.1.3 Deleting Files on a DOS Disk

Use mdel to delete a file on a DOS disk. Give as an argument the name of the file to delete preceded by the "drive letter" of the disk to delete from.

- To delete the file `resume.doc` on the DOS disk in the primary floppy drive, type:

```
$ mdel a:resume.doc RET
```

## 27.1.4 Formatting a DOS Disk

To format a floppy disk for DOS, writing an empty MS-DOS filesystem to the disk in the process, use mformat. Give as an argument the name of the "drive letter" of the disk to format. (Remember, when you format a disk, any existing information contained on the disk is lost.)

- To format the floppy disk in the primary floppy drive so that it can be used with MS-DOS, type:

```
$ mformat a: RET
```

NOTE: If you want to use a floppy disk with your Linux system and don't need DOS compatibility, don't bother using this MS-DOS format—the native Linux format is much more efficient (see section Formatting a Floppy Disk). If you know how long a DOS format takes, you'll be amazed at how much faster the Linux format is, too—it will do it so fast you'll think it didn't work!

## 27.2 Using Macintosh Disks

```
@sf(Debian): 'hfsutils'
@sf(WWW): http://www.mars.org/home/rob/proj/hfs/
```

Apple Macintosh computers use a file system called the "Hierarchical File System," or HFS. The hfsutils package contains a set of tools to read and write disks in the HFS format.

The following recipes describe the use of the individual tools in this package.

- 27.2.1 Specifying the Macintosh Disk to Use
- 27.2.2 Listing the Contents of a Macintosh Disk
- 27.2.3 Copying Files to and from a Macintosh Disk
- 27.2.4 Deleting Files on a Macintosh Disk
- 27.2.5 Formatting a Macintosh Disk

Specifying which Mac disk to use.
Listing the contents of a Mac disk.
Copying files to and from Mac disks.
Deleting files on a Mac disk.
Formatting a Mac disk.

## 27.2.1 Specifying the Macintosh Disk to Use

To use a Macintosh disk with any of the `hfsutils` commands, you must first use hmount to specify the location of the HFS filesystem. Give as an argument the name of the Linux device file where the HFS filesystem exists; this virtually "mounts" the disk for use with the other `hfsutils` described in this section.

The device file for the first floppy drive is `/dev/fd0`, and for the second drive, `/dev/fd1`. Any valid device name, such as a SCSI device or Zip disk, may be given.

- To introduce the floppy disk in the first floppy drive as an HFS volume for the `hfsutils`, type:

```
$ hmount /dev/fd0 RET
```

After you run this command, the other tools in the hfsutils package will work on the Macintosh disk in the first floppy drive.

## 27.2.2 Listing the Contents of a Macintosh Disk

Use hls to get a directory listing of the Macintosh disk currently specified with hmount (see section Specifying the Macintosh Disk to Use).

- To get a directory listing of the currently specified Macintosh disk, type:
