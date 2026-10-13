> You can use the z option to tell tar to gzip "on-the-fly"; the output will be compressed after the tar step, and you won't have to use gzip to compress it. Compressed tarfiles usually have extensions of .tar.gz or .tgz.
> 
> # tar cvfz /usr/backup/usr.local.tgz /usr/local

You can then copy this file (usr.local.tar.gz or usr.local.tgz) to a removable disk, another hard disk, or an NFS share—anything you like.

It might be helpful to keep the compressed tarfile around and not delete it after you've copied it to another medium; you can update changed files in it instead of deleting and re-creating it each time you make a backup, using the r (or replace) option:

```
# tar rvfz /usr/backup/usr.local.tgz /usr/local
```

Finally, you can find out what's in a tarfile using the t (or table of contents) option:

```
# tar tfz /usr/backup/usr.local.tgz
```

> Using tar to create files is all well and good, but the program is really designed primarily for interacting with tape drives. However, with today's respective prices of tape drives, digital tapes, optical drives, and CD media, it's much more cost-effective to use tarfiles and CD-R (or even DVD) backups instead of tapes, and much more likely that you will have the necessary equipment. The media is less fragile, too.

# Using burncd

If you have an ATAPI (IDE) CD-R or CD-RW drive, you will want to use the burned program, which is part of the base FreeBSD system, to write your CDs. (Most optical drives sold today are ATAPI. If you have a SCSI drive, you will instead need to use cdrecord, found in the ports at /usr/ports/sysutils/cdtools.) This tool is pretty simple to use, although it does involve a two-step process.

The first thing you must do is create an ISO disk image file, which is a bitwise copy of the data that will be written to the disc. You will need to install mkisofs in order to do this; it's in /usr/ports/sysutils/mkisofs (see Hour 7 for more on installing software from the ports or packages).