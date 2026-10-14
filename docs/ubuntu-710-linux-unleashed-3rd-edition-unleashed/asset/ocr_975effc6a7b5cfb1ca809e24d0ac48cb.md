# Restoring Files from an Archive with `tar`

The x option in tar will restore the files from a backup and preserve the file attributes as well, and tar will create any subdirectories it needs. Be careful when using this option because the backups might have been created with either relative or absolute paths. You should use the tvf option with tar to list the files in the archive before extracting them so that you will know where they will be placed.

For example, to restore a tar archive compressed with bzip2,

```
sudo tar xjvf ubuntutest.tar.bz2
```

To list the contents of a tar archive compressed with bzip2,

```
sudo tar tjvf ubuntutest.tar.bz2
-rw-rw-r-- paul/paul        0 2003-09-04 18:15:05 ubuntutest/
-rw-rw-r-- paul/paul      163 2003-09-03 22:30:49 ubuntutest/README
-rw-rw-r-- paul/paul      840 2003-09-01 19:27:59 ubuntutest/ubuntu_screenshot.txt
-rw-rw-r-- paul/paul     1485 2003-09-01 18:14:23 ubuntutest/style-sheet.txt
-rw-rw-r-- paul/paul      931 2003-09-01 19:02:00 ubuntutest/ubuntu_TOC.txt
```

Note that because the pathnames do not start with a backslash, they are relative pathnames and will install in your current working directory. If they were absolute pathnames, they would install exactly where the paths state.

# NOTE

The tar command can back up to a raw device (one with no file system) as well as a formatted partition. For example,

```
sudo tar czvf /dev/hdd /boot /etc /home
```

backs up those directories to device /dev/hdd (not /dev/hda1, but to the unformatted device itself).

The tar command can also back up over multiple floppy disks:

```
sudo tar czMf /dev/fd0 /home
```

will back up the contents of /home and spread the file out over multiple floppies, prompting you with this message:

```
Prepare volume #2 for `/dev/fd0' and hit return:
```