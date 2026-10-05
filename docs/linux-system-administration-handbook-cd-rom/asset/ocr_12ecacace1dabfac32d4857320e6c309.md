# 278

# Chapter 20 • Backing Up Your Data

With the new proposed standards for CD-ROM- (and thus WORM-) based filesystems this media will soon sport multiple gigabyte capacity. Though they will still be write-once, the easier access (random instead of sequential) will likely make them popolar once their price drops into the affordable range. In actuality, the technology for this has existed for some time, the popularity of the current standard has kept it from being replaced. But the need to store large amounts of data reliably has grown tremendously in recent years, and CD-ROMs are a big win over tape in both ease of access and longevity (decades versus years).

The rest of this chapter assumes you have some form of large capacity media on which to backup your data, though many of the guidelines are regardless of the media being used or its capacity.

In general, you will want to run your backup during times of low activity for two reasons. it’s not a good idea to have lots of files open or changing while the backup is running. Some programs will lock a file and the backup will, at best, be able to skip it or, at worst, the backup will exit or crash. Second, backing up your system will tend to consume a lot of system resources, and if your server is fairly loaded already, it will likely be bogged down considerably if you try to run the backup during “normal” business hours (whatever might be).

# 20.1 tar and mt

tar, as you may know, stands for Tape Archive. Before the most recent versions of GNU, tar was not really suitable for use as a backup tool. It had no way of performing incremental backups and properly handling files with holes (so-called sparse files).

At the base level, you can create a cron job that will compress all of your filesystems and network volumes to a tape drive every night or every few nights. There are a couple of drawbacks to this method.

Typically only a small fraction of the filesystem changes over the course of even a week. Making a copy of the whole filesystem every other night might kill. It would be better if incremental backups could be made.

It’s very possible that you could have more stuff than you have capacity on your particular combination of tape and drive. In this case you would have to break up the backup and change tapes at some point to complete the backup. Once again, incremental backups would alleviate this.

If your backup, or sections thereof, is small enough, you may want to put more than one on a single tape and you may need some way to access a par