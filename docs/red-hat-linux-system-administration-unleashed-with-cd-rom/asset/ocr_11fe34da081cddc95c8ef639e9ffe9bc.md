# Configuring dump to Accept Installation as Level-0

To configure the program dump to do this, you basically have two choices.

As soon as the system is configured, execute the command

```
/sbin/dump -0u -f /dev/null -B 8192000 /
```

in order to create the entry in /etc/dumpdates that declares now as being the time of the last level-0 dump. (This is referred to as the epoch—the beginning of time.) This basically says to dump, "Create a level-0 backup (-0u) on device /dev/null (-f /dev/null) (which throws away the resulting files away) of my entire 8-gigabyte hard drive (-B 8192000), starting at the root (/)."

If the system has been running for any length of time, you probably will have to avail yourself of the second choice, which is to manually edit the file /etc/dumpdates to reflect the time of installation. See the section "Developing Backup Scripts" later in the chapter for a hint or two on how to retroactively figure out when the date of installation was, if you don't remember. A line in /etc/dumpdates that looks like this:

```
/dev/hda2 0 Sat Jul 31 20:31:16 1999
```

creates an initial state for the dump program to start from. Subsequent incremental dumps add their information to the /etc/dumpdates file like this (I show a level-1, done immediately after users were added to the system):

```
/dev/hda2 1 Sat Jul 31 20:47:01 1999
```

and the program will never know that a real dump has never been done. Yes, we just lied to the computer, but don't worry about it. Real system administrators do that all the time in order to get things done. Real operating systems will let you lie to them, but you had better have a very good reason, and be right!

Immediately after the users have been added, Internet connectivity established, email and Web clients configured, and everything works to your satisfaction, everything that has been changed from the basic installation is backed up with a level-1 backup. To recover from a major disaster, install the operating system, then restore this level-1 backup, and you are back online. Add in the latest periodic level 2-9 incremental backups and you can be as current as you want to be, without needing to store hundreds (or possibly thousands) of megabytes of data.

Using this backup strategy allows me to use my old 40-megabytes-per-tape floppy-drive-controller-based tape drive to back up my 8-gigabyte Red Hat Linux hard drive with just a little ingenuity on my part. Actually, it allows me to back up all of my home network's machines on a regular basis with a minimum of hassle. Some of my