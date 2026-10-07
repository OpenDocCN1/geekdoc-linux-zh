# CHAPTER 11 Backing Up, Restoring, and Recovery

The tar command is used to create, list, and compress the files in the directory named data_folder. The output is piped through the ssh command and sent to the remote computer named remote_host. On the remote computer, the stream is extracted and saved in the directory named mybackup_dir. You will be prompted for a password to send the stream.

# Copying Files Using cp

To copy files, we could use the cp command. The general format of the command when used for simple copying is

```
$ cp -a <source directory> <target directory>
```

+   - a argument is the same as giving -dpR, which would be
- -d—Dereference symbolic link; never follow symbolic links; copy the files they point to instead of copying links.
- -p—Preserve file attributes if possible. (File ownership might interfere).
- -R—Copy directories recursively.

The cp command can also be used to quickly replicate directories and retain permissions by using the -av command-line options. Using these options preserves file and directory permissions, gives verbose output, and recursively copies and re-creates subdirectories. A log of the backup can also be created by redirecting the standard output like this:

```
# cp -avR dir_to_backup destination_vol_or_dir 1 >/root/backup_log.txt
```

or

```
# cp -avR nhu8 /d2 1>/root/backup_log.txt
```

This example makes an exact copy of the directory named nhu8 on the volume named /d2, and saves a backup report named backup_log.txt under /root.

# Copying Files Using cpio

You can use cpio instead of tar to make backup file copies, but remember that cpio really works with lists of files. So first create the list and feed it to cpio.

```
# find <source directory> -print | cpio -pudv <target directory>
```

Here, use the command on the current directory with the -print option to generate a list of files in that directory. Pipe that file list to cpio. when cpio gets the file list, it

+   -p—Runs in copy-pass mode. (We are not creating an archive file here.)
- -u—Replaces all files without asking (unconditional).