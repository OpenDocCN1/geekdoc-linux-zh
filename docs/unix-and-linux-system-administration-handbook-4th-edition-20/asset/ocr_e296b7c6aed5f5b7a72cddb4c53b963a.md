# Setting up a backup regime with dump

From a safety and convenience perspective, this schedule is the ideal. Don't stray
from it without a specific reason (e.g., conserve tapes or labor).

# A moderate schedule

A reasonable schedule for most sites is to assign a tape to each day of the
week, each week of the month (you'll need 5), and each month of the year. Every\day, do a level 9 dump to the daily tape. Every week, do a level 5 dump to the
weekly tape. And every month, do a level 3 dump to the monthly tape. Do a level
0 when incrementals get too big to fit on one tape, which is most
likely to happen on a monthly tape. Do a level 0 dump at least once a year.

The choice of levels 3, 5, and 9 is arbitrary. You could use levels 1, 2, and 3 with
same effect. However, the gaps between dump levels give you some breathing
room if you later decide to add another level of dumps. Other backup
software uses the terms full, differential, and incremental rather than numeric
dump levels.

This schedule requires 24 tapes plus however many tapes are needed for the level\0 dumps. Although it does not require too many tapes, it also does not afford
m redundancy.

# 10.4 SETTING UP A BACKUP REGIME WITH DUMP

The dump and restore commands are the most common ways to create and re-
from backups. These programs have been around for a very long time, and
the behavior is well known. At most sites, dump and restore are the underlying
commands used by automated backup software.

You may have to explicitly install dump and restore on your Linux systems, de-
pending on the options you selected during the original installation. A package is
av for easy installation on all except distributions. The current Red
Hat offers a system administration package at installation time that-
umps.

On Solaris systems, dump and restore are called ufsdump and ufsrestore. As the names say, the ufs*\dump command exists, but it's not backup-related. commands work only with the order UFS filesystems; they do not work on ZFS
filesystems; see page 316 for a discussion of ZFS backup options.

ufsdump accepts all the flags and arguments as other systems' traditional
dump, but it parses them differently. ufsdump expects all the flags to be
contained in the first argument and the flags' arguments to follow in order. For
example, where most commands would want -a 5 -b -c 10, on Solaris ufsdump
want abc 5 10.

ufsdump is only supposed to be used on unmounted filesystems. If you need
back up a level filesystem, be sure to run Solaris's fssnap command and then run
ufsdump against the snapshot.

![](bbox=[0.145, 0.595, 0.235, 0.645])