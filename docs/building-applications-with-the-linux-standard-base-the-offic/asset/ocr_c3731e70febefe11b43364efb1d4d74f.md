# Example 11.4: Running lsbchk

```
Checking symbols in /lib/ld-lsb.so.1
Checking symbols in /usr/lib/libGL.so.1
Checking symbols in /usr/X11R6/lib/libICU.so.6
Checking symbols in /usr/X11R6/lib/libSM.so.6
Checking symbols in /usr/X11R6/lib/libX11.so.6
Checking symbols in /usr/X11R6/lib/libXext.so.6
Checking symbols in /usr/X11R6/lib/libXt.so.6
Checking symbols in /lib/libcrypt.so.1
Checking symbols in /lib/libdl.so.2
Checking symbols in /lib/libm.so.6
Checking symbols in /lib/libncurses.so.5
Checking symbols in /lib/libpthread.so.0
Checking symbols in /lib/librt.so.1
Checking symbols in /lib/libutil.so.1
Checking symbols in /usr/lib/libz.so.1
```

# Example 11.5: A journal_.lsbchk File

```
0|lsb-0.1 14:50:07 20040113
|User: nicole (0) TCC Start, Command line: lsbchk
5|Linux suefan.chelsea.com 2.4.20-8 
#1 Sat Aug 26 13:24:28 EST 1984 i686 
|System Information
30|VSX_NAME=lsb1bchk version
10|/lib/ld-lsb.so.1 14:50:07
400|1 1 14:50:07|IC Start
200|1 1 0 14:50:07|Looking for library /lib/ld-lsb.so.1
220|1 1 0 14:50:07|PASS
520|1 1 0 0 0|FILE_SIZE 10450
520|1 1 0 0 0|BINARY_MD5SUM=727978f21c43e021a77c8b396ae82db
410|1 1 14:50:07|IC End
400|1 2 14:50:07|IC Start
200|1 2 14:50:07|Check header id EI_MAG0 is ELFPMAG0
220|1 2 0 14:50:07|PASS
410|1 2 14:50:07|IC End
400|1 3 14:50:07|IC Start
200|1 3 0 14:50:07|Check header id EI_MAG1 is ELFPMAG1
220|1 3 0 14:50:07|PASS
410|1 3 14:50:07|IC End
400|1 4 14:50:07|IC Start
200|1 4 0 14:50:07|Check header id EI_MAG2 is ELFPMAG2
220|1 4 0 14:50:07|PASS
410|1 4 14:50:07|IC End
400|1 5 14:50:07|IC Start
```