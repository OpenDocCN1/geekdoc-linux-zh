```
# odump -Dl /usr/sbin/caad

***LIBRARY LIST SECTION***
Name                Time-Stamp        CheckSum      Flags Version
/usr/sbin/caad:
libpolicy.so        Jan 16 04:39:17 2002 0x7958cdb5      0 osf.1
libbvm.so           Jan 15 17:37:17 2002 0xde4a5d09      0 osf.1
libclcu.so          Jan 15 17:36:05 2002 0xd148a817      0 osf.1
libm.so             Jan 15 17:20:50 2002 0x07775704      0 osf.1
libpthread.so       Jan 15 17:26:48 2002 0x4a2a0c94      0 osf.1
libcxx.so           Jan 15 17:29:14 2002 0x9060972e      0 cxx6.3
libexc.so           Jan 15 17:20:58 2002 0xb0f9a902      0 osf.1
libxc.so            Jan 15 17:19:09 2002 0x1e4e245f      0 osf.1
```

The following command output lists the location and some of the shared library files available in Tru64 UNIX.

```
# ls /usr/shlib
.mrg.so_locations      libarmui.so        libmfs.so
.new.so_locations      libaud.so          libmxr.so
.proto.so_locations    libbwt.so          libnbd.so
TCR_libclcu.so         libbwt_g.so        libnet.so
X11                    libbkr.so          libnuma_g.so
null                   libbuma.so         libpacl.so
diagui_unix.uid       libc_r.so          libpota.so
ev5                    libcfrom.so        libota3.so
generic                libcfg.so          libpacl.so
libDSNLlinkAPI.so      libchf.so          libproplist.so
libbDXm.so             libclcu.so         libpset.so
libbDXterm.so          libclua.so         libpthread.so
libbDECOR.so           libcmail.so        libpthreaddebug.so
libbHelp.so            libcsa.so          libpthreada.so
libbDmail.so           libcurses.so       libpthreads.so
...
```

# 2.1.6 Memory Wiring

Most of the physical memory on Tru64 UNIX is pageable. This means that the contents of the memory pages may be paged out to swap space (on disk), or swapped out to swap space if the system's free page list becomes critically low. Certain applications may require that portions of its memory be treated as if it were non-pageable. This activity (referred to as "wiring down" a page) is limited to processes that are owned by root. The kernel may also wire down pageable pages to meet its dynamic memory requirements.

The following example concludes with a section displaying statistics on the wired pages within the system.