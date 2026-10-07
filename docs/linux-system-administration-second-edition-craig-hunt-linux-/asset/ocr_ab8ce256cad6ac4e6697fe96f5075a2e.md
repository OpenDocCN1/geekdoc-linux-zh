```
# tar cfp - . | (cd /destination-dir; tar xvpf -)
```

The result of the preceding two commands is a duplication of the contents of /source-dir in /destination-dir, including ownership, permissions, symbolic links, and so on. This command can be very useful if you want to back up to a backup hard disk. If your system goes down, you can swap in the backup hard disk, boot with an emergency boot floppy, and be running the backup system in a matter of minutes.

Keep in mind that different versions of tar behave differently. GNU tar strips the “/” off of the path by default, resulting in a tarball with a relative path instead of an absolute one. Some versions do not, however, so you must be careful to not accidentally write to the wrong location.

# Archiving to Another Computer Remotely

To write the archive to a file on another computer, you simply precede the archive name with the name of the computer followed by a colon. This option, like the remote dump access described earlier, uses the rshd or in.rshd daemon on the destination system, so you can access a remote tape drive directly. Thus the archival commands would be something like:

```
# tar cvzf remote:/dev/st0 /usr/local/bin
# tar xzvrf remote:/dev/st0
```

# Archiving to a Floppy Disk

Yes, Virginia, it is possible to back up your system to floppy disks, but it will be painful. Each floppy disk will hold 1.44MB of data. This technique is most useful for copying individual files from one system to another using floppies, or copying files between Linux and other Unix systems that don’t share common filesystems. By writing a tarball directly to floppy, you bypass the need for a filesystem. Assume that you have a file /tmp/biggraphic.gif, with a size of 1.88MB. Obviously this won’t fit on a standard 3.5" floppy. You can use the tar command with the -M option as follows:

```
# tar -cvMf /dev/fd0 /tmp/biggraphic.gif
```

When the backup image reaches the floppy’s capacity, you will be prompted for a new floppy:

```
Prepare volume #2 for /dev/fd0 and hit return:
```

Put the second floppy in the drive and press the Enter key, and tar will continue the backup process. Each time the floppy capacity is exceeded, you will get this same prompt with an appropriate volume number.

To extract the file from the floppies, put the first volume in the drive and use the following command:

```
# tar -xvMf /dev/fd0
```

You will be prompted to put in the subsequent floppies, as you were when the archive was written. Unfortunately, the tar command won’t allow you to compress a multi-volume backup. If you attempt to do so, you will get the following error:

```
tar: Cannot use multi-volume compressed archives
tar: Error is not recoverable: exiting now
```

Although tar will write to standard output with the -O argument, it will not read a file list from standard input, unlike many other archiving utilities. Many consider this to be a major disadvantage.