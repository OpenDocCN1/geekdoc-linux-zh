
## Using dump

The dump tool is a command-line utility. It takes many parameters, but the most relevant are as shown in Table 23-2.

For example, here is the command to perform a level 0 dump to /dev/st0 of the /dev/rdal file system:

```bash
[root@lord /root]# dump -0 -t /dev/st0 /dev/rdal
```

### Suppressing the Tape Size Calculation

The dump tool requires that it know the size of the tape in units of bits per inch and feet per tape. It uses this information to provide multi-volume backups so that it can prompt the operator to insert the next tape when it is ready. But if you don't know the size of your tape in bits per inch and its length in feet, you may still know the dump will fit on the tape. (For example, you may know that the partition you are dumping is 2 GB and the tape capacity is 5 GB uncompressed.) In this situation, you can do a little trick to keep dump from calculating the tape size. Instead of dumping straight to the device, send the output to the standard output and then use the `cat` program to redirect the dump to the tape. Using the example in the previous section, you would enter this command:

```bash
[root@ford /root]# dump -0 -f - /dev/hda1 | cat > /dev/st0
```

Since you're sending the output to standard out, you can also use this opportunity to apply your own compression filters to the stream instead of relying on hardware compression. For example, to use `gzip` to compress your dump, you'd type:

```bash
[root@ford /root]# dump -0 -f - /dev/hda1 | gzip --fast -c > /dev/st0
```

> **WARNING:** It's considered dangerous to dump file systems that are being actively used. The only way to be 100% sure that a file system is not in use is by unmounting it first. Unfortunately, very few people can afford the luxury of unmounting a system for the time necessary to do backup. The next best thing is to do the thruxly unappealing task of verifying backups on a regular basis. Verification is best done by *listing* to see if the `restore` program (discussed later) can completely read the tape and extract files from it. It's tedious and it isn't fun. But many a systems administrator has lost a job over bad backups—not to one of them.

| Parameters for the dump Command | Description |
|---|---|
| -n | The dump level, where n is a number between 0 and 9. |
| -b blocksize | Sets the dump block size to blocksize, which is measured in kilobytes. If you are backing up many large files, using a larger block size will increase performance. |
| -B count | Specifies a number (count) of records per tape to be dumped. If there is more data to dump than there is tape space, dump will prompt you to insert a new tape. |
| -f filename | Specifies a location (filename) for the resulting dumpfile. You can make the dumpfile a normal file that resides on another file system, or you can write the dumpfile to the tape device. The SCSI tape device is /dev/st0. |
| -u | Update the /etc/dumpdates file after a successful dump. |
| -d density | The density of the tape in bits per inch. |
| -B size | The size of the tape in feet. |

*Table 23-2. Parameters for the dump Command*

## Using dump to Back Up an Entire System

The dump utility works by making an archive of one file system. If your entire system comprises multiple file systems, you need to run `dump` for each file system. Since `dump` creates its output as a single large file, you can store multiple dumps to a single tape by using a non-rewinding tape device.

Assume we're backing up to a SCSI tape device, `/dev/st0`, we must first decide which file systems we're backing up. This information can be in the file *fstab*. Obviously, we don't want to back up files such as */dev/srdisk*, so we skip those. Depending on our data, we may or may not want to back up certain partitions (such as **swap** and **/tmp**). Let's assume this leaves us with **/dev/hda1**, **/dev/hda3**, **/dev/hda4**, and **/dev/hda6**. To back these up to **/dev/st0**, compressing them along the way, we would issue the following series of commands:

```bash
[root@ford /root]# mt -f /dev/st0 rewind
[root@ford /root]# dump -0uf - /dev/hda1 | gzip --fast -c > /dev/st0
[root@ford /root]# dump -0uf - /dev/hda3 | gzip --fast -c > /dev/st0
[root@ford /root]# dump -0uf - /dev/hda5 | gzip --fast -c > /dev/st0
[root@ford /root]# mt -f /dev/st0 rewind
[root@ford /root]# mt -f /dev/st0 eject
```

