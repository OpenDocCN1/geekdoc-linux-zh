The table below summarizes the effects of the possible combinations of these three flags when a file is opened for writing using the call

```
open( "file", O_WRONLY | flags );
```

| flags | If the file exists | If the file does not exist |
|---|---|---|
| 0 | opens for writing and sets pointer to first byte | fails |
| O_CREAT | opens for writing and sets pointer to first byte | creates "file" |
| O_EXCL | opens for writing and sets pointer to first byte | fails |
| O_TRUNC | opens for writing and zeroes its contents | fails |
| O_CREAT | O_EXCL | fails | creates "file" |
| O_CREAT | O_TRUNC | opens for writing and zeroes its contents | creates "file" |
| O_TRUNC | O_EXCL | opens for writing and zeroes its contents | fails |
| O_CREAT | O_TRUNC | O_EXCL | fails | creates "file" |

The program wrflagtest.c in the demos directory for Chapter 5 can be used to test the effects of all combinations of these flags.

# 4.3 Device Files

Not only is every physical device in a UNIX system associated with a device special file, but every logical device is as well. Logical devices are devices that exist as abstractions of real physical devices. Although UNIX does not require this, it has been the convention that all of the device files are located in the /dev directory.

# 4.3.1 Naming and Organizing Device Files

Different versions of UNIX use different methods of organizing and naming device files. For example, under Solaris 9, you will find that almost all of the terminal files contained there are symbolic links to files in the directory /devices/pseudo, and that the targets of these symbolic links have names such as pts0:2.

In contrast, in Linux 2.6, instead of a /devices/pseudo directory there is a directory /dev/pts, and all of the device files within /dev/pts have small numbers such as 1,2,3, ... that correspond to the terminals of active connections.

> 3 Sometimes, for example, there may be more than one name for a given physical device, such as a port or a disk. A logical device is another name for that device.

> 4 At installation time, Linux can be configured so that its support of pseudo terminal devices is the same as that of systems such as Solaris 9 by using the CONFIG_UNIX98_PTYS and CONFIG_DEVPTS_FS flags. The Unix98 standard specifies how /dev/pts is used for pseudo-terminal support.