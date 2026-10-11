
## Backup Strategies

- What media should I use? (CDR/W, tape, HD, and so on)
- When should I back up? (During a slow or down time, if any)

There are various methods to backing up data. You need to understand that, if a system has just been installed, every file on the system has an archive attribute set to on, or changed. This is important for when you want to do anything other than a full backup of a system. After a full backup, all the files should have the archive bit set to off; thus, any incremental backups from that point will take only new or changed files.

The differences between the backup options are important. The following list lays out the possibilities and what they do to the archive attribute:

- **Copy**—Copies files, effectively backing them up. No archive bits are reset.
- **Full**—Backs up all the files on the system. The archive bit is reset for all files.
- **Incremental**—Backs up every file that has an archive bit set (setting each bit to off). Essentially, this is a differential of new or changed files since the last full or incremental backup.
- **Differential**—Backs up all the files with the archive bit set since the last full or incremental, but it doesn’t change the archive bit state.

Each of the backup commands handles these types of backup operations differently, and this is beyond the scope of this discussion.

![](img/49f4f38f3aec011238fa50f89e643db3_366_0.png)

Expect to be questioned about the following scenario: A full backup is done on a Friday or at month end; then a series of differential backups, a series of incremental backups, or a combination of the two is performed; and then a crash occurs. You’ll need to parse the questions to find out how many tapes are required of which variety to restore the system to its state at the time of the last backup.

## Backup Commands

A number of backup options are available for Linux systems. Some are more useful than others, and some act on files, whereas others work best on partitions or disks as a unit.

Backup commands on the exams include the following:

- cpio
- tar
- compress and uncompress
- gzip and gunzip
- bzip2 and bunzip2

### Using cpio

> The **cpio** command appears extensively in the Level 2 LP1 objectives. This level of the exam might ask you about the **cpio** command at only the simplest levels, such as knowing that it exists, how it works in general terms, and whether it can be used to back up a Linux system.

The **cpio** command actions all treat the file system as the home base. If you are copying out, it's from the file system out to another file. The same is true with copying in—it's from a file into the file system.

The **cpio** command has three options for acting on files and file systems:

- -o or --create—This copies files to an archive using a list of files typically created by the find command.
- -i or --extract—This copies files into the file system from an archive or a list of the archive contents.
- -p or --pass-through—This copies files from one directory tree to another without the use of an archive, essentially performing the same function as the cp -r command.

The **cpio** command accepts a list of files in a one-file-per-line format and uses this list to send the archived files to either the standard output or an archive file you specify.

**cpio** supports a variety of archive formats, including binary, ASCII, crc, and tar, to name the most relevant.

An example of creating a **cpio** archive from the files in the current directory is shown here:

```bash
find . "*" | cpio -o > archive.cpio
```

This outputs the list of files found by this particular find command, with the **cpio** command taking the entirety of the files and sending them to the archive.cpio file by redirecting standard output to the file.

The `cpio` command doesn't gather files to be archived by itself, so be aware that using either `find` or `ls` command is necessary to feed `cpio` a list of filenames. For example, if you needed to archive all the files that have an extension of .txt in the current directory to a `cpio` archive named txt.cpio, you would use the following command:

```bash
find . -name "*.txt" | cpio -o > txt.cpio
```

### Using tar

The tar command is relatively complex, too. It's used by default to take a grouping of files and create a single container .tar file that holds the individual files. Although it's conventional wisdom that tar doesn't compress the contents, this is not true because some compression is involved.

The tar command also can utilize or snap in various archive commands, particularly the `gzip/gunzip` and `bzip2/bunzip2` commands by the use of special option characters. This has the effect of creating a compressed archive file, typically named .tar.gz for gzip-compressed files and .tar.bz2 for bzip2-compressed files.

As Figure 13.1 shows, the tar command has three main methods that act on files or tar archives. You can remember all the possible first letters with the acronym actdux. Also, any tar command must start with one of those letters.

A more explanatory list of the options is shown here:

- `a`—Appends tar files to an archive
- `c`—Creates an archive
- `d`—Compares an archive and a file system and reports the differences
- `r`—Appends files to the end of an archive
- `t`—Lists the contents of an archive
- `u`—Updates an archive with changed or new files
- `x`—Expands or unarchives the archive

Although the previously listed options can be used with tar, reality is more limited. Figure 13.1 explains the method that most tar commands follow.

![](img/49f4f38f3aec011238fa50f89e643db3_368_0.png)

**Figure 13.1** The tar command's methods.

As you can see, most tar commands create, list, or expand an archive, with the addition of the verbose option to see the full `ls -l` style output of each file. If you need to compress or uncompress an archive, the `-z` option for `gzip/gunzip` and the `-j` option for `bzip2/bunzip2` are useful. Or, it can be left out entirely when working with `.tar` files. Finally, you must specify the `-f` (for filename) option so tar knows to which file you are referring (remember that everything on a Linux system can be referred to as a file). The target is any file or path.

### Creating tar Archives

When you're creating an archive with tar, you should think about what you want to archive, where you want the resulting archive to be created, and what compression if any you want to use.

To create a simple tar archive, the options you need are as follows:

```bash
tar -cf archive.tar /tarfoo
```

In this example, the `-c` option signals tar to create the file specified after the `-f` option, specifies the name of the file that will be created, and specifies the directory you are compressing. tar can compress just about anything that's a file, and everything is a file.

To create the same archive with `gzip` compression, you simply insert a `-z` option and use the letters `.gz` as the filename suffix:

```bash
tar -czf archive.tar.gz /tarfoo
```

This creates a compressed archive file that uses the `gzip` compression algorithms. If you want slightly higher compression, use the `-j` option (instead of the `-z` option) for `bzip2` compression.

![](img/49f4f38f3aec011238fa50f89e643db3_369_0.png)

> You will likely see questions on the exam that test your knowledge of which compression command has the highest compression. For example, using `bzip2` results in a smaller archive file.

To create a tar archive and see a long style listing that includes ownership and permission information, use the `-v` option:

```bash
tar -cvf archive.tar /tarfoo
```

This produces the following output:

```
tar: Removing leading "/" from member names
tarfoo/
tarfoo/install.log
```

As you can see, creating a `tar` file from a directory causes the `tar` command to strip the leading `/` from the full path of the objects in the archive.

If you were in the same directory as the entry for the `tarfoo` directory (the root of the system) and issued the command again, you’d see a slightly different set of messages:

```bash
tar -cvf /root/archive.tar tarfoo
```

This produces the output shown here:

```
tarfoo/
tarfoo/install.log
tarfoo/install.log.syslog
tarfoo/.bash_logout
```

Notice that the `tar: Removing leading ‘/’ from member names` message is gone because you’re not using absolute pathnames for the archive.

### Taking Pity on the Unarchiver

It’s considered proper and elegant to create `tar` archives by specifying a directory that contains the files to be archived, not just a bunch of files that are in the current directory.

For example, creating an archive of the `/etc` directory contents with the following command causes the archive to place the file in `/etc` into a folder in the archive named `etc` and then the files:

```bash
tar -cf etc.tar /etc
```

When you unarchive the `tar` file, by default it creates an `etc` directory in the current directory, which contains the entirety of the `/etc` directory you archived.

Contrast this with the nightmare that happens when you navigate to the `/etc` directory and create the archive from there with this command:

```bash
tar -cf /root/badetc.tar *
```

This archive file contains the same files as the previous one, except they aren’t contained in a top-level `etc` directory—everything is in the top level of the archive.

Imagine what will happen to your system when you unarchive this file in the root user’s home directory. You will have spewed approximately 2,400 files directly into the root user’s home directory!
