# Asynchronous I/O

Once you have the test program compiled, use the truss(1) command to do a sys-
-call trace of the execution path.

```
# truss -t kaio,kaio create aio /dev/rdsk/c0t3d0s0\                                                              = 9
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 2
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio_create(3, 0xFFEFF19, 1024, 0xFFEFB590)                                     = -268438128
kaio (AIOWAIT, 0x00000000)
aio succeeded
```

Note that you run this as root because it's reading directly from a raw
device-specific file. On the command, the -t flag is specified with truss to
instruct truss to trace only the kaio and lwp_create system calls.

The example used a raw device-specific file as the argument to the aio pro-
gram. You have to specify a full path name for the file when you invoke aio).
truss(1) output shows a kaio system call, followed by two lwp_create calls, and
two more entries into the kaio routine to do the actual read, followed by
the aiwait. The last line is the output from the kaio (aio succeeded).
in this example, kaio is in fact a supported facility for this I/O operation—the kaio
call with the AIREAD flag not return an error.

In the example, kaio is not supported for the I/O.

```
# truss -t kaio,kaio create junkfile
kaio(5, 0xFFFFFF, 0xFFFFFF, 0xE6F68B50, 0x00000000, 0x00000000, 0x00000000) = 0
lwp_create(0xFFEFEB10, 0x00000000)                                                                = 0
lwp_create(0x00000000, 0x00000000)                                                               = 0
kaio (AIOWAIT, 0xFFEFF188, 1024, 0xFFEFB558)                                 Err#48 ENOTSUP
lwp_create(0xFFEFEDA8, 0xE6F672A)                                                               = 3
lwp_create(0x00000000, 0x00000000)                                                               = -278369456
lwp_create(0xFFEFEDA8, 0xE6F7D4A)                                                               = 4
lwp_create(0x00000000, 0x00000000)                                                               = -278406320
lwp_create(0xFFEFEDA8, 0xE6F6A4A)                                                               = 5
lwp_create(0x00000000, 0x00000000)                                                               = -278434184
lwp_create(0xFFEFEDA8, 0xE6F6B4A)                                                               = 6
lwp_create(0x00000000, 0x00000000)                                                               = -2784804008
lwp_create(0xFFEFEDA8, 0xE6F5EE8)                                                               = 7
lwp_create(0x00000000, 0x00000000)                                                               = -278516912
lwp_create(0xFFEFEDA8, 0xE6F594A)                                                               = 8
lwp_create(0x00000000, 0x00000000)                                                               = -278553776
lwp_create(0xFFEFEDA8, 0xE6F577A)                                                               = 9
lwp_create(0x00000000, 0x00000000)                                                               = -278590640
lwp_create(0xFFEFEDA8, 0xE6F47F2)                                                               = 10
lwp_create(0x00000000, 0x00000000)                                                               = -278627504
lwp_create(0xFFEFEDA8, 0xE6F6388)                                                               = 11
lwp_create(0x00000000, 0x00000000)                                                               = -278664368
kaio (AIOWAIT, 0x00000000)                                                        Err#22 EINVAL
kaio (AIOWAIT, 0x00000000)                                                        Err#22 EINVAL
kaio (AIOWAIT, 17560)                                                                = 0
aio succeeded
```

In this example, we are reading a file in the system. The trace shows that our
entry entered the kernel with a kaio call, created a couple of LWPs, and