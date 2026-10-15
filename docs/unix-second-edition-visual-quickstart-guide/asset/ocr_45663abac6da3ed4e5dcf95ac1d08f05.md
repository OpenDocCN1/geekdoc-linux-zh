# Making Backups with rsync

The rsync utility is a fancy way to synchronize files and directories, either locally or across a network. We like to use it to make backups so we don’t have to worry when we mess something up. Yes, we could use cp or something equally boring, but we like the speed and flexibility of rsync. In this example, we’re copying files locally, but we could as easily be making remote backups to another server somewhere else.

# To make backups with rsync:

+   1. mkdir ~/ .BACKUPDIR
+   Create a directory to house your backups. Ideally, you’ll create the directory on a different physical disk from the stuff you’re backing up, but do what you can. We’re creating a backup directory that’s a subdirectory of the home directory, which will help protect us against self-inflicted damages but not against a disk failure. (We trust the system administrator for protecting against disk failures...er, Eric, you are up-to-date on our backups, aren’t you?)

+   2. rsync -v -a /home/jdoe/data ~/ .BACKUPDIR
+   Specify the rsync command, the -v (for verbose) and -a (for archive) options, and the source and destination directories (Code Listing 17.8).
+   Wait while it does the initial backup (showing you each file as it gets copied). The first backup takes awhile but no longer than using cp would.

```
[jdoe@frazZ bin]$ rsync -v -a /home/jdoe/data ~/ .BACKUPDIR
building file list ... done
data/
data/#scratch#
data/#ll. programs#
data/#local. programs. txt#
data/*scratch*
data/1
data/2
data/Mail/
data/News/
data/Project/
data/Project/keep
data/Project/keeper.jpg
data/Project/kept
data/Project/kidder.txt
data/Project/kiddo
data/Project/kidnews
data/Project/kidneypie
data/Project/kids
data/Project/kidupdate
data/address. book
data/address. book~
data/all. programs
data/b
data/backup-files/
data/backup-files/.Xauthority
data/backup-files/.bash_history
data/backup-files/.bash_logout
data/backup-files/.bash_profile
data/backup-files/.bashrc
data/backup-files/.mailcap
data/backup-files/.screenrc
data/backup-files/.ssh/
...
wrote 24841142 bytes  read 14708 bytes
-> 741965.67 bytes/sec
total size is 24779055  speedup is 1.00
[jdoe@frazZ bin]$ 
[jdoe@frazZ jdoe]$ rsync -v -a /home/jdoe/data ~/ .BACKUPDIR
building file list ... done
data/newer. programs.txt
wrote 30149 bytes  read 36 bytes  20123.33 -> bytes/sec
total size is 24765461  speedup is 820.46
[jdoe@frazZ jdoe]$
```

Code Listing 17.8 The rsync utility is a handy tool for making backups. Note that it takes much less time for all updates after the first one.