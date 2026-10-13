
> The locate command works like grep on a database of your files. In some distributions, the slocate command is used for this purpose.

## grep

The grep command is a handy way to search through a file. As a system administrator, you may have long lists of users. If you want to search through your /etc/passwd file for a user named "michael jang," you could try the following command:

```
grep "michael jang" /etc/passwd
```

If the user named "michael jang" exists, you would see a line similar to the following:

```
mj:x:500:500:michael jang:/home/mj:/bin/bash
```

This preceding line tells you the home directory and default shell for that user. If the search string exists in more than one line, you’ll see those lines as well. You can even use grep to search through a series of files with commands like the following:

```
grep mj *
```

```
grep -c bash /etc/passwd
```

The first command looks for the string mj in all files in the current directory. The second command counts (-c) the number of lines that include the word bash.

> To use the asterisk (*) and other wildcards as search terms (rather than as wildcards), use a backslash. For example, if you wanted to search for asterisks in the /etc/passwd file, use the grep \* /etc/passwd command.

## Multiple Commands

It’s a common practice to use more than one Linux command in a line. For example, if you’re using the find command and you know that the result will have a large number of files, you can use a command like grep to search through the result. Specifically, let’s say you want to find your Netscape cache file. You might start with the following command:

```
find / -name netscape
```

However, you might get discouraged when you see hundreds of files flashing past you on your terminal screen. An alternative is to combine commands like this:

```
find / -name netscape | grep cache
```

This command searches through the results of the find command for the text string cache. Only those files with both strings are output to the screen. Other possible command combinations include the following:

- who | grep mj
- ps aux | grep netscape

The first command, who, lists all users currently logged on to your Linux system. When you pipe (|) the result to the grep mj command, you'll find the number of times that user mj is currently logged on to your system.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_180_0.png)

The letter w is also a bash command. Both w and who show users who are currently logged on.

The second command, ps, lists the processes currently running on your Linux system. The three switches, aux (a dash is not required for ps command switches), lead to a very long list of processes: all processes run by all users (a) each associated with the user name (u) independent of the virtual terminal (x). You need a tool like grep to search through these processes. This combined command returns all processes with the word netscape.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_180_1.png)

Commands like who and ps are discussed in detail in Chapter 11.

## MS-DOS File Tools

Linux includes tools that you can use to view an MS-DOS directory. Yes, you can use regular Linux commands such as ls and cd to review a mounted MS-DOS directory. But with MS-DOS tools, you don't have to mount the MS-DOS directory. Instead you can run familiar looking commands like the following:

```
mdir a:
mmove fig07-01.tif a:
mcopy a:rh1.txt
```

The first command lists the current files in your a: drive. The second command moves the fig07-01.tif file from your current directory to the a: drive. The third command copies the file rh1.txt from your a: drive to your current directory. These commands do not work if you've already mounted your floppy drive.

## Managing Multiple Files

There are two basic commands that are used as common Linux ways to manage multiple files: gzip and tar. For those of you familiar with Microsoft Windows-based "zip" utilities, these two commands break the zip process down into two parts. The tar command collects a series of files into an archive, and the gzip command compresses a file.

## Archiving by tar

The tar command is known as the tape archive command for historical reasons: Backups used to be primarily made to tape drives. Although tape drives are now less common, tar is the main Linux backup utility. It is designed to copy a series of files into a single large file. If you want to back up the files in your current directory, you might run the following command:

```
tar cvzf goodbackup.tar *
```

This command creates (c) a backup, listing every file name in the archive (v=verbose) in compressed format (z=zip) in the file (f) named goodbackup.tar. Files in subdirectories are also saved to this archive. You can then save this archived file to a backup area such as another volume or a tape drive.

> TIP
> When setting up an archive, it's good practice to save to a file with the .tar extension. Many Linux downloads are archived in .tar format.

You can just as easily unarchive files with the following command:

```
tar tkvzf goodbackup.tar
```

This command lists (t) the files in your archive. When it restores, it does not overwrite your current files (k=keep old files). In verbose (v) mode, you see everything that happens. If you stored files in a zipped format, you need to restore from the zipped (z) format. Finally, the command is restoring from the backup file (f) named goodbackup.tar. You can review some of the available tar switches in Table 8.8. Note that the first switch in the tar command should start with c, t, or x.

**Table 8.8 Command switches for tar.**

| Switch | Purpose |
|---|---|
| c | Create an archive |
| t | List files in a current archive |
| x | Extract files from an archive |
| d | Compare files between an archive and a current directory |
| f | Use the following file name for the archive |
| k | Do not overwrite existing files |
| v | Verbose option; list all files going in or coming out of an archive |
| r | Add files to the end of an archive |
| z | Zip; compress files to or from an archive |

There are a number of tar commands that you can use to create and extract archives. Some typical commands include the following. Read them over, referring to the descriptions in Table 8.8:

```
tar xvf download.tar
tar cvf backup.tar
```

## gzip and gunzip

You can compress a file with the gzip command. You can also further compress a tar file that's already been compressed with the z option. The syntax of this command is fairly simple:

```
gzip goodarchive.tar
```

The gzip command compresses the target file and adds a .gz extension to the end of the file name. The gunzip command reverses the process as follows:

```
gunzip goodarchive.tar.gz
```

> > **TIP**
> > When you download a new Linux program from the Internet, it often has a .tar.gz extension at the end of the file. You can use the gunzip and tar commands to extract the files that you need from this type of download.

## Disk Management Commands

There are two very similar disk management commands available in Linux: du and df. The directory usage (du) command lists the amount of space used by each file in and below your current directory. The free disk space (df) command lists

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_183_0.png)

Figure 8.2 Output from the du command.

the amount of space available on each hard disk volume. Figure 8.2 shows the output you get if you run the du command in a Linux user's home directory.

The number you see on the left is the size of the file, in kilobytes, which is the default from both the df and du commands. The applicable file is shown on the right. For example, you may see the following:

```
1941    ./gimp/tmp
```

The first dot (.) means that you start in your current directory. The slash (/) navigates to a subdirectory, in this case .gimp. In other words, this line means there are 1941 kilobytes of disk space dedicated to the .gimp/tmp subdirectory.

The df command shows how full each file system is on your computer. As you can see in Figure 8.3, the df command assesses each file system and displays the results in bytes. It includes any other file systems, such as your floppy or CD-ROM drives, that are currently mounted. The -m switch gives you results in megabytes, and the -k switch gives you results in kilobytes.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_183_1.png)

Figure 8.3 Output from the df command shows available disk space on each volume.
