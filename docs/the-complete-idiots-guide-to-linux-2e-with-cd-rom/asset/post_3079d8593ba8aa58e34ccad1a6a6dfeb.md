
To extract files backed up with dump, use restore. The restore copies files stored in a dump tape or file to the current directory. It's important to note that using restore can, and will, clobber existing files with matching names. Restore will also create any directories or directory trees that it needs before extracting a file. This feature is powerful if you know what you are doing. When in doubt, extract files using restore to an empty directory and move the files by hand. Restore has the following syntax:

```
restore [options [argument ...]]
```

To specify the device holding your backup, use the -f option and follow it by the location of your dump.

The restore command has an easy-to-use interactive shell-like interface that allows you to navigate through the dump tape as if you were in a file system. The interactive session is started by using the -i option:

```
restore -f /dev/nst0 -i
```

When restore loads, you can use commands such as cd and ls to move around the tape catalog. These commands are built into restore and are not the same ones you use on a shell.

To add a file to a list of files you wish to extract (restore), type add filename, where filename is the name of the file you want to extract. If you add a directory, all files and directories it contains are added. To remove files from a list, type del filename. This command doesn't delete the file from the tape; it just removes it from the extract list. To extract the files, just type extract. At the end of the extraction, you will be asked if you want to set the owner/mode for '.'?[yn] You should respond no, as this could change the owner and mode of the directory where restore is going to extract files from.

Here's a sample session:

```
1: [root@digital /tmp]# restore -i -f /dev/nst0
2: restore > ls
3: :.
4: auto/ dev/ etc/ home/ root/ tmp/ var/
5: restore > add home
6: restore > ls
7: :.
8: auto/ dev/ etc/ *home/ root/ tmp/ var/
9:
10: restore > del home
11: restore > ls
12: :.
13: auto/ dev/ etc/ home/ root/ tmp/ var/
14:
15: restore > cd home/alberto/test
16: restore > ls
17: ./home/alberto/test:
18: afile
19:
20: restore > add afile
21: restore > extract
22: You have not read any tapes yet.
23: Unless you know which volume your file(s) are on you should start
24: with the last volume and work towards the first.
25: Specify next volume #: 1
26: restore > quit
27: [root@digital /tmp]# ls
28: home
29: [root@digital /tmp]# cd home/alberto/test
30: [root@digital test]# ls
31: afile
```

The version of restore shipped with my version of Linux has a problem. If you try to add a file, it will give you an error message. The workaround is to add a directory such as home (see line 5 of the previous listing). Note that when you add a file or a directory, restore marks it by placing a star (*) next to it (see line 8). After adding this directory, delete it (see line 10). Then you can go ahead and add files as you want. Parent directories will be automatically added. When you are done making your file selection, type extract (see line 21). Dump will ask you to read a tape. If your dump only spans one tape, type 1; otherwise, type the number of the last tape you used for this dump. To get information on a dump, type what. To get help on an interactive restore, type help or ?, which will print the following information:

```
restore > ?
Available commands are:
    ls [arg] - list directory
    cd arg - change directory
    pwd - print current directory
    add [arg] - add `arg' to list of files to be extracted
    delete [arg] - delete `arg' from list of files
        to be extracted
    extract - extract requested files
    setmodes - set modes of requested directories
    quit - immediately exit program
    what - list dump header information
    verbose - toggle verbose flag (useful with `ls')
    help or `?' - print this list
If no `arg' is supplied, the current directory is used
```

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## restore Examples

Restoring interactively is easier than using the command line. However, you can do this too. To restore a particular file, specify the -x option and provide a path relative of root, like this:

```
restore -x home/alberto/file.rtf -f /dev/nst0
```

The preceding command will extract (-x) the file specified (/home/alberto/file.rtf) from the tape to the current directory. If the directory path doesn't exist, restore will create them. It's a good idea to change directory to /tmp so that recovered files go to a safe place and existing files are not overwritten. After the file has been recovered, you can move the file to its final destination.

To create a catalog from files on a dump tape, use the -t option. Unless you know that your tape drive supports read-behind-write verification, it is always a good idea to create a catalog from your tape. This will ensure that the backup tape you made contains the correct information and that the tape is readable.

To create a catalog, enter the following:

```
restore -t -f /dev/nts0 > tapecat.txt
```

This will create a file called tapecat.txt with the listing of the files on your tape.

## Graphical Backup Programs

There are a couple of graphical backup programs available: BRU2000, included on your CD, and KDat, a KDE backup application (go to http://www.kde.org for more information on KDat).

## BRU2000

Currently, OpenLinux is including a license to BRU2000, a program that can be used both through the command line and a graphical interface to perform dump-like backups of your system. The big advantage over dump is in using its graphical user interface, so it is easy to use. Not having to worry about tape sizes and other insidious details could be well worth it. Using the program is self-explanatory. You first select your backup device (/dev/nst0 or whatever applies to you). To create your backup device, just use the New Device command under the File menu. After you've selected your backup device, you'll need to pick your backup options from the Backup command under the options menu. A dialog box will require various settings. Then click the backup button. This will prompt you for the files you want to back up. From there, click the Start Backup button, and you are on your way.

Like dump, BRU supports incremental backups, so you can implement the backup strategy discussed in the section “A Backup Strategy.”

Here are some screen shots of the program:

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_0.png)

![](img/edf072a03d4de1f8f4a13465ac79e7fb_242_1.png)

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Chapter 20
Installing Programs and Applications

### In This Chapter

- RPM: The Red Hat Package Manager
- Installing, Upgrading, Downgrading, and Removing Software
- Verifying Your System
- Graphical Front Ends to RPM
- Non-RPM Packages

Software installation on Linux is fairly sophisticated through the use of RPM. Although you can install software that has been archived by tar and other programs, most of the time you'll want to install RPM packages. It goes without saying that when you have a choice on what package format to install, pick the RPM version. RPM packages provide a multitude of benefits, and that's why we'll cover it in great detail.

## RPM: The Red Hat Package Manager

RPM is an open software and source packaging system. It was initially developed for Linux but has since made available for anyone to use under the GPL.

RPM is a great packaging system because it not only deals with installing software as other systems have done for years but also maintains a database of
