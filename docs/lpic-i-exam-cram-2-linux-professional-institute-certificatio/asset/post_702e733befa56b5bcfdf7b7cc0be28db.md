
It really does matter where you are and which path options you use when you create or expand an archive file. It’s best practice to use absolute pathnames and make sure that **tar** removes the leading / from the path when it’s created.

To solve the problem of 2,400 files polluting your root user’s home directory, use the following command, where **badetc.tar** is the offending archive file:

```
tar -tf badetc.tar | xargs rm -rf
```

This command produces a list of the paths and filenames of files in the archive and uses the **xargs** command to feed each line of output as a filename specification to the **rm -rf** command, removing all the files and directories that were expanded from the **badetc.tar** file.

## Useful Creation Options

A number of other options can be used for creating tar archives. Here is a list of the more useful and testable ones:

- -b—Sets the block size to fit the media to which you are archiving. This is necessary for some tape devices.
- -M—This specifies multiple archive targets or spreads a large archive across multiple tapes or media.
- -g—Creates a new format incremental backup (only those that have changed since the last full or incremental).
- -1—Stays on the local file system; it’s used to keep from backing up the entire NFS network by accident.
- -L—This is followed by a number that reflects 1024 bytes, so -L 500 equals 500KB. (It’s used for setting the tape length so multiple tapes can be used for an archive.)
- --remove-files—This is very dangerous because the specified files are removed from the file system after they have been added to the archive!

## Listing Archive Files

Arguably the Rodney Dangerfield of the tar options, listing is something that typically is used after you don’t get the results you wanted or realize what you’ve just done and want to confirm how hard it is going to be to clean up.

To list the contents of a tar archive, use the following command:

```
tar -tf archive.tar
```

This produces the output shown here:

