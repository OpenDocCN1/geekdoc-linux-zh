
You can verify the contents of an archive by using *zasc*'s option to list pathnames and files in an archive. For example, to decompress and see the contents of the new archive, use the tar command like this:

```
# tar txf home01.tgz
home/bball/Xdefaults
home/bball/Xresources
home/bball/.bashrc
home/bball/.dayplan
home/bball/.dayplan.priv
home/bball/.dviprc
home/bball/.emacs
home/bball/.exrc
home/bball/.ginitrc
home/bball/.grok
...
```

Note that not all the output is shown here, and that the leading directory path designator (.) is not present. This is important to remember when restoring files to their proper directories in your filesystem. Decompressing an archive is easy. Use the tar command, along with its *z* or *extract* option, and if extracting from a compressed archive, include the *z* option like this:

```
# tar xzvf home01.tgz
```

The *v* or verbose option will list the files being extracted, or else the action occurs silently.

By combining the power of the tar command and the archive creation and compression features of *tar*, even novice system administrators can quickly build backup scripts to accomplish the hard work of performing backup operations. This task becomes even easier when you add automation, and perform these tasks unaided on a regularly scheduled basis. To learn how to do this, read the next section about using cron for system administration.

## Scheduling with cron

Every Linux distribution includes the cron daemon, or some other software mechanism for performing regularly scheduled tasks. While the at command helps users to perform specific tasks at a specified time, the *cron* daemon is generally used for system-wide administrative tasks that need to be performed repeatedly.

Like other network or server services, the `cron` scheduling service is controlled by startup scripts under your system's `/etc/rc.d/init.d` or `/etc/init.d` directories. This service should always be started on your system, because it initiates pre-programmed tasks that are essential to the health and well-being of your filesystem.

The `cron` daemon checks the `cron` table, `/etc/crontab`, every minute for instructions regarding what task to run at a given time. The table's format is documented in the `crontab` manual page, and looks like this (on a LinuxPPC 2000 Q4 system):

```
SHELL=/bin/bash
PATH=/usr/sbin:/usr/bin:/sbin:/bin
MAILTO=root
HOME=/

# m h dom mon dow user  command
00 2  * * *  root run-parts /etc/cron-weekly
30 4 * *  1    root run-parts /etc/cron-monthly
50 4  * * 0   root run-parts /etc/cron-weekly
42 4 1 * *    root run-parts /etc/cron-monthly
```

The first part of the `crontab` file contains options settings for the default shell, the `path(s)` to use, and who to e-mail about problems or task completion. The `run-parts` section is the actual table, which consists of a number of fields.

The first five fields (from left to right) designate when to run a task and include the `minute`, `hour`, `day of month`, `month`, and `day of week`. The rest of the line is a command line, which uses the `run-parts` shell script to execute scripts found under the `/etc/daily`, `/etc/weekly`, `/etc/monthly`, and `/etc/annually` directories. For example, if you look under the `/etc/daily` directory, you will see a number of scripts like these:

```
$ ls /etc/cron-daily
fskscan  inn-cron-expire  logrotate  slocate.cron  tetex.cron
bridge-tizer  inn-cron-news  makewhatis.cron  elfsync-expire  tmpwatch
```

These scripts perform quite a bit of house keeping for your system, such as handling Usenet newsfeeds (if enabled), updating the `slocate` search database, and rebuilding the `tex` command's database. SuSE Linux has a similar `crontab`, but takes a different approach:

```
SHELL=/bin/bash
PATH=/usr/bin:/usr/sbin:/sbin:/bin:/usr/lib/news/bin
MAILTO=root

*    * * * *  root test -x /usr/sbin/atrun && /usr/sbin/atrun
0 21 * * * root test -x /usr/sbin/faxqclean && /usr/bin/faxqclean
5 22 * * * root test -x /usr/sbin/faxexpire && /usr/bin/faxexpire
25 23 * * * root test -e /usr/sbin/faxcron && sh /usr/sbin/faxcron | mail FaxMaster
#check scripts in cron.hourly, cron.daily, cron.weekly and cron.monthly
-*/15 * * * * root test -x /usr/lib/cron/run-crons && /usr/lib/cron/run-crons
0 0 * * * root rm -f /var/spool/cron/lastrun/cron.daily
0 0 * * 6 root rm -f /var/spool/cron/lastrun/cron.weekly
0 0 1 * * root rm -f /var/spool/cron/lastrun/cron.monthly
```

Under SuSE Linux, services for the at command, faxing, and newsreading are handled by entries in the first half of the table. In the second half, the /usr/lib/cron/run-crons script is executed every 15 minutes, and checks for scripts under /etc/cron.xxxx directories for jobs to run each hour, day, week, or month.

