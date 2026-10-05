
## Filesystem cleanup

The following crontab entry implements a simple email reminder. (Lines have been fitted to the page. In reality, this is one long line.)

```
30 4 25 * * /usr/bin/mail -s "Time to the TPS reports\nowen@atrust.com%%TPS reports are due at the end of the month! Get busy!\%%Sincerely;%%cron
```

Note the use of the % character both to separate the command from input text and to mark line endings within the input. This entry sends email on the 25th day of each month.

## Filesystem cleanup

Some of the files on any system are worthless junk (not the system files). For example, when a program crashes, the kernel may write out a file (usually named core, core.pid, or program.core) that contains an image of the program's address space. Core files are useful for developers, for administrators they are usually a waste of space. Users often do not know about core files, so they tend not to delete them on their own.

NFS, the Network File System, is described in Chapter 18.

NFSv3 is another extra of files. Because NFSv3 servers are stateless, they have to use a special convention to preserve files that have been deleted locally but in use by a machine. Most implementations rename such files to .nfsxxx, where xxx is a number. Various situations can result in these files being forgotten and left around after they are supposed to have been deleted.

Many programs create temporary files in /tmp or /var/tmp that aren't erased for one reason or another. Some programs, especially editors, like make a backup copy of each file they work.

A solution to the junk file problem is to institute some sort of nightly space reclamation using cron. Modern systems usually come with something of this set up for you, but it's a good idea to review your system's default behavior to make it appropriate for your situation.

Below are several common idioms with the find command.

```
find /xdev -type f '(' -name core -o name '[0-9]*' -o name "core.*") -atime +7 -exec rm -f {} \;
```

This command removes core images that have not been accessed in a week. The xdev argument makes that find does not cross over to filesystems other than the root; restraint is important on networks where many filesystems are cross-mounted. If you want to clean up more than one filesystem, use a separate command for each. (Note that /var is typically a separate filesystem.)

- Many systems' kernels can be configured to put core dumps in a particular directory, or optionally, not generate them at all. For see man core on Linux or marecore on Solaris.
- Not all versions of find support the -xdev argument. On some systems, it is called -x.

![](img/579efec8c67772f31ecf34844bbb71a2_337_0.png)

## Chapter 9

## Periodic Processes

The **-type f** argument is important because the Linux kernel source contains a directory called **core**. You wouldn't want to be deleting that, would you?

```
find / -xdev -atime +3 '-name "*" -o -name "*#" -o -name "*.-*" -o -name "*nfs*" -exec rm -f {} \;
```

This command deletes files that have not been accessed in three days and begin with . or # or nfs or ~ or .CKP. These patterns are typical of various sorts of temporary and editor backup files.

For performance reasons, some administrators use the **noatime** mount option to prevent the filesystem from maintaining access stamps. That configuration will confuse both of the **find** commands as the files will have been unregistered even if they were recently used. Unfortunately, the failure mode is to delete the files; be sure you are maintaining access times before using these commands as shown

```
cd /tmp; find . -name * -type d -mtime +3 -exec rm -f {} \;
```

This command removes all subdirectories of **/tmp** not modified in 72 hours. On most systems, plain files in **/tmp** are removed at boot by system startup scripts. However, some systems do not remove directories. A directory exists is treated specially and is not removed. This is important if /tmp is a separate filesystem. See page 260 for more information about cleanup.

If you use any of these commands, make sure that users are aware of your cleanup policies before disaster strikes!

## Network distribution of configuration files

If you are running a network of machines, it's often convenient to maintain a network-wide version of configuration files such as alias database. Usually the sharing mechanism is some form of periodic distribution, this is also an ideal task for cron. Master versions of system files can be distributed every day with **rsync** or **rdist**.

Sometimes, postprocessing is required. For example, you might need to run **newaliases** to convert aliases to hashed format using **sendmail.cf**. You might also need to load files into an administrative database such as NIS.

## Log rotation

Systems vary in the quality of their log management, and you will probably need to adjust the defaults to conform to your local policies. To divide log into segments by size or by date, keeping older versions available at all times is a regularly scheduled event, an ideal task for cron. See Chapter 11, Syslog and Log Files for more details.

## 9.6 EXERCISES

- 9.1 A local user has been abusing privileges by running tasks at frequent intervals. Asking him to stop you are forced to revoke his privileges and make sure he can't add a new one.
- 9.2 Think of three tasks (other than those mentioned in this chapter) that might need to be run periodically. Write cron entries for each task and specify where they go on your system.
- 9.3 Choose three entries from your system's cron files. Decode each one and describe when it runs, what it does, and why you think the entry is needed (Requires root access.).
- 9.4 Write a script that keeps your startup files synchronized among all the machines on which you have account. Schedule this script to run regularly from cron (Is it safe to blindly copy every file whose name starts with a dot? How will you handle directories? Should files on the destination machines be backed up before they are overwritten?).

## 10 Backups

At most sites, the information stored on computers is worth far more than the computers themselves. It is also much harder to replace. Protecting this information is one of the system administrator's most important (and, unfortunately, most tedious) tasks.

There are hundreds of creative and not-so-creative ways to lose data. Software bugs routinely corrupt documents. Users accidentally delete data. Hackers and disgruntled employees erase disks. Hardware problems and natural disasters take out machine rooms.

If executed correctly, backups allow an administrator to restore a filesystem (or any portion of a filesystem) to the condition it was in at the time of the last backup. Backups must be done carefully and on a strict schedule. The backup system and backup media must also be tested regularly to verify that they are working.

The integrity of your backup procedure directly affects your company's bottom line. Senior management needs to understand what the backups are actually capable of doing, as opposed to what they want the backups to do. It may be OK to lose a day's work at a university computer science department, but it probably isn't OK at a commodity trading firm.

## Label your media

 begin this chapter with some general backup philosophy, followed by a discussion of the most commonly used backup devices and media (their strengths, weaknesses, and costs). Next, we talk about how to design a backup scheme and review the mechanics of the popular dump and restore utilities.

We then discuss some additional backup and archiving commands and suggest which commands are best for which situations. Finally, we take a look at Bacula, a free network backup package, and offer some comments about other open source and commercial alternatives.

## 10.1 MOTHERHOOD AND APPLE PIE

Before we get into the meat and potatoes of backups, we want to pass on some general hints that we have learned over time (usually, the hard way). None of these suggestions is an absolute rule, but you will find that the more of you follow, the smoother your backups and restores will go.

## Perform all backups from a central location

Many backup utilities allow you to perform dumps over the network. Although there is some performance penalty for dumping that, the ease of administration makes it worthwhile. If you manage only a handful of servers, its probably easier to run a script from a central location that executes dump (by ssh) on each machine that needs to be dumped. If you have more than a few servers, you should use a software package (commercial or free) to automate this process.

Even if your backups are too large to be funneled through a single server, you should still try to keep your system as centralized as possible. Centralization facilitates administration and lets you restore data to alternate servers. Depending on the media you are using, you can put more than one media device on server without affecting performance.
