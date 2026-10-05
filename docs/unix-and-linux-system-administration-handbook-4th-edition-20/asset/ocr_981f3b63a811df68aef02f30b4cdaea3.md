# Chapter 10 Backups

```
restore> add iamlast
restore> ls -l
afile bfile cfile iamlast*
restore> extract
```

You have not read any volumes yet.
Unless you know which volume your files are on you
start with the last volume and work towards the first.
Specify volume # 1
set owner/mode for '?' [yn] n

Volumes (tapes) are enumerated starting at 1, not 0, so for a dump that on
single tape, you specify 1. When restore asks if you want to set the owner and
mode, it is asking whether it should set the current directory to the root of
the tape. If you are restoring an entire filesystem, you probably do not
to this.

Once the restore has completed, give the file to janet:

```
$ cd /var/restore
$ ls jane\iamlast
$ ls -jane
afile bfile
$ sudo cp -p jane/iamlast -jane/iamlast.restored
$ sudo chown staff -jane/iamlast.restored
$ sudo chgrp staff -jane/iamlast.restored
$ cd / sudo rm -rf /var/restore
$ mail jane
```

Your file iamlast has been restored as requested and has
placed in /users/jane/iamlast.restored.

Your name, Humble System Administrator

Some administrators prefer to restore files into a special directory and allow users
to copy their files out by hand. In that scheme, the administrator must protect the
priv of the restored files by verifying their ownership and permissions. If you
choose to use such a system, remember to clean out the directory so often.

If you originally wrote a backup to a remote tape drive and are unable to restore
files from locally, however trying to host it on the same remote host that was used for
the original backup.

restore -i is usually the easiest way to restore a few files or directories from a
dump, it does not work if the tape device cannot be moved backwards a
record at a time (a problem with some 8mm drives). If restore -i fails, try restore
-x before jumping out the window. restore -x requires you to specify the complete
path of the file you want to restore (relative to the root of the dump) on the com-\mand line. The following sequence of commands repeats the previous example,
with -x.

The next to -x iamlast indicates that it has been marked for extraction.