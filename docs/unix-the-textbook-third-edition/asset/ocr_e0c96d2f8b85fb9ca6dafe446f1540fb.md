```
$find . -newer level.0.cpio.timestamp -print \ | cpio -oacvB > device
...
$
```

# 23.6.3.2 rsync

As introduced in Chapter 16, the rsync command is a very space-efficient way to backup files and directories, particularly from one machine to another using ssh across a network. Its operation can also be automated by designing and implementing an appropriate entry in the crontab file. The general syntax of rsync for local or remote copying is

Local:

```
rsync [option(s)...] src... [dest]
```

Remote:

Pull(copying to a remote location): rsync [option(s)...] [user@] host:src... [dest]

Push(copying from a remote location): rsync [option(s)...] src... [user@]host:dest

where option(s) are the valid options for the rsync command, src is the source file or directory, and dest is the destination path.

An example of using rsync to copy a file named rsynctest from the current working directory to the local destination /usr/home/bob/USBint is

```
$ rsync -av rsynctest /usr/home/bob/USBint
sending incremental file list
rsynctest
sent 192 bytes received 35 bytes 454.00 bytes/sec
total size is 92 speedup is 0.41
$
```

An example of using rsync to copy an entire directory named syncdir locally is

```
$ rsync -av syncdir /usr/home/bob/USBint
sending incremental file list
syncdir/
syncdir/Chap16.doc
syncdir/backup1.py
syncdir/ossystem.py
sent 280,176 bytes received 77 bytes 186,835.33 bytes/sec
total size is 279,855 speedup is 1.00
0
$
```