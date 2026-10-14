
At this point, the boot sector from the active partition is loaded into memory. In the case of Windows 2000, the boot sector contains NTLDR, which is loaded and initialized. This is where the boot process really begins.

## THE WINDOWS 2000 BOOT PROCESS

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

![](img/415c89a1ede71e11e5040a0038b6916c_116_0.png)

## Figure 3.5

Starting Windows screen.

NTDETECT is included in the Registry under HKEY_LOCAL_MACHINE\HARDWARE. NTDETECT looks for the following on your system:

- CPU ID.
- BUS type.
- Video board.
- Keyboard and mouse (if present).
- Serial and parallel ports.
- Floppy drives.

Next, once NTDETECT has successfully completed, NTLDR passes control of the system to NTOSKRNL.EXE. We can divide the rest of the boot process into five phases: loading the kernel, initializing the kernel, loading system services, starting the Win32 subsystem, and user logon.

## LOADING THE KERNEL

As soon as NTLDR passes control to NTOSKRNL.EXE, the kernel is loaded. While the Starting Windows screen from Figure 3.5 is displayed, you can press the <F8> key to display the Advanced Options Menu,

which provides advanced boot and recovery options. This menu provides the ability to start your system after experiencing problems during a normal boot. We will discuss the Advanced Options Menu later in this chapter.

Once the kernel is loaded, the system HAL is loaded from HAL.DLL. Once the HAL has been loaded, the kernel loads the System Hive from SystemRoot\System32\Config\System and scans it to determine which drivers and services should be loaded. The drivers and services set to start at boot (this setting can be viewed/changed from the services and devices applets in the Control Panel) are loaded based on the order in which they appear in the HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\ServiceGroupOrder\List Registry value. As we mentioned previously, device driver files are accessed from the SystemRoot\System32\Drivers folder. While this phase is executing, the system displays a series of progress dots (...) across the top of the display. If you wish to have a more detailed progress display, you can add the ShowOnScreen (/sos) switch to the Operating System entry in boot.ini.

## INITIALIZING THE KERNEL

After the kernel has been successfully loaded into memory (NTOSKRNL.EXE, HAL, and all drivers and services), the system must initialize the loaded components. If you are familiar with the Windows NT 4.0 boot sequence, then you can immediately recognize this phase when the screen has been painted blue and the following (or something similar) is displayed at the top of the screen:

```
Microsoft ® Windows NT ® Version 4.00 (Build 1381)

2 System Processors MultiProcessor Kernel [512 MB Memory]
```

Windows 2000, however, greets you with a "modernized" splash screen. This splash screen is shown in Figure 3.6.

During this phase, the following operations are completed:

- 1. The current control set is saved and used to create the clone control set, which is stored under the HKEY_LOCAL_MACHINE\SYSTEM\Clone Registry key.
- 2. The services and drivers loaded into memory during the kernel load phase are initialized.
- 3. The HKEY_LOCAL_MACHINE\HARDWARE key is built using the information collected by NTDETECT (x86) or OSLOADER (RISC) earlier in the boot process.
- 4. The System Hive is again scanned to locate, initialize, and start the services and drivers set to be started by the system.
