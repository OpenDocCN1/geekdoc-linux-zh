# 8.6.2 tar

Once you get up to a certain size, backing files up into a Linux filesystem starts to become unwieldy. What you really need then is to be able to write whole directories with all their subdirectories and files straight out to a tape drive. One of the commands that can perform this operation is called tar (i.e. Tape ARchiver).

What this command does effectively, is to pack all the files in the directories it is given into a single huge file, called a tarfile, which can then be written to tape.

So far, tar would seem to be of limited use as so few systems support a tape drive of any kind. However, tar is capable of writing its output file to anywhere including: onto floppy disk, out to the screen or even into an ordinary file. In addition to this, tar also has a couple of other tricks it can perform. If the tarfile is being written to floppy but it is too large to fit onto a single disk, then tar can be instructed to split the file over multiple disks (called a multi-volume archive). It is also possible to instruct tar to use the gzip algorithm to compress the tarfile before writing the result to its output.

The general format of the tar command is:

```
tar [options] files
```

where files is the list of files and directories whose contents will be included in or extracted from the archive.

The tar command has many options, the most useful are:

+   -c create a new tarfile archive;
-x extract files from a tarfile archive;
-t display the contents of a tarfile archive;
-f file specify tarfile name as file;
-v get tar to be verbose about what it is doing;
-l stay in local filesystem, don't cross mount points;
-M create/extract/display a multi-volume archive;
-N date only store files newer than date;
-z use gzip to compress/uncompress archive.

By convention, a tar archive filename should be given the suffix .tar and a compressed archive filename should have the suffix .tgz (as all the packages probably had on your Linux distribution disks).

A typical tar command to create a compressed archive containing the home directory contents for user rachel would be:

```
# tar -cvzf /tmp/rachel.tgz /home/rachel
```

A command to examine the contents of this archive would be:

```
# tar -tzf /tmp/rachel.tgz
```

And a command sequence to restore user rachel's home directory from the archive after some of the original files were accidentally deleted: