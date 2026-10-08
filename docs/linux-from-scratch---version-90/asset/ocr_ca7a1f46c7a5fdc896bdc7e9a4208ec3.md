# Linux From Scratch - Version 9.0

Now log out and reenter the chroot environment with an updated chroot command. From now on, use this updated chroot command any time you need to reenter the chroot environment after exiting:

logout

```
chroot "$LFS" /usr/bin/env -i \\
HOME=/root TERM="$TERM" \\
PS1=(lfs chroot) u:\w\$ \\
PATH=/bin:/usr/bin:/sbin:/usr/sbin \\
bin/bash --login
```

The reason for this is that the programs in /tools are no longer needed. For this reason you can delete the /tools directory if desired.

![](bbox=[0.036, 0.311, 0.08, 0.345])

# Note

Removing /tools will remove the temporary copies of Tcl, Expect, and DejaGNU which used for running the toolchain files. If you need these later on, they will need to be recompiled and installed. The BLFS book has instructions for this (see http://www.linuxfromscratch.org/blfs/).

If the virtual kernel file systems are mounted, unmounted or through a reboot, ensure that the virtual kernel file systems are mounted when reentering the chroot. This process was explained in Section 6.2.2, "Mounting and Populating /dev" and Section 6.2.3, "Mounted Virtual Kernel File Systems"

There were several static libraries that were suppressed earlier in the chapter in order to satisfy the regression tests in several packages. These libraries are from binutils, bzip2, e2fsprogs, flex, libtool, and zlib. If desired, remove them now:

```
rm -f /usr/bin/lib(bfd,opcodes).a
rm -f /usr/bin/lib/libb2.a
rm -f /usr/bin/lib(com_err,e2p,ss).a
rm -f /usr/bin/lib/libtdl.a
rm -f /usr/bin/lib/libf1.a
rm -f /usr/bin/lib/libz.a
```

There are also files installed in the /usr/lib and /usr/libexec directories with a file name extention of .la. These are "libtool archive" and generally unneeded on a linux system. None of them are necessary at this point. To remove them, run:

```
find /usr/lib /usr/libexec -name *.la -delete
```

For more information about libtool archive files, see the BLFS section "About Libtool Archive (.la) files".

222