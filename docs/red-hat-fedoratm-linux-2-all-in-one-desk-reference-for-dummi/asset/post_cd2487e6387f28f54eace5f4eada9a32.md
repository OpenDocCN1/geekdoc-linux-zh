
matching file. The last part (`2> /dev/null`) simply sends the error messages to a special file that's the equivalent of simply ignoring them.

You can use variations of this simple form of `find` to locate a file in any directory (as well as any subdirectories contained in the directory). If you forget where in your home directory you have stored all files named `report*` (names that start with `report`), you can search for the files by using the following command:

```
find ~ -name "report*" -print
```

When you become comfortable with this syntax of `find`, you can use other options of `find`. For example, to find only specific types of files (such as directories), use the `type` option. The following command displays all top-level directory names in your Linux system:

```
find / -type d -maxdepth 1 -print
```

You probably don't have to use the complex forms of `find` in a typical Linux system — but if you ever need to, you can look up the rest of the `find` options by using the following command:

```
man find
```

![](img/9f89727199836b0f871f1745838aa8b2_192_0.png)

An easy way to find all files that match a name is to use the `locate` command that searches a periodically updated database of files on your system. For example, here's what I get when I type `locate xorg.conf` on my system:

```
/usr/X11R6/man/man5/xorg.conf.5x.gz
/xorg.conf.new
/etc/X11/xorg.conf
```

# Commands for mounting and unmounting

Suppose you want to access the files on this book's companion DVD-ROM when you are logged in at a text console (with no GUI to help you). To do so, you have to first mount the DVD-ROM drive's file system on a specific directory in the Linux file system.

![](img/9f89727199836b0f871f1745838aa8b2_192_1.png)

By the way, the procedure I am about to describe works for CDs as well as DVDs.

**Log in as `root` (or type `su -` to become `root`)**, insert the DVD-ROM in the DVD drive, and then type the following command:

```
mount /dev/cdrom /mnt/cdrom
```

This command mounts the file system on the device named `/dev/cdrom` (the DVD/CD-ROM) on the `/mnt/cdrom` directory (which is also called the *mount point*) in the Linux file system.

After the `mount` command successfully completes its task, you can access the files on the DVD-ROM by referring to the `/mnt/cdrom` directory as the top-level directory of the disc. In other words, to see the contents of the DVD-ROM, type

```
ls -F /mnt/cdrom
```

When you're done using the DVD-ROM — and before you eject it from the drive — you have to “unmount” the disc drive with the following `umount` command:

```
umount /dev/cdrom
```

![](img/9f89727199836b0f871f1745838aa8b2_193_0.png)

Mounting devices on directories in the `/mnt` directory is customary. Linux comes with the two predefined directories: `/mnt/cdrom` for mounting the DVD/CD-ROM and `/mnt/floppy` for mounting the floppy drive.

# Commands for checking disk-space usage

I want to tell you about two commands — `df` and `du` — that you can use to check the disk-space usage on your system. These commands are simple to use. The `df` command shows you a summary of disk-space usage for all mounted devices, as shown in this example:

```
df
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/hda5             7392428   3855112    3161800  55% /
/dev/hda3              101105     15760       80124  17% /boot
none                   127880         0      127880   0% /dev/shm
/dev/cdrom             658144    658144           0 100% /mnt/cdrom
```

The output is a table that shows the device, the total kilobytes of storage, how much is in use, how much is available, the percentage being used, and the mount point.

![](img/9f89727199836b0f871f1745838aa8b2_193_1.png)

