
## Using Linux Backup Utilities

When working with Linux, you have a host of different utilities at your disposal to conduct a backup. Many come with the operating system; others can be obtained from third parties. For your LPIC II CompTIA Linux+ exam, you need to be familiar with the tools that are common to most distributions and are run from the shell prompt. In this part of the chapter, we're going to look at the following:

- Using tar
- Using cpio
- Using dd to copy data

Let's begin by looking at the venerable tar utility.

## Using tar

The tar utility has been around for a very long time and is a very commonly used Linux backup tool. The acronym "tar" stands for tape archive. The tar utility takes a list of specified files and copies them into a single archive file (.tar). The .tar file can then be compressed with the gzip utility on your Linux system, resulting in a file with a .tar.gz extension. This is called a tarball.

The tar utility can be used to send backup jobs to a variety of backup media, including tape drives and removable hard disk drives. The syntax for using tar to create backups is `tar -cf filename directory`. The `-c` option tells tar to create a new archive. The `-v` option tells tar to work in verbose mode, displaying each file being backed up on screen. The `-f` option specifies the name of the tar archive to be created.

For example, if you wanted to create a backup of the /home directory named backup.tar on an external USB hard drive mounted in /media/usb, you would enter `tar -cf /media/usb/backup.tar /home`, as shown in this example:

```bash
wsl:/ # tar -cvf /media/usb/backup.tar /home
tar: Removing leading '/' from member names
/home/
/home/tux/
/home/tux/.gftp
/home/tux/.gftp/gftp.log
/home/tux/.gftp/bookmarks
/home/tux/.gftp/gftp.rsc
/home/tux/.nautilus/
/home/tux/.local/
/home/tux/.local/share/
... 
```

Notice in this example that a message stating `tar: Removing leading '/' from member names` is displayed. When a tar archive is created, absolute paths are converted to relative paths by default. As a result, the leading `/` is removed.

You can use the options shown in Table 10-2 with tar.

| Option | Function |
| :--- | :--- |
| -A | Appends tar files to an existing archive. |
| --concatenate | |
| -C | Creates a new archive file. |
| --create | |
| -d | Identifies differences between an archive file and files in the file system. |
| --compare | |
| -P | Causes tar to not strip leading / from filenames. |
| --absolute-names | |
| -r | Adds files to the end of a tar archive. |
| --append | |
| -t | Lists the contents of an archive file. |
| --list | |
| -u | Append files only if they are newer than the existing files in an archive. |
| --update | |
| -x | Extracts files from an archive. |
| --extract | |
| -z | Does one of two things. During archive creation, it compresses the new tar archive by running it through the gzip utility. During extraction, it first decompresses the tar archive using the gunzip utility. |
| --gzip | |
| --gunzip | |
| -j | Does one of two things. During archive creation, it compresses the new tar archive by running it through the bzip2 utility. During extraction, it first decompresses the tar archive using the bzip2 utility. |
| --bzip2 | |
| -X filename | Causes tar to exclude files listed in the text file specified. |
| --exclude-from | |

**Table 10-2 tar Command Options**

> **NOTE** You can also compress/decompress tar archives (or any other files, for that matter) directly from the shell prompt using the gzip and gunzip utilities or the bzip2 and bunzip2 utilities. Archive files compressed with bzip2 instead of gzip will usually have an extension of .bz2 instead of .gz.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_433_0.png)

If you wanted to back up to a tape drive instead of a USB drive, you could do this by replacing the filename parameter in the tar command to the device name for your tape drive. On most distributions, the first SCSI tape drive in the system is referenced through /dev/st0. Therefore, you could enter `tar -cvf /dev/st0 /home` if you wanted to run the same backup as in the previous example, but send it to a SCSI tape drive instead.

To restore a tar archive, simply enter `tar -xvf filename`. For example, to extract the archive we just created, you would enter `tar -xvf /media/usb/backup.tar`. This will extract the archive into the current working directory. If the archive has been zipped, you can also use the `-z` option to unzip the archive before extracting it.

In addition to tar, you can also use cpio to create backups. Let's discuss how it is used next.

## Using cpio

The cpio utility can also be used to make archive files just like tar. A key difference between tar and cpio is the fact that you must provide cpio with a list of files and directories to back up from the standard input. This can be done using cat to display the contents of a file or by generating a listing using find or ls.

