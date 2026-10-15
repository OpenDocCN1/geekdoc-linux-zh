

```text
% ls -l /
-rw-r--r--   1 root       61440 Nov 29  1991 boot
drwxr-xr-x   4 root       23552 Sep 27 11:31 dev
drwxr-xr-x   6 root        3072 Oct 11 16:30 etc
drwxr-xr-x   2 root        8192 Apr 12  1991 lost+found
lrwxr-xr-x   1 root           7 Jul 28  1988 sys -> usr/sys
drwxrwxrwx  65 root       12800 Oct 11 17:33 tmp
drwxr-xr-x 753 root       14848 Oct  5 10:07 usera
drwxr-xr-x 317 root       13312 Oct  5 10:17 userb
drwxr-xr-x 626 root       13312 Oct  8 13:02 userc
drwxr-xr-x 534 root       10752 Sep 30 13:06 users
drwxr-xr-x  34 root        1024 Oct  1 09:10 usr
drwxr-xr-x   5 root        1024 Oct  1 09:20 var
```

```text
lrwxr-xr-x 1 root 7 Jul 28 1988 sys -> usr/sys
```

```text
% chmod g+w test
% ls -l test
-rw-rw-r--  1 taylor      0 Oct 11 18:29 test
```

```text
% chmod g+x test
% ls -l test
-rw-rwxr--  1 taylor      0 Oct 11 18:29 test
```

```text
% chmod o-r test
% chmod g-rwx test
% ls -l test
-rw------  1 taylor           0 Oct 11 18:29 test
```

```text
% chmod a+r test
% ls -l test
-rw-r--r--  1 taylor      0 Oct 11 18:29 test
```

```text
drwx------  2 taylor        512 Sep 30 10:38 Archives/
-rw------  1 taylor     106020 Oct 10 13:47 LISTS
-rw-rw-r--  1 taylor     280232 Oct 10 16:22 mailing.lists
-rw-rw---  1 taylor       1031 Oct  7 15:44 newlists
```

```text
% touch example
% ls -l example
-rw-rw----  1 taylor      0 Oct 12 10:16 example
```

```text
% chmod 600 example
% ls -l example
-rw-------  1 taylor      0 Oct 12 10:16 example
```

```text
% chmod 666 example
% ls -l example
-rw-rw-rw-  1 taylor      0 Oct 12 10:16 example
```

```text
% chmod 755 example
% ls -l example
-rwxr-xr-x 1 taylor      0 Oct 12 10:16 example
```

```text
% umask
0007
% touch test.07
% ls -l test.07
-rw-rw----  1 taylor      0 Oct 12 14:38 test.07
```

```text
% touch test.077
% ls -l test.077
-rw------- 1 taylor 0 Oct 12 14:38 test.077
```

```text
% umask 277
% touch test.277
% ls -l test.277
-r--------  1 taylor           0 Oct 12 14:39 test.277
```

```text
% ls -lg /tmp
-rw-r--r-- 1 root    root        0 Oct 12 14:52 sh145
drwxr-xr-x 2 shakes  root      512 Oct 12 07:23 shakes/
-rw------- 1 meadmd  com435      0 Oct 12 14:46 snd.12
-rw------- 1 dessy   stuprsac 1191 Oct 12 14:57 snd.15
-rw------- 1 steen   utech      1 Oct 12 10:28 snd.17
-rw-r----- 1 jsmith  utech   258908 Oct 12 12:37 sol2
```

```text
r--rw-r--
 rw--w--w-
 rwxr-xr-x

r--r--rw-
 -w--w--w-
 r-x--x--x
```

```text
% id
uid=19 (smith) gid=50 (users) groups=50 (users)

% ls -lg
drwxr-xr-x 2 root users 512 Oct 12 14:52 sh/
drwxr-xr-x 2 shakes root 512 Oct 12 07:23 shakes/
drwx------ 2 meadmd com435 1024 Oct 12 14:46 tmp/
drwxr-x--- 3 smith users 512 Oct 12 12:37 viewer/
drwx------ 3 jin users 512 Oct 12 12:37 Zot!/
```

```text
% cd
% ls -F
Archives/      OWL/           rumors.26Oct.Z
InfoWorld/     PubAccessLists.Z   rumors.5Nov.Z
LISTS          bin/            src/
Mail/          educ
News/          mailing.lists.bitnet.Z
```

```text
% mkdir NEWDIR
% ls -F
Archives/      News/          mailing.lists.bitnet.Z
InfoWorld/     OWL/           rumors.26Oct.Z
LISTS          PubAccessLists.Z rumors.5Nov.Z
Mail/          bin/           src/
NEWDIR/        educ
```

```text
% ls -ld NEWDIR
drwxrwx---  2 taylor        24 Nov  5 10:48 NEWDIR
% ls -la NEWDIR
total 2
drwxrwx---  2 taylor        24 Nov  5 10:48 .
drwx------ 11 taylor       1024 Nov  5 10:48 ..
```