> The hyphen (-) preceding the minute crontab entry tells the cron daemon not to use e-mail after successfully running a task. This will keep root's mailbox from getting too cluttered!

However, you can craft your own crontab entries, and run tasks directly from the system's crontab file. As the root operator, edit /etc/crontab with your favorite text editor. You can try some sample entries like these:

- * * * * * root /sbin/clock -w
- */2 * * * * root /usr/bin/rddate -s ntp2.usno.navy.mil
- 0,15,30,45 * * * * root /usr/bin/play /usr/share/sounds/wav/silphon.wav
- 0 1 * * * root /usr/bin/find / -xdev -name core -exec /bin/rm '\{' \;
- 15 2 * * * root /bin/tar czf /d3/sunday.tgz /
- * 12 25 12 * root /bin/echo 'Happy Holidays' | /bin/mail -s Xmas root

The first example runs the clock command every minute to update the computer's hardware clock using the Linux system time. The second example retrieves the current time every two minutes from the Internet and updates the system clock. The third example plays a ship's horn every 15 minutes. The fifth example, used for cleaning up your system, searches the directories at 1:00 AM each morning for core files and deletes them. The sixth example creates a backup of your entire filesystem (excluding remotely mounted drives) every Sunday at 2:15 AM. The last example e-mails a holiday greeting every December 25th at noon.

Combine your system administration tasks with automation by first testing your scripts, and then using them in your `crontab`. If you do not feel like crafting scripts at the top level, then use the various hourly, daily, weekly, or monthly directories as a starting place. For efficiency’s sake, make sure to run backup operations after cleanup operations, such as system-wide deletions of core, .bak, or other files.

## Using HFS Utilities

Many Linux (especially PowerPC Linux) distributions come with a variety of software tools aimed at making life easier when dealing with Mac OS volumes. Table 16.2 lists a number of HFS utilities you can use during your Linux sessions.

### Table 16.2 Linux Mac OS HFS Utilities

| Name | Description |
| :--- | :--- |
| hattrib | Modify HFS file or directory attributes |
| hcd | Change working HFS directory |
| hcopy | Copy files to or from HFS volume |
| hdel | Delete both data and resource forks of HFS file |
| hdir | Detailed display of an HFS directory |
| hformat | Format and create new HFS filesystem |
| hfs | Shell for manipulating HFS volumes |
| hfssh | Tcl interpreter with HFS extensions |
| hfsutils | Introduction to HFS utilities |
| hls | Display files in HFS directory |
| hmkdir | Make new HFS directory |
| hmount | Mount an HFS volume |
| hpwd | Print current HFS working directory |
| hrename | Rename HFS file or directory |
| hrmdir | Delete an empty HFS directory |
| hunmount | Unmount an HFS volume |
| hvol | Display and/or change current HFS volume |
| mkhybrid\* | Create hybrid ISO9660/JOLIET/HFS filesystem |
| xhfs | GUI tool for manipulating HFS volumes |

\*not part of the `hfsutils` package

## Command-Line Tools

Using the HFS utilities is fairly easy. You need to know the proper device for the desired volume to use. For example, after installing PowerPC Linux on your Macintosh, you should know the partition number for at least one Mac HFS volume. Note that one limitation of the HFS utilities is that they only work with HFS standard volumes, not new HFS extended volumes.

![](img/1ea833f5a3e3c1547e3dd2891f52804a_437_0.png)

> Support for the Mac OS HFS+ filesystem has started, but is still in its infancy and no software has been released. The current project (see "Resources" at the end of this chapter) aims to provide some form of support in the Linux 2.4-series kernels.

In order to access an HFS volume, use the mount command, followed by a device name, like this (as root):

```
# mount /dev/hda10
Volume name is "hfsboot"

Volume was created on Thu Apr 5 15:59:00 2001
Volume was last modified on Tue Apr 10 15:13:43 2001
Volume has 18280448 bytes free
```

You can then get information about the volume by using the hvol command like this:

```
$ hvol
Current volume is mounted from:

    /dev/hda10

Volume name is "hfsboot"
Volume was created on Thu Apr 5 15:59:00 2001
Volume was last modified on Tue Apr 10 15:13:43 2001
Volume has 18280448 bytes free
```

To list files and directories on the volume, use the hls command:

```
$ hls
Desktop Folder  Linux Kernels  System Folder
```

## Graphical HFS Tools

For a graphical interface to using and manipulating your mounted HFS volume during an X session, use the xhfs client from the command line like this (as root):

```
# xhfs &
```