For example, let’s suppose you wanted to back up the contents of the /home/tux/myproject directory on your Linux system. To use cpio to do this, you must somehow generate a listing of files and directories in this directory and send it to cpio. Then you must redirect the output from cpio to a file. This can be done using the find utility, discussed earlier. You could switch to /home/tux/myproject and then enter `find -print -depth | cpio -ov > /media/usb/backup.cpio`. The find utility will generate a listing of all files in the current directory. Because the `-print` option was used, find will print the full name of each file to the screen (the standard output). Because the `-depth` option was also used, find checks the contents of each directory before processing the directory itself.

> **TIP** If there are no subdirectories in the MyProjects directory, an easier way to do this would be to enter `ls | cpio -ov > /media/usb/backup.cpio`.

The key here is the fact that we’ve piped the standard output from find to the standard input of cpio. The cpio utility uses this as a list of files and directories to archive. The `-o` option tells cpio to create a new archive. The `-v` option simply tells cpio to run verbosely, displaying the name of each file and directory as it’s processed. Finally, we have to redirect the standard output from cpio (the archive) to a file in the file system. This is done by entering `>` followed by the name of the archive file.

You can also compress a cpio archive by adding the gzip utility to the pipe. For example: `ls | cpio -ov | gzip > /media/usb/backup.cpio.gz`.

To restore files from a cpio archive, you run cpio from the shell prompt using the `-i` option and specifying the name of the archive to process. When you do this, the archive files will be extracted into the current working directory. For example, we could extract the archive we just created by entering `cpio -iv < /media/usb/backup.cpio`, like this:

```bash
ws1:/tmp # cpio -iv < /media/usb/backup.cpio
acpidump
accessdb
acpirc

341 blocks
ws1:/tmp #
```

If the cpio archive was compressed with gzip, you will have to run it through the gunzip command to decompress the archive before you can extract files from it with cpio. This is shown here:

```bash
ws1:/media/usb # ls
backup.cpio.gz  backup.cpio.tar
```

```bash
ws1:/media/usb # gunzip backup.cpio.gz
ws1:/media/usb # ls
backup.cpio  backup.tar
ws1:/media/usb
```

As you can see, the backup.cpio.gz file is decompressed by the gunzip command into the backup.cpio file, which can now be manipulated with the cpio command. Another way to do this is to add the `-c` option to the gunzip command and then pipe the results to `cpio -i`. The `-c` option tells gunzip to write the output of the command to the standard output, leaving the original file intact. Essentially, this just writes the uncompressed filename to the standard out, which is then sent to cpio for processing. Here is an example:

```bash
ws1:/media/usb # ls
backup.cpio.gz  backup.tar
ws1:/media/usb # gunzip -c backup.cpio.gz | cpio -i
341 blocks
ws1:/media/usb # ls
accesdb  acpidump  acpiscr  backup.cpio.gz  backup.tar
ws1:/media/usb #
```

As you can see, the gunzip command extracted the name of the file compressed in the gzip archive and sent it to the `cpio -i` command, which then extracted the three files out of the archive to the local directory.

Before we end this Chapter, we need to look at the dd utility. Let’s do that next.

## Using dd to Copy Data

You can use the dd command to convert and copy files. You can copy all kinds of Linux data with this command, including entire partitions. You may be thinking, “Big deal, I already know how to use cp and mv.” Actually, the dd utility is quite useful. The key difference between dd and other file copy utilities is the fact that it copies data using records. The default size for a record is 512 bytes.

Let’s first look at how you copy a file with dd. The syntax is `dd if=input_file of=output_file`. Use the `if=` (input file) option to specify the file to copy. Use the `of=` (output file) option to specify the name of the new file. Here is an example:

```bash
ws1:/ # dd if=/home/tux/MyProject/acpidump of=/home/tux/acpidump.copy
29+1 records in
29+1 records out
15112 bytes (15 kB) copied, 0.000263333 s, 57.4 MB/s
ws1:/ #
```

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_435_0.png)

> **NOTE** You can modify the default record size using the `bs=block_size` option.

One of the cool things about dd is the fact that, because it uses records, it can copy an entire partition to a single file. This is powerful. Essentially, dd is a simple command-line tool that you can use to implement a form of drive imaging. I have a friend (who is Mr. Uber Linux Admin) and he uses dd in scripts to create his own imaging application. Cool stuff!
