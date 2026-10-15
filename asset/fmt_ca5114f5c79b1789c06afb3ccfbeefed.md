
# tar options destination source

The options are usually specified by a sequence of single letters, each specifying what tar should do. The device name of the backup device is `destination`, and `source` is a list of file or directory names denoting the files to back up.

## Backing up and restoring a single volume archive

Suppose you want to back up the contents of the `/etc/X11` directory on a single floppy disk. Log in as root, place a disk in the floppy drive, and then type the following command:

```
tar zcvf /dev/fd0 /etc/X11
```

The `tar` program displays a list of filenames as each file is copied to the compressed tar archive on the floppy disk. In this case, the options are `zcvf`, the destination is `/dev/fd0` (the floppy disk), and the source is the `/etc/X11` directory (which implies all its subdirectories and their contents). You can use a similar `tar` command to back up files to a tape. Simply replace `/dev/fd0` with the tape device — such as `/dev/st0` for a SCSI tape drive.

A few common tar options are defined here:

| Option | Definition |
|---|---|
| z | compresses the tar archive using gzip |
| c | creates a new archive |
| v | displays verbose messages |
| x | extracts files from the archive |
| t | lists the contents of the archive |
| M | specifies a multi-volume archive (next section describes multi-volume archives) |
| f | specifies the name of the archive file or device on the next field in the command line |

To view the contents of the tar archive you create on the floppy disk, type the following command:

```
tar ztf /dev/fd0
```

You should see a list of the filenames (each begins with `/etc/X11`) indicating the contents of the backup. In this tar command, the `t` option lists the contents of the tar archive.

To learn how to extract the files from a tar backup, try the following steps while logged in as root:
- 1. Change the directory to `/tmp` by typing the command:
  ```
  cd /tmp
  ```
  That is where you extract the files from the tar backup.
- 2. Type the following command:
  ```
  tar zxvf /dev/fd0
  ```
  This `tar` command uses the `x` option to extract the files from the archive stored on `/dev/fd0` (the floppy disk).

If you check the contents of the `/tmp` directory, you notice that the `tar` command creates an `etc/X11` directory tree in `/tmp` and restores all the files from the tar archive into that directory. The `tar` command strips off the leading `/` from the filenames in the archive and restores the files in the current directory. If you want to restore the `/etc/X11` directory from the archive on the floppy, use the following command:

```
tar zxvf /dev/fd0 /
```

The `/` at the end of the command denotes the directory where you want to restore the backup files.

As you can see, the `tar` command enables you to create, view, and restore an archive. You can store the archive in a file or in any device that you specify with a device name.

## Backing up and restoring a multivolume archive

Sometimes the capacity of a single storage medium is less than the total storage space needed to store the archive. In that case, you can use the `M` option for a multivolume archive — meaning that the archive can span multiple tapes or floppies.

> You cannot create a compressed, multivolume archive. That means you cannot use the `z` option.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_324_0.png)

To see how multivolume archives work, log in as root, place one disk in the floppy drive, and type the following tar command:

```
tar cvfM /dev/fd0 /usr/doc/ghostscript*
```

Note the `M` option in the option letters, which tells `tar` to create a multivolume archive. The `tar` command prompts you for a second floppy when the first one fills to capacity. Take out the first floppy and insert another floppy when you see the following prompt:

```
Prepare volume #2 for `/dev/fd0` and hit return:
```
