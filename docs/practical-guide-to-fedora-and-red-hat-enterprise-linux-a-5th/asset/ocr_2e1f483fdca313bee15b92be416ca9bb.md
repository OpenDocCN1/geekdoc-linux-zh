setserial Gets and sets serial port information. Superuser can use this utility to configure a serial port. The following command sets the input address of /dev/ttys0 to 0x100, the interrupt (IRQ) to 5, and the baud rate to 115,000 baud:

```
# setserial /dev/ttys0 port 0x100 irq 5 spd_vhi
```

You can also check the configuration of a serial port with setserial:

```
# setserial /dev/ttys0
/dev/ttys0, UART: 16550A, Port: 0x0100, IRQ: 5, Flags: spd_vhi
```

Normally, setserial is called when the system is booting if a serial port needs custom configuration.

stat Displays information about a file or filesystem. Giving the -f (filesystem) option followed by the device name or mount point of a filesystem displays information about the filesystem including the maximum length of filenames (Namelen in the following example). See the stat man page for more information.

```
$ stat -f /dev/sda
File: "/dev/sda"
ID: 0   Namelen: 255   Type: tmpfs
Block size: 4096   Fundamental block size: 4096
Blocks: Total: 121237   Free: 121206   Available: 121206
Inodes: Total: 121237   Free: 120932
```

umask A shell builtin that specifies a mask a system user uses to set up access permissions when you create a file. A umask command has the following format:

```
umask [mask]
```

where mask is a three-digit octal number or a symbolic value such as you would use with chmod (page 204). The mask specifies the permissions that are not allowed. When mask is an octal number, the digits correspond to the permissions for the owner of the file, members of the group the file is associated with, and everyone else. Because mask specifies the permissions that are not allowed, the system subtracts each of the three digits from 7 when you create a file. The result is three octal numbers that specify the access permissions for the file (the numbers you would use with chmod). A mask that you specify using symbolic values indicates the permissions that are allowed.

Most utilities and applications do not attempt to create files with execute permissions, regardless of the value of mask; they assume you do not want an executable file. As a result, when a utility or application (such as touch) creates a file, the system subtracts each of the three digits in mask from 6. An exception is mksdir, which assumes that you want the execute (access in the case of a directory) bit set.

The following commands set the file-creation permissions mask and display the mask and its effect when you create a file and a directory. The mask of 022, when subtracted from 777, gives permissions of 644 (rw-r--r--) for a file and 755 (rwxr-xr-x) for a directory.