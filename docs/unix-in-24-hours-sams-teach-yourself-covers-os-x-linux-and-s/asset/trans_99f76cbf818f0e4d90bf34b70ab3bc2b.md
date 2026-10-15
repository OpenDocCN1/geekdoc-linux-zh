

```
% ls -l big.file
-rwx------ 1 taylor taylor 3198588 23 Apr 22:48 big.file
% gzip -v big.file
big.file:              72.7% -- replaced with big.file.gz
% ls -l big.file*
-rwx------ 1 taylor taylor 871440 23 Apr 22:48 big.file.gz
```

```
% gunzip LISTDATA2
% ls -l LISTDATA2
-rw-r--r-- 1 taylor  taylor  24064 23 Apr 22:41 LISTDATA2
```

```
% ls -l LISTDATA2 big.file
-rw-r--r--  1 taylor taylor     24064 23 Apr 22:41 LISTDATA2
-rwx------  1 taylor taylor  3198588 23 Apr 22:48 big.file
% compress -v LISTDATA2 big.file
LISTDATA2.Z: 25% compression
big.file.Z: 33% compression
% ls -l LISTDATA* big.file*
-rw-r--r--  1 taylor taylor     5962 23 Apr 22:41 LISTDATA2.Z
-rwx------  1 taylor taylor 1068457 23 Apr 22:48 big.file.Z*
% uncompress LISTDATA* big.file*
% bzip2 -v LISTDATA2 big.file
LISTDATA2: 5.979:1, 1.338 bits/byte, 83.27% saved, 24064 in, 4025 out.
big.file: 5.305:1, 1.508 bits/byte, 81.15% saved, 3198588 in, 602958 out.
% bunzip2 LISTDATA* big.file*
% ls -l LISTDATA big.file
-rw-r--r--  1 taylor taylor     24064 23 Apr 22:41 LISTDATA2
-rwx------  1 taylor taylor  3198588 23 Apr 22:48 big.file
```

```
% ls -l
total 403
drwx------ 2 taylor 512 Sep 30 10:38 Archives/
drwx------ 3 taylor 512 Oct 1 08:23 InfoWorld/
-rw------ 1 taylor 106020 Oct 10 13:47 LISTS
drwx------ 2 taylor 1024 Sep 30 10:50 Mail/
drwx------ 2 taylor 512 Oct 6 09:36 News/
drwx------ 2 taylor 512 Sep 30 10:51 OWL/
-rw------ 1 taylor 4643 Oct 10 14:01 RUMORS.18Sept
drwx------ 2 taylor 512 Oct 10 19:09 bin/
-rw------ 1 taylor 3843 Oct 10 16:22 iecc.list
-rw-rw-r-- 1 taylor 280232 Oct 10 16:22 mailing.lists
-rw-rw--- 1 taylor 1031 Oct 7 15:44 newlists
drwx------ 2 taylor 512 Oct 10 19:09 src/
```

```
% ls -l bin
total 57
-rwx------  1 taylor      1507 Aug 17 13:27 bounce.msg
-rwxrwx---  1 taylor     32916 Oct 10 19:09 calc
-rwx------  1 taylor     18567 Sep 14 22:14 fixit
-rw-------  1 taylor       334 Oct  1 09:53 punt
-rwx------  1 taylor      3424 Sep 10 22:27 rumor.mill.sh
```

```
% pwd
/home/taylor
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local:/usr/local/bin:
% ls -l bin/say.hi
-rwxrwx---  1 taylor        9 Oct 11 13:32 bin/say.hi
% say.hi
hi
```

```
% chmod -x bin/say.hi
% ls -l bin/say.hi
-rw-rw----  1 taylor         9 Oct 11 13:32 bin/say.hi
% say.hi
/home/taylor/bin/say.hi: Permission denied.
```

% my.new.cmd
/home/taylor/bin/my.new.cmd: Permission denied.

```
% chmod +x bin/my.new.cmd
% ls -l bin/my.new.cmd
-rwxr----- 1 taylor 0 Oct 11 15:07 bin/my.new.cmd
% my.new.cmd
%
```

-rw------ 1 taylor 3843 Oct 10 16:22 iecc.list
-rw-rw-r-- 1 taylor 280232 Oct 10 16:22 mailing.lists
-rw-rw---- 1 taylor 1031 Oct 7 15:44 newlists
-rwxr-x--- 1 taylor 64 Oct 9 09:31 the.script

```
% ls -ld testme
dr-x------ 2 taylor      512 Oct 11 17:03 testme/
% ls -l testme
total 0
-rw-rw--- 1 taylor      0 Oct 11 17:03 file
% ls -l testme/file
-rw-rw--- 1 taylor      0 Oct 11 17:03 testme/file
```

```
% ls -ld testme
dr--------  2 taylor              512 Oct 11 17:03 testme/
% ls -l testme
testme/file not found
total 0
% ls -l testme/file
testme/file not found
```

```
% ls -ld testme
dr-x-----  2 taylor      512 Oct 11 17:03 testme/
% ls -l testme
testme unreadable
% ls -l testme/file
-rw-rw----  1 taylor      0 Oct 11 17:03 testme/file
```

```
% ls -l
total 403
drwx------ 2 taylor      512 Sep 30 10:38 Archives/
drwx------ 3 taylor      512 Oct  1 08:23 InfoWorld/
-rw------ 1 taylor    106020 Oct 10 13:47 LISTS
drwx------ 2 taylor     1024 Sep 30 10:50 Mail/
drwx------ 2 taylor      512 Oct  6 09:36 News/
drwx------ 2 taylor      512 Sep 30 10:51 OWL/
-rw------ 1 taylor     4643 Oct 10 14:01 RUMORS.18Sept
drwx------ 2 taylor      512 Oct 10 19:09 bin/
-rw------ 1 taylor     3843 Oct 10 16:22 iecc.list
-rw-rw-r-- 1 taylor   280232 Oct 10 16:22 mailing.lists
-rw-rw--- 1 taylor     1031 Oct  7 15:44 newlists
drwx------ 2 taylor      512 Oct 10 19:09 src/
```