To see the output of `df` in a more human-readable format, type `df -h`. Here is the output of the `df -h` command:

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/hda5        7.1G  3.7G  3.1G  55% /
/dev/hda3         99M   16M   79M  17% /boot
none             125M     0  125M   0% /dev/shm
/dev/cdrom       643M  643M     0 100% /mnt/cdrom
```

If you compare this output with the output of plain `df` (see previous listing), you see that `df -h` prints the sizes with terms like **M** for megabytes and **G** for gigabytes. These are clearly easier to understand than 1K-blocks.

The other command — `du` — is useful for finding out how much space a directory takes up. For example, type the following command to view the contents of all the directories in the `/etc/rc.d` directory (this directory contains system startup files):

```
du /etc/rc.d
4            /etc/rc.d/rc1.d
4            /etc/rc.d/rc0.d
4            /etc/rc.d/rc5.d
4            /etc/rc.d/rc3.d
4            /etc/rc.d/rc4.d
4            /etc/rc.d/rc2.d
308          /etc/rc.d/init.d
4            /etc/rc.d/rc6.d
372          /etc/rc.d
```

Each directory name is preceded by a number — which tells you the number of kilobytes of disk space used by that directory. Thus the `/etc/rc.d` directory, as a whole, uses 372K disk space whereas the `/etc/rc.d/init.d` subdirectory uses 308K. If you simply want the total disk space used by a directory (including all the files and subdirectories contained in that directory), use the `-s` option, as follows:

```
du -s /etc/rc.d
372          /etc/rc.d
```

The `-s` option causes `du` to print just the summary information for the `/etc/rc.d` directory.

Just as `df -h` prints the disk-space information in megabytes and gigabytes, you can use the `du -h` command to view the output of `du` in more human-readable form. For example, here’s how I combine it with the `-s` option to see the space I’m using in my home directory (`/home/naba`):

![](img/9f89727199836b0f871f1745838aa8b2_194_0.png)

```
du -sh /home/naba
29M          /home/naba
```

# Chapter 4: Exploring Fedora Core Applications

**In This Chapter**

-   ✔ Taking stock of Fedora Core applications
-   ✔ Exploring office applications
-   ✔ Setting up databases
-   ✔ Playing with multimedia
-   ✔ Working with images

Fedora Core comes with a whole lot of applications. All you have to do is look at the menus in GNOME or KDE and you’ll see what I mean. Often, there is more than one application of each type. Both GNOME and KDE come with the OpenOffice.org office application suite with a word processor, spreadsheet, presentation software, and more. You find many choices for CD players and multimedia players, not to mention the games, utility programs, and useful tools, such as a scanner and digital camera applications.

I give you an overview of some of these applications and briefly show you some interesting and useful applications. After you know about these applications, you can try them out when you need them.

## Taking Stock of the Fedora Core Applications

Table 4-1 shows a sampling of major Fedora Core applications, organized by category. For the major applications, I also show a relevant Web site where you can get more information about that application. This list is by no means comprehensive. Fedora Core distribution comes with many more applications and utilities than the ones I show in this table.

If your system has both GNOME and KDE installed, most of these applications are already available from either GUI desktop.

I briefly introduce some of the applications from Table 4-1, selecting one or two from each category. I describe the Internet applications in Book V.

# 170 Taking Stock of the Fedora Core Applications

**Table 4-1 A Sampling of Fedora Core Applications**

| Application | Description |
| :--- | :--- |
| **Office Applications** | |
| OpenOffice.org Writer | A word-processing program similar to Microsoft Word (www.openoffice.org) |
| OpenOffice.org Calc | A spreadsheet program similar to Microsoft Excel (www.openoffice.org) |
| OpenOffice.org Impress | A presentation application similar to Microsoft PowerPoint (www.openoffice.org) |
| OpenOffice.org Draw | A drawing program (www.openoffice.org) |
| OpenOffice.org Math | An equation editor for writing mathematical equations, which you can then include in OpenOffice.org Writer documents (www.openoffice.org) |
| Dia | A drawing program, designed to be like the Windows application called Visio (www.gnome.org/gnome-office/dia.shtml) |
| **Office Tools** | |
| GNOME Calculator | A simple calculator |
| Kcalc | A calculator (part of KDE) |
| Aspell | A text-mode spell checker (aspell.sourceforge.net) |
| Dictionary | A graphical client for the dict.org dictionary server so you can look up words |
| **Database** | |
| PostgreSQL | A sophisticated object-relational database-management system that supports Structured Query Language (SQL) (www.postgresql.org) |
| MySQL | A popular relational database-management system that supports SQL (www.mysql.com) |
| **Multimedia** | |
| GNOME CD Player | An audio CD player (needs a working sound card) |
| KsCD | Audio CD player from KDE (needs a working sound card) |
| Rhythmbox | A multimedia audio player that can play several different sound formats (rhythmbox.sourceforge.net) — including MP3 files if you download a plugin for the purpose |
| XMMS | X Multimedia System — a multimedia audio player that can play many different sound formats (www.xmms.org) — including MP3 files if you download a plugin for the purpose (XMMS is not installed by default, but you can install it easily from the companion DVD) |
