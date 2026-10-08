Now that we’ve seen how to get the last of the words to appear on the command line with `escape_`, how about the third word of the last command? You can specify the third word by typing `escape3_` or substitute for the "3" for any of the words on the last command line. The following example shows listing the third word of the last command:

![](bbox=[0.03, 0.23, 0.13, 0.32])

```
martyP $ ls -al
 total 11704
drwxrwxr-x 2 root sys 512 Nov 27 14:55.
drwxr-xr-x 31 root root 1024 Apr 19 03:24 ..
-rw-r-xr-x 1 bin bin 200356 Sep 1 1998 autopsuh
lrwxrwxrwx 1 root root 21 Nov 27 14:55 bpgetfile - > ../usr/sbin/e
-r-xr-xr-x 1 bin bin 470436 Sep 1 1998 chcapng
-r-xr-xr-x 1 bin bin 433064 Sep 1 1998 dhcpinfo
-rwxr-xr-x 1 bin bin 255362 Sep 1 1998 fdisk
-r-xr-xr-x 1 bin bin 762816 Sep 1 1998 hconfig
-r-xr-xr-x 1 bin bin 535900 Sep 1 1998 iconfig
-r-xr-xr-x 1 bin bin 516484 Sep 1 1998 init
drwxr-xr-x 2 bin root 257444 Sep 1 1998 jsh
-r-xr-xr-x 1 bin bin 224596 Sep 1 1998 mount
-r-xr-xr-x 1 root sys 6935 Jan 1 1970 mountall
-rwxr-xr-x 3 root sys 2689 Jan 1 1970 rc0
-rwxr-xr-x 3 root sys 2905 Jan 1 1970 rc1
drwxr-xr-x 1 root sys 2491 Jan 1 1970 rc2
drwxr-xr-x 1 root sys 1948 Jan 1 1970 rc3
drwxr-xr-x 3 root sys 2689 Jan 1 1970 rc5
drwxr-xr-x 3 root sys 2689 Jan 1 1970 rc6
lrwxr-xr-x 1 root sys 9412 Jan 1 1970 rcS
drwxr-xr-x 2 bin root 257444 Sep 1 1998 sh
-r-xr-xr-x 1 bin bin 195300 Sep 1 1998 soconfig
lrwxrwxrwx 1 root root 13 Nov 27 14:40 su - > ../usr/bin/su
-r-xr-xr-x 1 root sys 473808 Sep 1 1998 su.static
drwxr-xr-x 1 root bin 288544 Jan 1 1998 sulogin
drwxr-xr-x 1 root sys 3138 Jan 1 1970 swappd
drwxr-xr-x 1 root sys 29736 Jan 1 1998 sync
drwxr-xr-x 1 root sys 435004 Sep 1 1998 yadmin
drwxr-xr-x 1 root sys 213408 Sep 1 1998 udomin
drwxr-xr-x 1 root sys 3292 Jan 1 1970 umountall
drwxr-xr-x 1 root sys 193152 Sep 1 1998 uname
martyP $ ls r ; typed ls rescape=
1) rc0
2) rc1
3) rc2
4) rc3
5) rc5
6) rc6
7) rcS
martyP $ ls rc0 rc1 rc2 rc3 rc5 rc6 rcS ; typed escape* to get seven files
rc0 rc1 rc2 rc3 rc5 rc6 rcS
martyP $ ls rc1 ; typed lsecape3_ to get third word
```

Because the previous command included the `ls` command, the third word is not `rc2` but `rc1`, because `ls` was the first entry in the previous command.