The first `mt` command is to make sure the tape is completely rewound and ready to accept data. Then come all the `dump` commands run on the partitions, with their outputs piped through `gzip` before going to the tape. To make the backups go a little faster, the --fast option is used with `gzip`. This results in compression that isn't as good as normal `gzip` compression, but it's much faster and takes less CPU time. The -c option on `gzip` tells it to send its output to the standard out. We then rewind the tape and eject it.

## Using restore

The `restore` program reads the dumpfiles created by `dump` and extracts individual files and directories from them. Although `restore` is a command-line tool, it does offer a more intuitive interactive mode that lets you go through your directory structure from the tape. Table 23-3 shows the command-line options for the `restore` utility:

### A Typical Restore

A typical invocation of `restore` is as follows:

```bash
[root@fdoroot]# restore -iv /dev/st0
```

which will pull the dump file from the device */dev/st0* (the first SCSI tape device), print out each step `restore` takes, and then provide an interactive session for you to decide which files from the dump get restored.

| Options for the restore utility | Description |
|---|---|
| -i | Enables interactive mode for *restore*. The utility will read the directory contents of the tape and then give you a shell-like interface in which you can move directories around and tag files you want to recover. When you’ve tagged all the files you want, *restore* will go through the dump and restore those files. This mode is handy for recovering individual files, especially if you aren’t sure which directory they’re in. |
| -r | Rebuilds a file system. In the event you lose everything in a file system (a disk failure, for instance), you can simply recreate an empty file system and *restore* all the files and directories of the dump. |
| -b blocksize | Set the dump’s block size to *blocksize* kilobytes. If you don’t supply this information, *restore* will figure this out for you. |
| -t filename | Read the dump from the file *filename*. |
| -t directory | Specify the temporary workspace (*directory*) for the restore. The default is /tmp. |
| -v | The verbose option; it shows you each step *restore* is taking. |
| -y | In the event of an error, automatically retry instead of asking the user if he wants to retry. |

*Table 23-3. Command-Line Options for the restore Utility*

### A Complete Restore

Should a complete file system be lost, you can re-create the file system using the `mke2fs` command and then `restore` to populate the file system. For example, let's say our external SCSI drive (`/dev/sda`), which has a single partition on it (`/dev/sda1`), fails. After replacing it with a new drive, we would re-create the file system like so:

```bash
[root@ford /root]# mke2fs /dev/sda1
```

Next, we have to mount the partition in the appropriate location. We'll assume this is the `/home` partition, so we type the following:

```bash
[root@ford /root]# mount /dev/sda1 /home
```

Finally, with the dump tape in the SCSI tape drive (`/dev/st0`), we perform the restore using the commands:

```bash
[root@ford /root]# cd /home; restore -rf /dev/st0
```

> **TIP:** If you used `gzip` to compress your dump, you'll need to decompress it before `restore` can do anything with it. Simply let `gzip` decompress the tape device and send its output to the standard out. Standard out should then be piped to `restore`, with the `-f` parameter set to read from standard in. Here's the command:

```bash
[root@ford /root]# gzip -d -c /dev/st0 | restore -ivf -
```

## tar

In Chapter 6 we discussed the use of **tar** for creating archives of files. What we didn't discuss is the fact that **tar** was originally meant to create archives of files onto tape (**tar** = tape archive). Because of Linux's flexible approach of treating devices the same as files, we've been using **tar** as a means to archive and unpack a group of files into a single disk file. Those same **tar** commands could be rewritten to send the files to tape instead.

The **tar** command can archive a subset of files much more easily than `dump` can. The `dump` utility works only with complete file systems, but **tar** can work on mere directories. Does this mean **tar** is better than `dump` for backups? Well, sometimes ... Overall, `dump` turns out to be much more efficient than **tar** when backing up entire file systems. Furthermore, `dump` stores more information about the file, requiring a little more tape space but making recovery of that file easier. On the other hand, **tar** is truly cross-platform—and **tar** files created under Linux can be read by the **tar** command under any other UNIX. And `gzipped` **tar** files can even be read by the WinZip program! Whether you're better off with **tar** or `dump` depends on your environment and needs.
