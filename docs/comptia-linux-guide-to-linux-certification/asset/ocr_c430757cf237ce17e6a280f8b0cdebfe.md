```
checking for stdint.h... yes
checking for unistd.h... yes
checking whether byte ordering is bigendian... no
checking for X11 libraries, headers
checking for gethostbyname... yes
checking for connect... yes
checking for remove... yes
checking for shmat... yes
checking for IceConnectionNumber in -lICE... no
checking for pkg-config... /usr/bin/pkg-config
checking for library containing socket... none required
checking for library containing inet_aton... none required
checking sys/select.h usability... yes
checking sys/select.h presence... yes

<Additional checks omitted here>

checking for struct statvfs.f namemax... yes
checking for struct statfs.f namelen... yes
checking for struct statvfs.f namelen... no
checking for special C compiler options needed for large files... no
checking for _FILE_OFFSET_BITS value needed for large files... no
checking mntent.h usability... yes
checking mntent.h presence... yes
checking for mntent.h... yes
checking for setmntent... yes
configure: creating ./config.status
config.status: creating Makefile
[root@server1 rdesktop-1.8.2]# 
```

After the configure script has run, a Makefile exists in the current directory, as shown in the following output:

```
[root@server1 rdesktop-1.8.2]# head Makefile
#
# rdesktop: A Remote Desktop Protocol client
# Makefile.in
# Copyright (C) Matthew Chapman 1999-2007
#
prefix = /usr/local
exec_prefix = ${prefix}
bindir = ${exec_prefix}/bin
mandir = ${datarootdir}/man
[root@server1 rdesktop-1.8.2]# 
```

This Makefile contains most of the information and commands necessary to compile the program. Some program source code that you download might contain commented lines that you need to uncomment to enable certain features of the program or to allow the program to compile on your computer architecture. Instructions for these commented areas are documented in the Makefile itself; thus, it is good form to read the Makefile after you run the