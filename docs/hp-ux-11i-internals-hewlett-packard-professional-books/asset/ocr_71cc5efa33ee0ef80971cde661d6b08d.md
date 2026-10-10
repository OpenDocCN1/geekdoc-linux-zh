This
is my
data file

# Listing 8.2 # fsdb -F hfs /dev/vg00/lvol10 session output

First we will point **fsdb** (actually **fsdb_hfs**) toward the file system mount point and then examine the contents of inode #2

```
```
fsdb -F hfs /dev/vg00/lvol10  ← This opens the file system on
/dev/vg00/lvol10 for examinationby fsdb.
Note: fsdb has no prompt string
```
```

```
```
file system size = 53248 (frags)
isize/cyl group=160 (Kbyte blocks)
primary block size=8192 (bytes)
fragment size=1024 (bytes)
```
```

```
```
21  ← This command list the contents of inode #2
no. of cyl groups = 7
i#:2 md: d---rwxr-xr-x ln: 4 uid: 0 gid: 0 sz: 1024
ci:0
a0 : 208 a1 : 0 a2 : 0 a3 : 0 a4 : 0 a5
: 0
a6 : 0 a7 : 0 a8 : 0 a9 : 0 a10: 0
a11: 0
a12: 0 a13: 0 a14: 0
at: Fri Aug 8 12:56:54 2003
mt: Fri Aug 8 12:46:22 2003
ct: Fri Aug 8 12:46:22 2003
```
```

```
```
a0b.p0d ← Next we list the block pointed to by "a0"
and format it as directory data
d0: 2 .
d1: 2 .
d2: 3 lost + found
d3: 1280 chris
```
```

```
```
1280i ← We see that inode #1280 is the "chris"
directory and list its contents

i#:1280 md: d---rwxrwxrwx ln: 2 uid: 0 gid: 3 sz: 1024 ci:0
a0 : B200 a1 : 0 a2 : 0 a3 : 0 a4 : 0 a5
: 0
a6 : 0 a7 : 0 a8 : 0 a9 : 0 a10: 0
a11: 0
```
```