```
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

To list an archive that uses compression, simply insert the necessary letter between the -t and the -f options, such as the bzip2 j option shown here:

```
tar -tjf archive.tar.bz2
```

This produces the following output:

```
etc/
etc/sysconfig/
etc/sysconfig/network-scripts/
etc/sysconfig/network-scripts/ifup-aliases
etc/sysconfig/network-scripts/ifcfg-lo
```

To list an archive and see the file details for its contents, you add the -v option to the existing command to see an output of the details:

```
tar -tvjf archive.tar.bz2
```

This returns output similar to the following:

```
drwxr-xr-x root/root        0 2004-04-02 15:56:13 etc/
drwxr-xr-x root/root        0 2004-04-01 14:28:40 etc/sysconfig/
drwxr-xr-x root/root        0 2003-08-13 11:10:49 etc/sysconfig/
►network-scripts/
```

![](img/49f4f38f3aec011238fa50f89e643db3_372_0.png)

> When you create an archive with the -v option, a list of the files being archived is shown onscreen. When you unarchive an archive with the -v option, it shows a similar list of the files being unarchived.
> 
> It's only when you list an archive with the -v option that you get the type of output that approximates an ls -l command being run on the archive contents. This is an exam topic, so be ready for it.

### Other Compression Utilities

Whereas the tar command is used to gather files and put them in a container, the compress, gzip, and bzip2 commands are used to compress that container. Used by themselves, they act on each file they find and replace that file with a compressed version that has an extension that indicates the file is compressed.

### compress, uncompress, and zcat

Some older utilities are no longer used or have been obsoleted by the rise of gzip and bzip2. Chief amongst them is the compress utility.

The exams don't focus much on compress or its sister utility, *uncompress*. It's enough to know the information in this small section so you can identify a *compress* archive and know what to do with it.

*compress*, *uncompress*, and *zcat* are utilities that date back to when the *tar* command didn't offer the *gzip* and *bzip2* compression options.

Creating an archive in precompression *tar* days was a two-step process: You archived the files in a *.tar* file and then ran *compress*, *gzip*, or *bzip2* on the file. Using any of the three replaced the original file with one that added an extension to the original filename that indicated it was compressed.

For example, the first step in the process is to use the following command to create a *.tar* file:

```
tar -cf archive.tar /tarfoo
```

This creates a file named *archive.tar* in the current directory. The next step is to run the *compress* command on the file:

```
compress archive.tar
```

This produces a file named *archive.tar.z* in the current directory, replacing the *archive.tar* file.

Using *uncompress*, you can then uncompress the *archive.tar.z* archive with the following command:

```
uncompress archive.tar.z
```

Or, you can use the *gunzip* command to uncompress the file, meaning you can then recompress it with *gzip* or do whatever you want with it:

```
gunzip archive.tar.z
```

Either way, uncompressing the *archive.tar.z* file removes the compression and the *.z* extension, leaving only the original *.tar* file.

Another utility used in conjunction with the *compress* and *uncompress* commands is the *zcat* utility. You should never use *zcat* on a *.z* compressed file because it shows the contents of the file as if you had used *cat* on the original file and makes a lot of horrible beeping noises when the control codes in the binary file are shown onscreen.

For example, you can take a compressed file such as a copy of the /etc/sysconfig directory contained in a file named *sysconfig.tar.gz* and uncompress it with the *tar* command and the *zcat* command:

```
zcat sysconfig.tar.gz | tar xvf -
```

This command uncompresses a copy of the etc/sysconfig directory and its contents in the current directory, in a tree that begins with the etc directory. The use of a hyphen (-) as the file specifier in the tar command means that tar is accepting the standard output of the zcat command and sending that output directly to the tar command as a set of files to be uncompressed.

![](img/49f4f38f3aec011238fa50f89e643db3_374_0.png)

> This is useful for only one or two exam questions if you find yourself on an older system or a Solaris box that offers only precompression tar.

### Using gzip and bzip2 for Compression

The gzip and bzip2 compression utilities are more up-to-date and useful than compress and zcat, and they are similar in their functions and operations. The main difference is that bzip2 offers slightly better compression than gzip, but gzip is much more widely used.

![](img/49f4f38f3aec011238fa50f89e643db3_374_1.png)

> These commands replace the original file with a new file that has an additional extension, so don't delete the .gz or .bz2 files with you create. They are the original files in a compressed wrapper!

To compress all the files in the current directory with gzip or bzip2, use this command:

```
gzip *
```

This replaces all the regular files (not the directories or their contents) in the current directory with the original filenames plus a .gz extension. So, if you had two files named file1 and file2 in the directory, they would be replaced with

```
file1.gz
file2.gz
```

To uncompress these files, just do the exact opposite of the compression:

```
gunzip *
```

This restores the original files.

Using bzip2 produces the same sort of results. You can issue the following command in the same directory:

```
bzip2 *
```

You would then have the following two files:

`file1.bz2`
`file2.bz2`

To uncompress these files, issue this command:

`bunzip2 *`

This restores the files to their original states.

> **ALERT**
> 
> Watch for questions that ask about why you'd use either **gzip** or **bzip2** for a particular compression task (**bzip2** offers slightly better compression).

## Maintaining System Time

Systems need to have the correct time for so many reasons, not the least of which are sending messages, putting entries in log files, copying files, and completing transactions in databases.

The primary source of organized time synchronization is the Network Time Protocol (NTP) protocol and suite of tools. NTP is comprised of a daemon (`ntpd`), a configuration file (`/etc/ntp.conf`), and various utilities that help maintain system time. NTP works by connecting both to peer servers and more authoritative time servers across the network and Internet.

The overall goal of NTP is to frequently compare time with peers and the upper-tier servers, so that when disconnection from an upper-tier source or network outages occur, relatively correct time can be maintained.

NTP was developed and designed to use multiple tiers of time sources. The time sources and their levels are

- **Tier 1**—Usually physically connected to a time-source, (the atomic clock)
- **Tier 2**—Hosts that communicate directly with Tier 1 sources
- **Tier 3**—Your local time server, or your ISP's
- **All else**—As many layers as you want to maintain

Figure 13.2 shows the hierarchical nature of the NTP sources.
