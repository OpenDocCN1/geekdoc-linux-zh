
The main weapon in your arsenal is the `find` command. This command can quickly traverse designated directories (and other filesystems) and display found files according to your specifications. For example, you can use the `find` command to search your system for backup files (generally designated with a `.bak` extension) like this:

```
# find / -name *.bak
/home/dball1/Office51/config/rootag.bak
/home/dball1.kde/share/apps/kfm/cookies.bak
/usr/X11R6/lib/X11/xfig/html/images/add-arrow-button.gif.bak
/usr/X11R6/lib/X11/xfig/html/images/open-compound-button.gif.bak
/usr/X11R6/lib/X11/xfig/html/images/screen-image.fig.bak
/usr/X11R6/lib/X11/xfig/html/images/update-control.gif.bak
/var/lib/nfs/sm.bak
/etc/printcap.bak
/root/.kde/share/apps/kfm/cookies.bak
```

You can then quickly delete these files by piping the `find` command's output through the `xargs` command to delete the files with the `rm` command:

```
# find / -name *.bak | xargs rm -f
```

Other candidates for deletion include `*.bak` files, files with an `.o` extension (object files from compile operations), and files with the name "core." If you don't want to delete these files, you can build a candidate list:

```
# find / -name *.o >> files_to_delete.txt
```

## Minimizing System Logs

Another area of your Linux system that will grow over time is your system logs. Logging records nearly every action and output by different software, such as the kernel, mail, database, printing, and other daemons and services. These logs can become quite large, taking up many megabytes of valuable disk space.

Each month, these logs, contained in the `/var/log` directory, are generally “rolled over” and renamed to allow new logs to be created. The old log files have a number such as 1, 2, 3, and so on appended to their file names. After using Linux on your notebook for a while, you can get a quick idea of the size of these logs by using the `find` and `ls` commands:

```
# find /var/log -name *.4 | xargs ls -l
-rw------- 1 root root 645185 Feb 6 04:02 /var/log/cron.4
-rw-r---m 1 root root 0 Jan 30 04:02 /var/log/httpd/access_log.4
-rw-r---m 1 root root 979 Jan 31 13:31 /var/log/httpd/error_log.4
-rw-r--r-- 1 root root 1472087 Feb 6 04:02 /var/log/maillog.4
-rw-r--r-- 1 root root 171891 Feb 6 04:02 /var/log/messages.4
-rw-r-x--x-- 1 root root 0 Oct 12 08:41 /var/log/netconf.log.4
-rw-r-x--x-- 1 root root 23795 Jan 24 09:55 /var/log/samba/log.nmb.4
-rw-r--r-- 1 root root 2300 Feb 4 21:48 /var/log/secure.4
-rw-r--r-- 1 root root 0 Jan 30 04:02 /var/log/spooler.4
-rw-r--r-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Debug.4
-rw-r-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/log.4
-rw-f-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Stats.4
-rw-r--r-- 1 root root 130101 Jan 31 14:20 /var/log/xferlog.4
```

As you can see, some of these logs can get quite large in the course of a single month! If you don't need these files, you can safely delete them and free up disk space.

## Putting It Together with Automation

Linux comes with not only the tools you need to handle finding and deleting files, but also the software required to automate the process.

By using the `cron` daemon and your system's `crontab` table, you can set up Linux to automatically search for and delete unwanted files. Log in as root, and then use your favorite editor to open the `/etc/crontab` file. You might see something like this:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The `/etc/crontab` file contains directions for the `cron` daemon, which is started when you boot Linux. This software, which runs in the background, looks to this file every minute for tasks to run.

In this example, the `cron` daemon looks into the `/etc/cron.hourly` directory every hour on the hour. Once a day at 4:02 a.m., it looks at `/etc/cron.daily` for tasks. Every Sunday at 4:22 a.m., it runs tasks in the `/etc/cron.weekly` directory. And on the first day of every month at 4:42 a.m., the daemon runs the tasks listed in `/etc/cron.monthly`.

If you're satisfied with these times and arrangements, create your command, such as combining the `find` command's output with the `xargs` and `rm` commands, and put it in a text file. Next, name the file and make it executable. For example:

```
chmod +x cleanup
```

Then move the file into the daily, weekly, or monthly directory. For example, to clean up your system logs, you could use this:

```
/usr/bin/find /var/log -name *\*.1 | /usr/bin/xargs /bin/rm -f
```

To have this run on the 15th of every month at 2:30 p.m., you could use an `/etc/crontab` entry like this:

```
30 14 15 * * root /usr/bin/find /var/log -name *\*.1 | /usr/bin/xargs /bin/rm -f
```

## Compression and Compressed Filesystems

Compression of computer data is not only a scientific pursuit, but also an art form. Even before computers were invented, people strived to find better ways to compress data. Hieroglyphics and the cuneiform alphabet could be considered early and rudimentary forms of compressed information. Journalists reporting from battlefields during the telegraph era used compressed language in order to squeeze in as much information as possible, and they put the most important information at the beginning in case the transmission got cut off.

Today, compression is used invisibly when we go online via modem, listen to streaming audio or video, or upload or download files using Web browsers (which can be set to decompress files on-the-fly). The Linux kernel has had the ability to use built-in compression since 1997, but because of the additional overhead in time and hard drive activity, this form of filesystem activity has not caught on in popular distributions.

### In a Squeeze to Try Compression?

Intrepid notebook users who want or need to take advantage of compression can download the `e2compr` kernel patches from

```
http://www.netinspace.net/-reiter/e2compr/
```

You'll need to apply the kernel patches and then use the included utilities to compress and decompress files you use with Linux.

### Compression Use with Linux

The Linux distribution you've installed on your notebook comes with many different utilities for compressing and decompressing files. This section introduces you to compression tools for Linux. These tools, like most other command-line utilities, may be combined with other programs or included in shell scripts to automate file compression during your Linux sessions.

> **Man Page Compression**
>
> Nearly all Linux distributions now use compressed manual pages. These pages, found under the `/usr/man` directories, can be decompressed by utilities specified in the `/etc/man.config` file. Without using compression, these pages of documentation would require 100MB or more of drive space.

Table 8.2 lists a number of compression tools included with Linux. You might (or might not) be surprised to see some old favorites.

### Extracting Archives

You'll most likely run into compressed files when downloading new software or software packaged as source code. Although the standard software package management software for Red Hat, Mandrake, Caldera OpenLinux, and SUSE Linux is the Red Hat Package Manager, or the `rpm` command, many different Linux software developers distribute files in compressed archives known as *tarballs*. These files are easily recognizable, with extensions such as `.tar.gz` and `.tgz`.

Decompressing these files is quite easy using the `gunzip`, `gzip`, or `tar` command. For example, if you download a file that has a `.tar.gz` extension, you can first decompress the file with the `gunzip` command like this:

```
$ gunzip xp2.tar.gz
```

You end up with a file named `xp2.tar`. You can then list the contents of the archive with `tar`'s `-t` (list) option:

```
$ tar tf xp2.tar
...
usr/
usr/X11R6/
usr/X11R6/bin/
```
