At this point, the boot sector from the active partition is loaded into memory. In the case of Windows 2000, the boot sector contains NTLDR, which is loaded and initialized. This is where the boot process really begins.

# THE WINDOWS 2000 BOOT PROCESS

The NTLDR program is the first step of the boot process. We will focus in this section on booting x86 systems. If you would like to know more about booting RISC systems, we suggest you acquire one of the Microsoft Press reference guides, such as the Windows 2000 Beta Training Kit.

NTLDR first switches the processor into 32-bit flat memory mode (386 mode). Next, NTLDR starts built-in simple filesystem drivers to access the operating system. At this point, NTLDR may access NTBOOTDD.SYS (in the unlikely event you are using a SCSI controller without a BIOS) to boot from a SCSI device. Once NTLDR has access to the filesystem, it examines the boot.ini file to determine which operating systems are on the system. The boot.ini file contains an entry for each operating system, specifying where it is located on the system. A detailed description of the boot.ini file and instructions on modifying it are included later in this chapter. The following sample boot.ini includes entries for Windows 2000 and DOS:

```
[boot loader]

timeout=30

default=multi(0)disk(0)rdisk(0)partition(1)\WINNT

[operating systems]

multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Server" /fastdetect

C:\="Microsoft MS-DOS 6.22"
```

Once NTLDR has examined the boot.ini file, it presents the user with a screen allowing the selection of one of the installed operating systems. If Windows 2000 is the only installed operating system, the selection screen is not displayed. If the user does not select an operating system within the specified timeout period (30 seconds by default), NTLDR selects the default. If the user selects an operating system other than Windows 2000, NTLDR loads and runs BOOTSECT.DOS and relinquishes control to that operating system.

After selecting Windows 2000, NTLDR executes NTDETECT.COM. At this point, NTDETECT.COM will display the Starting Windows screen shown in Figure 3.5.

NTDETECT.COM is used to examine your system’s hardware and returns a list of what hardware was found to NTLDR. The list of hardware located by