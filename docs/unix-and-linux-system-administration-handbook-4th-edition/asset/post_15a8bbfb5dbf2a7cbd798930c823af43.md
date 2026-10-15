
When you are notified of a lost file, first determine which tapes contain versions of the file. Users often want the most recent version, but that is not always the case. For example, a user who loses a file by inadvertently copying another file on top of it would want the version that existed before the incident occurred. It’s helpful if you can browbeat users into telling you not only what files are missing but also when they were lost and when they were last modified. We find it helpful to structure users’ responses with a request form.

If you do not keep on-line catalogs, you must mount tapes and repeatedly attempt to restore the missing files until you find the correct tape. If the user remembers when the files were last changed, you may be able to make an educated guess about which tapes the files might be on.

After determining which tapes you want to extract from, create and cd to a temporary directory such as /var/restore where a large directory hierarchy can be created; most versions of restore must create all the directories leading to a particular file before that file can be restored. Do not use /tmp—your work could be wiped out if the machine crashes and reboots before the restored data has been moved to its original location.

The restore command has many options. Most useful are -i for interactive restores of individual files and directories and -r for a complete restore of an entire filesystem. You might also need -x, which requests a noninteractive restore of specified files—be careful not to overwrite existing files.

restore -i reads the table of contents from the tape and then lets you navigate through it as you would a normal directory tree, using commands called ls, cd, and pwd. You mark the files that you want to restore with the add command. When you finish selecting, type extract to pull the files off the tape.

> See page 317 for a description of mt.

If you placed multiple dumps on a single tape, you must use the mt command to position the tape at the correct dump file before running restore. Remember to use the non-rewinding device!

For example, to restore the file /users/janet/iamlost from a remote tape drive, you might issue the following commands. Let’s assume that you have found the right tape, mounted it on tapehost:/dev/nst0, and determined that the filesystem containing janet’s home directory is the fourth one on the tape.

```
$ sudo mkdir /var/restore
$ cd /var/restore
$ sudo ssh tapehost mt -f /dev/nst0 fsf 3
$ sudo restore -i -f tapehost:/dev/nst0
restore> ls
..
janet/ garth/ lost+found/ lynda/
restore> cd janet
restore> ls
afile bfile cfile iamlost
```

```
restore> add iamlost
restore> ls
* afile bfile cfile iamlost*
restore> extract
You have not read any volumes yet.
Unless you know which volume your files are on you should
start with the last volume and work towards the first.
Specify next volume #: 1
set owner/mode for '?' [yn] n
```

Volumes (tapes) are enumerated starting at 1, not 0, so for a dump that fits on a single tape, you specify 1. When restore asks if you want to set the owner and mode, it's asking whether it should set the current directory to match the root of the tape. Unless you are restoring an entire filesystem, you probably do not want to do this.

Once the restore has completed, give the file to janet:

```
$ cd /var/restore
$ ls janet
iamlost
$ ls ~janet
afile bfile cfile
$ sudo cp -p janet/iamlost ~/janet/iamlost.restored
$ sudo chown janet -j janet/iamlost.restored
$ sudo chgrp staff -j janet/iamlost.restored
$ cd /
$ sudo rm -rf /var/restore
$ mail janet
Your file iamlost has been restored as requested and has
been placed in /users/janet/iamlost.restored.

Your name, Humble System Administrator
```

Some administrators prefer to restore files into a special directory and allow users to copy their files out by hand. In that scheme, the administrator must protect the privacy of the restored files by verifying their ownership and permissions. If you choose to use such a system, remember to clean out the directory every so often.

If you originally wrote a backup to a remote tape drive and are unable to restore files from it locally, try hosting the tape on the same remote host that was used for the original backup.

restore -i is usually the easiest way to restore a few files or directories from a dump. However, it does not work if the tape device cannot be moved backwards a record at a time (a problem with some 8mm drives). If restore -i fails, try restore -x before jumping out the window. restore -x requires you to specify the complete path of the file you want to restore (relative to the root of the dump) on the command line. The following sequence of commands repeats the previous example, but with -x.
