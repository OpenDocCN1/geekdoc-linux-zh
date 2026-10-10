
## 8.5 Exercises

Configuring and testing printers involves being in the possession of one, and having access to the root account. If so, you may try:

- Installing the printer using the GUI on your system.
- Printing a test page using the GUI.
- Printing a test page using the `lp` command.
- Print from within an application, for example Mozilla or OpenOffice, by choosing File->Print from the menu.
- Disconnect the printer from the network or the local machine/print-server. What happens when you try to print something?

The following exercises can be done without printer or root access.

- Try to make PostScript files from different source files, (e.g. HTML, PDF, man pages). Test the results with the `gv` viewer.
- Check that the print daemon is running.
- Print the files anyway. What happens?
- Make a PostScript file using Mozilla. Test it with `gv`.
- Convert it to PDF format. Test with `xpdf`.
- How would you go about printing a GIF file from the command line?
- Use `a2ps` to print the `/etc/profile` file to an output file. Test again with `gv`. What happens if you don't specify an output file?

## Chapter 9
### Fundamental Backup Techniques

Accidents will happen sooner or later. In this chapter, we'll discuss how to get data to a safe place using other hosts, floppy disks, CD-ROMs and tapes. We will also discuss the most popular compressing and archiving commands.

Upon completion of this chapter, you will know how to:

- Make, query and unpack file archives
- Handle floppy disks and make a boot disk for your system
- Write CD-ROMs
- Make incremental backups
- Create Java archives
- Find documentation to use other backup devices and programs
- Encrypt your data

## 9.1 Introduction

Although Linux is one of the safest operating systems in existence, and even if it is designed to keep on going, data can get lost. Data loss is most often the consequence of user errors, but occasionally a system fault, such as a power or disk failure, is the cause, so it's always a good idea to keep an extra copy of sensitive and/or important data.

### 9.1.1 Preparing your data

#### 9.1.1.1 Archiving with tar

In most cases, we will first collect all the data to back up in a single archive file, which we will compress later on. The process of archiving involves concatenating all listed files and taking out unnecessary blanks. In Linux, this is commonly done with the **tar** command. **tar** was originally designed to archive data on tapes, but it can also make archives, known as **tarballs**.

**tar** has many options, the most important ones are cited below:

- `-v:` verbose
- `-t:` test, shows content of a tarball
- `-x:` extract archive
- `-c:` create archive
- `-f archive_device`: use `archive_device` as source/destination for the tarball, the device defaults to the first tape device (usually `/dev/st0` or something similar)
- `-j:` filter through **bzip2**, see Section 9.1.1.2

It is common to leave out the dash-prefix with **tar** options, as you can see from the examples below.

**Use GNU tar for compatibility**

The archives made with a proprietary **tar** version on one system, may be incompatible with **tar** on another proprietary system. This may cause much headaches, such as if the archive needs to be recovered on a system that doesn't exist anymore. Use the GNU **tar** version on all systems to prevent your system admin from bursting into tears. Linux always uses GNU **tar**. When working on other UNIX machines, enter **tar --help** to find out which version you are using. Contact your system admin if you don't see the word GNU somewhere.

In the example below, an archive is created and unpacked.

```bash
gaby:~> ls images/
me+tux.jpg  nlmf.jpg

gaby:~> tar cvf images-in-a-dir.tar images/
images/nlmf.jpg
images/me+tux.jpg

gaby:~> cd images

gaby:~/images> tar cvf images-without-a-dir.tar *.jpg
me+tux.jpg
nlmf.jpg

gaby:~/images> cd
```

```bash
gaby:~> ls */\*.tar
images/images-without-a-dir.tar

gaby:~> ls \*.tar
images-in-a-dir.tar

gaby:~> tar xvf images-in-a-dir.tar
images/
images/nlmf.jpg
images/me+tux.jpg

gaby:~> tar tvf images/images-without-a-dir.tar
-rw-r-r--- gaby/gaby  42888 1999-06-30 20:52:25 me+tux.jpg
-rw-r-r--- gaby/gaby   7578 2000-01-26 12:58:46 nlmf.jpg

gaby:~> tar xvf images/images-without-a-dir.tar
me+tux.jpg
nlmf.jpg

gaby:~> ls \*.jpg
me+tux.jpg   nlmf.jpg
```

This example also illustrates the difference between a tarred directory and a bunch of tarred files. It is advisable to only compress directories, so files don't get spread all over when unpacking the tarball (which may be on another system, where you may not know which files were already there and which are the ones from the archive).

