# GNU gdb (GDB) 7.6.1-ubuntu
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GPL version 3 or later
<http://gnu.org/licenses/gpl.html>

This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law. Type "show
copying"

and "warranty" for details.
This GDB was configured as "i686-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/gdb/bugs>/...

```
Reading symbols from /home/dennis/polygon/a.out...
(gdb) b 17_l.c:61
Breakpoint 1 at 0x804845f: line 11
(gdb) run
Starting program: /home/dennis/polygon/.a.out
Breakpoint 1, comp (_a=0xbffff08, b_=b@entry=0xbffff08) at
17_l.c:61
11
(gdb) p *a
    if (*a==b)
$1 = 18892
(gdb) p *b
$2 = 45
(gdb) c
Continuing.
```

Breakpoint 1, comp (_a=0xbffff084, b_=b@entry=0xbffff084) at
17_l.c:11

```
(gdb) p *a
    if (*a==b)
$3 = -98
(gdb) p *b
$4 = 4087
(gdb) bt
#0 comp (_a=0xbffff088, b_=b@entry=0xbffff08fc) at 17_l.c:11
#1 0x7e42732 in msort_with_tmp (p=@entry=0xbffff07fc,
b_=b@entry=0xbffff08ff, n=entry=2)
    at msort.c:65
#2 0x7e4273e in msort_with_tmp (n=2, b=0xbffff0ff8, p=0xbffff07fc) at
msort.c:45
#3 msort_with_tmp (p=@entry=0xbffff07fc, b_=b@entry=0xbffff08ff,
n=entry=5) at msort.c:53
#4 0x7e4273e in msort_with_tmp (n=5, b=0xbffff0ff8, p=0xbffff07fc) at
msort.c:45
#5 msort_with_tmp (p=@entry=0xbffff07fc, b_=b@entry=0xbffff08ff,
n=entry=10) at msort.c:53
#6 0x7e422cef in msort_with_tmp (n=10, b=0xbffff0ff8, p=0xbffff07fc) at
msort.c:45
#7 GI_sort_r (b=@entry=0xbffff0ff8, n=entry=10, s=@entry=4,
cmp_arg=@entry=0x0) at msort.c:297
#8 0xb7e42cdcf in GI_sort (b=0xbffff0ff8, n=10, s=4, cmp=0x804844d
<comp>) at msort.c:307
```