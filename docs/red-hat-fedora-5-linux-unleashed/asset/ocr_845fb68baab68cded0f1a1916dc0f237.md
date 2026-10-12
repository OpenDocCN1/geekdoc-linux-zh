# NOTE

> The software in a backup system must support the hardware, and this relationship can determine which hardware or software choices you make. Many sysadmins choose a particular backup software not because they prefer it to other options, but because it supports the hardware they own.
> 
> The price seems right for free backup tools, but consider the software's ease of use and automation when assessing costs. If you must spend several hours implementing, debugging, documenting, and otherwise dealing with overly elaborate automation scripts, the real costs go up.

# tar: The Most Basic Backup Tool

The tar tool, the bewhiskered old man of archiving utilities, is installed by default. It is an excellent tool for saving entire directories full of files. For example, here is the command used to back up the /etc directory:

```
# tar cvf etc.tar /etc
```

Here, the options use tar to create an archive, be verbose in the message output, and use the filename etc.tar as the archive name for the contents of the directory /etc.

Alternatively, if the output of tar is sent to the standard output and redirected to a file, the command appears as follows:

```
# tar cv /etc > etc.tar
```

and the result is the same.

All files in the /etc directory will be saved to a file named etc.tar. With an impressive array of options (see the man page), tar is quite flexible and powerful in combination with shell scripts. With the -z option, it can even create and restore gzip compressed archives while the -j option works with bzip2ed files.

# Creating Full and Incremental Backups with tar

If you want to create a full backup,

```
# tar cjvf fullbackup.tar.bz2 /
```

creates a bzip2-compressed tarball (the j option) of the entire system.

To perform an incremental backup, you must locate all the files that have been changed since the last backup. For simplicity, assume that you do incremental backups on a daily basis. To locate the files, use the find command:

```
# find / -newer name_of_last_backup_file ! -a -type f -print
```

When run alone, find will generate a list of files systemwide and print it to the screen. The ! -a -type eliminates everything but regular files from the list; otherwise, the entire directory would be sent to tar even if the contents were not all changed.