When a tape drive is connected to your machine and configured by your system administrator, the file names ending in .tar are replaced with the tape device name, for example:

```bash
tar cvf /dev/tape mail/
```

The directory mail and all the files it contains are compressed into a file that is written on the tape immediately. A content listing is displayed because we used the verbose option.

### 9.1.1.2 Incremental backups with tar

The tar tool supports the creation of incremental backups, using the -n option. With this option, you can specify a date, and tar will check modification time of all specified files against this date. If files are changed more recent than date, they will be included in the backup. The example below uses the timestamp on a previous archive as the date value. First, the initial archive is created and the timestamp on the initial backup file is shown. Then a new file is created, upon which we take a new backup, containing only this new file:

```bash
jimmy:~> tar cvpf /var/tmp/javaproggies.tar java/\*.java
java/btw.java
java/error.java
java/hello.java
java/income2.java
java/income.java
java/inputdevice.java
java/input.java
java/master.java
java/method1.java
java/mood.java
java/moodywaitress.java
java/test3.java
java/TestOne.java
java/TestTwo.java
java/Vehicle.java
```

```bash
jimmy:~> ls -l /var/tmp/javaproggies.tar
-rw-rw-r- 1 jimmy    jimmy    10240 Jan 21 11:58 /var/tmp/javaproggies.tar
```

```bash
jimmy:~> touch java/newprog.java
```

```bash
jimmy:~> tar -n /var/tmp/javaproggies.tar \
-cvp /var/tmp/incremental-javaproggies.tar java/*.java 2> /dev/null
java/newprog.java
```

```bash
jimmy:~> cd /var/tmp/
```

```bash
jimmy:~> tar xvf incremental-javaproggies.tar
java/newprog.java
```

Standard errors are redirected to /dev/null. If you don't do this, tar will print a message for each unchanged file, telling you it won't be dumped.

This way of working has the disadvantage that it looks at timestamps on files. Say that you downloaded an archive into the directory containing your backups, and the archive contains files that have been created two years ago. When checking the timestamps of those files against the timestamp on the initial archive, the new files will actually seem old to tar, and will not be included in an incremental backup made using the -N option.

A better choice would be the -g option, which will create a list of files to backup. When making incremental backups, files are checked against this list. This is how it works:

```bash
jimmy:~> tar cvpf work-20030121.tar -g snapshot-20030121 work/
work/file1
work/file2
work/file3
jimmy:~> file snapshot-20030121
snapshot-20030121: ASCII text
```

The next day, user *jimmy* works on `file3` a bit more, and creates `file4`. At the end of the day, he makes a new backup:

```bash
jimmy:~> tar cvpf work-20030122.tar -g snapshot-20030121 work/
work/
work/file3
work/file4
```

These are some very simple examples, but you could also use this kind of command in a crontab (see Section 4.4.4), which specifies for instance a snapshot file for the weekly backup and one for the daily backup. Snapshot files should be replaced when taking full backups, in that case.

More information can be found in the `tar` documentation.

**The real stuff**

![](img/996aa590a5237ef824c7c29efdbb64f8_204_0.png)

As you could probably notice, `tar` is OK when we are talking about a simple directory, a set of files that belongs together. There are tools that are easier to manage, however, when you want to archive entire partitions or disks or larger projects. We just explain about **tar** here because it is a very popular tool for distributing archives. It will happen quite often that you need to install a software that comes in a so-called "compressed tarball". See Section 9.3 for an easier way to perform regular backups.

### 9.1.1.3 Compressing and unpacking with `gzip` or `bzip2`

Data, including tarballs, can be compressed using zip tools. The `gzip` command will add the suffix .gz to the file name and remove the original file.

```bash
jimmy:~> ls -la | grep tar
-rw-rw-r-- 1 jimmy jimmy    61440 Jun  6 14:08 images-without-dir.tar

jimmy:~> gzip images-without-dir.tar

jimmy:~> ls -la images-without-dir.tar.gz
-rw-rw-r-- 1 jimmy jimmy    50562 Jun  6 14:08 images-without-dir.tar.gz
```

Uncompress gzipped files with the -d option.

**bzip2** works in a similar way, but uses an improved compression algorithm, thus creating smaller files. See the `bzip2` info pages for more.

Linux software packages are often distributed in a gzipped tarball. The sensible thing to do after unpacking that kind of archives is find the README and read it. It will generally contain guidelines to installing the package.

The GNU `tar` command is aware of gzipped files. Use the command
