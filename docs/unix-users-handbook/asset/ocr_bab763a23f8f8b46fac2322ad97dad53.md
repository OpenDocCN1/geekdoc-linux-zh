# Command and Path Completion

**ksh** sometimes knows what you're thinking. You can type part of a command or pathname and **ksh** can complete the remainder for you. You can type part of a command or pathname and press *escape* key to complete the command. If, for instance, you wish to issue the **uname** command to view the current system run level but can't remember the full command, you can type "un" and *escape* followed by the "=" key and the command is completed for you. In the following example, we'll change to the /sbin directory, list its contents, and then type **unescape**:

```
marty p $ cd /sbin
marty p $ ls -al
total 11704
drwxrwxr-x  2 root    sys

     512 Nov 27 14:55 .
drwxr-xr-x 31 root    root

 1024 Apr 19 03:24 ..
-r-x-r-xr-x  1 bin     bin

200356 Sep 1   1998 autopush
lrwxrwxrwx  1 root    root

  21 Nov 27 14:55 dpgetfile -> ../usr/sbin/e
dpgetagent
-r-xr-xr-x  1 bin     bin

 470436 Sep 1   1998 dp
getagent
-r-x-r-xr-x  1 bin     bin

433064 Sep 1   1998 dp
pinfop
-r-x-r-xr-x  1 bin     bin

253664 Sep 1   1998 fdisk
-r-x-r-xr-x  1 bin     bin

 762816 Sep 1   1998 host
config
-r-x-r-xr-x  1 bin     bin

535900 Sep 1   1998 icon
fig
-r-x-r-xr-x  1 root    sys

516484 Sep 1   1998 init
-r-xr-xr-x  2 bin     root

257444 Sep 1   1998 jsh
-r-xr-xr-x  1 bin     bin

224596 Sep 1   1998 mount
-r-xr-xr-x  1 root    sys

  6935 Jan 1   1970 mountall
drwxr-xr-x  3 root    sys

  2689 Jan 1   1970 rc0
-rwxr-xr-x  1 root    sys

 2905 Jan 1   1970 rcl
-rwxr-xr-x  1 root    sys

 2491 Jan 1   1970 rc2
-rwxr-xr-x  1 root    sys

 1948 Jan 1   1970 rc3
-rwxr-xr-x  3 root    sys

 2689 Jan 1   1970 rc5
-rwxr-xr-x  3 root    sys

 2689 Jan 1   1970 rc6
-rwxr-xr-x  1 root    sys

  9412 Jan 1   1970 rcs
-r-xr-xr-x  2 bin     root

257444 Sep 1   1998 sh
-r-xr-xr-x  1 bin     bin

195300 Sep 1   1998 soconfig
lrwxrwxrwx  1 root    root

 13 Nov 27 14:40 su -> ../usr/bin/su
-r-x-r-xr-x  1 root    sys

473808 Sep 1   1998 su.static
-r-xr-xr-x  1 root    bin

288544 Sep 1   1998 sulogin
-rwxr-xr-x  1 root    sys

 3138 Jan 1   1970 swapadd
-r-xr-xr-x  1 bin     bin

29736 Sep 1   1998 sync
-r-xr-xr-x  1 root    sys

435004 Sep 1   1998 uadmin
-r-xr-xr-x  1 bin     bin

213408 Sep 1   1998 umount
-r-xr-xr-x  1 root    sys

 3292 Jan 1   1970 umountall
-r-xr-xr-x  1 bin     bin

193152 Sep 1   1998 uname
marty p $ un ; ; typed unescape=
1) uname
marty p $ un
```

![](bbox=[0.8, 0.08, 0.95, 0.18])

**ksh** determined that the only command that starts with "un" is **uname**. The **uname** command was listed and *un* was again put at the command prompt for me. You can't see the *escape*= I typed after the first "un," so I made a comment to the side showing the full command.

![](bbox=[0.8, 0.3, 0.95, 0.4])