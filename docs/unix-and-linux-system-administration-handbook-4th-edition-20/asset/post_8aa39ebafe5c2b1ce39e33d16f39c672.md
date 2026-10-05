
# Setting up a backup regime with dump

From a safety and convenience perspective, this schedule is the ideal. Don't stray from it without a specific reason (e.g., conserve tapes or labor).

## A moderate schedule

A reasonable schedule for most sites is to assign a tape to each day of the week, each week of the month (you'll need 5), and each month of the year. Every day, do a level 9 dump to the daily tape. Every week, do a level 5 dump to the weekly tape. And every month, do a level 3 dump to the monthly tape. Do a level 0 when incrementals get too big to fit on one tape, which is most likely to happen on a monthly tape. Do a level 0 dump at least once a year.

The choice of levels 3, 5, and 9 is arbitrary. You could use levels 1, 2, and 3 with same effect. However, the gaps between dump levels give you some breathing room if you later decide to add another level of dumps. Other backup software uses the terms full, differential, and incremental rather than numeric dump levels.

This schedule requires 24 tapes plus however many tapes are needed for the level 0 dumps. Although it does not require too many tapes, it also does not afford m redundancy.

## 10.4 SETTING UP A BACKUP REGIME WITH DUMP

The dump and restore commands are the most common ways to create and restore from backups. These programs have been around for a very long time, and the behavior is well known. At most sites, dump and restore are the underlying commands used by automated backup software.

You may have to explicitly install dump and restore on your Linux systems, depending on the options you selected during the original installation. A package is available for easy installation on all except distributions. The current Red Hat offers a system administration package at installation time that dumps.

On Solaris systems, dump and restore are called ufsdump and ufsrestore. As the names say, the ufs-dump command exists, but it's not backup-related. commands work only with the order UFS filesystems; they do not work on ZFS filesystems; see page 316 for a discussion of ZFS backup options.

ufsdump accepts all the flags and arguments as other systems' traditional dump, but it parses them differently. ufsdump expects all the flags to be contained in the first argument and the flags' arguments to follow in order. For example, where most commands would want -a 5 -b -c 10, on Solaris ufsdump want -abc 5 10.

ufsdump is only supposed to be used on unmounted filesystems. If you need to back up a level filesystem, be sure to run Solaris's fssnap command and then run ufsump against the snapshot.

![](img/579efec8c67772f31ecf34844bbb71a2_355_0.png)

For AIX, the dump command is called backup, although restore is still called restore. A dump command exists, but it's not backup-related.

For simplicity, we refer to the backup commands as dump and restore and show their traditional command-line flags. Even on systems that call the commands something else, they function similarly. Given the importance of reliable dumps, however, you must check these flags against the man pages on the machine you are dumping; most vendors have tampered with the meaning of at least one flag.

## Dumping filesystems

dump builds a list of files that have been modified since a previous dump, then packs those files into a single large file to archive to an external device. dump has several advantages over most of the other utilities described in this chapter.

- Backups can span multiple tapes.
- Files of any type (even devices) can be backed up and restored.
- Permissions, ownerships, and modification times are restored.
- Files with holes are handled correctly.
- Backups can be performed incrementally (when only modified files are written out to tape).

The GNU version of tar on Linux provides all these features as well. However, dump's handling of incremental backups is a bit more sophisticated than tar's. You may find the extra horsepower useful if your needs are complex.

Unfortunately, the version of tar shipped with most UNIX distributions lacks many of GNU features. If you must support backups for both Linux and UNIX variants, dump is your best choice. It is the only command that handles these issues (fairly) consistently across platforms, so if you are lucky to be in a completely homogeneous Linux environment, pick your favorite. dump is less filling, but tar tastes great!

On Linux systems, dump supports filesystems in the ext family. You may have to download and install other versions of dump to support other filesystems.

The dump command understands the layout of raw filesystems, and it reads a filesystem inode table directly to decide which files must be backed up. The knowledge of filesystem makes dump very efficient, but it also imposes a couple of limitations.

The first limitation is that every filesystem must be dumped individually. The other limitation is that only filesystems on the local machine can be dumped; the you

- 6. Holes are blocks that have never contained data. If you open a file, write one byte, seek 1MB into the file, then write another byte, the resulting "sparse" file takes up two disk blocks though its logical size is much bigger. Files created by Berkeley DB or ndbm contain many holes.
- 7. dump requires access to raw partitions. Anyone allowed to dumps can read all the files on the system with a little effort.
- 8. Legacy systems may use separate device number.
- 9. All the entries use the major device number.

## Chapter 10 Backups

In the past, you had to tell dump exactly how your tapes were. Modern tape drives can tell when they reached the end of tape. Since the variability of compression makes the tape length indeterminate, it is best to rely on end-of-tape (EOT). All versions of dump understand the -d and -s options, which specify the tape density in bytes per inch and the tape length in feet, respectively. A few more versions let you specify sizes in kilobytes with the -B option.

For example, let suppose we want to dump to a DAT drive whose native capacity is 20GB (with compressed capacity of 40GB). DAT drives recover EOT, so we need to lie to dump and set the tape size to much bigger than 40GB, say 50GB. That works out to 60,000 feet, 6,250 bpi:

```
# dump -5u -s 60000 -d 6250 /dev/nst0/work
DUMP: Date of level 5 dump: Wed Nov 18 14:28:05 2009
DUMP: Date of last level 0 dump: Sun Nov 15 21:11:05 2009
DUMP: Dumping /dev/hda2 (/work) to /dev/nst0
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 1875003 tape blocks on .23 tape(s)
```

The flags -5u are followed by the parameters -s (size: 60,000 feet), -d (density: 6,250 bpi), and -f (tape device: /dev/nst0). Finally, the filesystem name (/work) is given; this argument is required. Most versions of dump allow you to specify the filesystem by its mount point, as in the example above. Some require you to specify your raw device file.

The last line of output above verifies that dump will not attempt to switch tapes on its own initiative, since it believes that only a quarter of tape is needed for this dump. It is fine if the number of estimated tapes is more than 1, as long as the specified tape size is larger than the actual tape size. dump will reach the actual EOT before it reaches its computed limit.

# Restoring from dumps with restore

The program that extracts data from dump is called restore. We first discuss restoring individual files (or a small set of files), then explain how to restore entire filesystems.

Normally, the restore command is dynamically linked, so you need the system's shared libraries available to do anything useful. Building a statically linked version of restore takes some extra effort but makes it easier to recover from a disaster because restore is completely self-contained.
