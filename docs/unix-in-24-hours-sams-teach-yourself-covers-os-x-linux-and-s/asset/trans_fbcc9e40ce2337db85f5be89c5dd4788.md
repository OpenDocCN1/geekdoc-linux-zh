

```
$ unzip -l /tmp/archive.zip
Archive:  /tmp/archive.zip
    Length      Date        Time    Name
---------  ----------  -----   ----
        0  10-27-2014  10:00   Desktop/
        0  10-27-2014  10:00   Documents/
        0  10-27-2014  10:00   Downloads/
        0  10-27-2014  10:00   Public/
      458  03-16-2015  07:42   cmdcnt.sh
      252  03-16-2015  08:02   diskspace.sh
      440  03-16-2015  08:28   hi-low.sh
        0  12-28-2014  11:42   test/
        0  01-29-2015  12:35   testme
---------                     -------
     1150                        9 files
```

```
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
$ compress backup.tar
$ ls -l backup.tar
ls: backup.tar: No such file or directory
```

```
$ ls -l backup.tar.Z
-rw-r--r--  1 taylor wheel 7807489 Feb  8 02:58 backup.tar.Z
```

```
$ uncompress backup.tar.Z
$ ls -l backup.tar
-rw-r--r--  1 taylor  wheel  15800320 Feb  8 02:58 backup.tar
```

```
$ uncompress -v backup.tar.Z
backup.tar.Z:  202.3% OK
```

```
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
$ zip backup.tar.zip backup.tar
    adding: backup.tar (deflated 67%)
$ ls -l backup.tar.Z
ls: backup.tar.Z: No such file or directory
```

```
$ ls -l backup.tar.zip
-rw-r--r-- 1 taylor wheel 5214105 Feb  8 02:58 backup.tar.zip
$
```

```
$ unzip backup.tar.zip
Archive:  backup.tar.zip
replace backup.tar? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
    inflating: backup.tar
$
```

```
$ find . -name "*.c" -print | cpio -oO sourcefiles.cpio
$
```

```
$ cp io -itI sourcefiles.cpio
./bin/fixit.c
./Src/Embot/embot.c
./Src/Embot/error.c
./Src/Embot/interact.c
./Src/Embot/log.c
./Src/Embot/mail_utils.c
./Src/Embot/savemsg.c
./Src/Embot/sendfile.c
./Src/Embot/utils.c
./Src/Misc/usage_summary.c
./Src/Misc/fixit.c
./Src/Misc/info.c
./Src/Misc/isnew.c
./Src/Misc/mydate.c
./Src/Misc/showmatches.c
./Src/Misc/change.c
./Src/change.c
./Src/cleanup.c
./Src/cribbage.c
./Src/expandurl.c
```

```
./Src/extract-mall.c
./Src/futuredate.c
./Src/import.c
./Src/assemble.c
./Src/make-html.c
./Src/old-import.c
./Src/process-data.c
./Src/showmatches.c
./Src/sum-up.c
./Src/text-counter.c
./Src/login.c
./Src/calc.c
$
```

```
$ cpio -i cribbage < sourcefile.cpio
cpio: WARNING! These patterns were not matched:
cribbage
$
```

```
$ cpio -i '*cribbage*' < *cpio
cpio: Unable to create ./Src/cribbage.c <No such file or directory>
$
```

```
$ cpio -ivd '*cribbage*' < *cpio
./Src/cribbage.c
30 blocks
$
```

```
snapdir="$HOME/Snapshots"
thedate="$(date +%m.%d.%Y.%H:%M)"
outfile="$snapdir/snapshot.$thedate.tar.gz"
```

/home/taylor/Snapshots/snapshot.12.08.2015.14:40.tar.gz

```
$ cat snapshot.sh
#!/bin/bash

snapdir="$HOME/Snapshots"
thedate="$(date +%m.%d.%Y.%H:%M)"
outfile="$snapdir/snapshot.$thedate.tar.gz"

if [ $# -gt 0 ] ; then
    dirs=$1
else
    dirs="."
fi

echo "Backing up $dirs to $outfile"

tar -czf $outfile $dirs

echo "done."

exit 0
$
```

```
$ alias snapshot="$HOME/bin/snapshot.sh"
$ snapshot
Backing up . to /home/taylor/Snapshots/snapshot.11.08.2015.14:50.tar
done.
$
```

```
find $HOME -cnewer $HOME/.marker -print | cpio -o /dev/rst0
touch $HOME/.marker
```

$ mailx
mailx version 5.0. Type ? for help.
/var/mail/taylor": 9 messages 5 new
 1 disserli Mon Nov 22 19:40 54/2749 "Re: Are you out there"
>N 2 Laura.Ramsey Tue Nov 30 16:47 46/1705 "I've got an idea..."
 N 3 ljw Fri Dec 3 22:57 130/2712 "Re: Attachments"
 N 4 sartin Sun Dec 5 15:15 15/341 "I need your address"
 N 5 rustle Tue Dec 7 15:43 29/955 "flash cards"
 6 harrism Tue Dec 7 16:13 58/2756 "Re: Writing Lab OWL proj"
 7 CBUTCHER Tue Dec 7 17:00 19/575 "Smartphone Based GRE's"
 8 harrism Tue Dec 7 21:46 210/10636 "writing environments"
 N 9 v892127 Wed Dec 8 07:09 38/1558 "Re: Have you picked up"
& _

