
| Option | Description |
|---|---|
| -a | The startup program interprets this flag to mean "Ask me," so it prompts for the name of the stand-alone program to load. |
| -f | When starting an Autoclient system, this option forces the boot program to bypass the client's local cache and read all files over the network from the client's file server. This option is ignored for all non-Autoclient systems. The -f option is then passed to the stand-alone program. |
| -r | Triggers device reconfiguration during startup. (This option is covered in Chapter 16, "Device Administration and Disk Management.") |
| flags | The boot program passes all startup flags to filename. They are not interpreted by boot. (See the next section for information on the options available with the default stand-alone program, kernel/unix.) |

If you want to start up the default program when auto-boot? is false, a few options are available for starting up the system from the ok prompt.

When you type the following:

```
boot
```

the machine will start up from the default startup device using no startup arguments. This is set in the boot-device variable.

Type the following:

```
boot [OBP name]
```

When you specify an explicit OBP name, such as disk3, the machine will start up from the specified startup device using no startup arguments.

Here's an example:

```
boot disk3
```

The system will boot from the disk drive defined by the devalias named disk3. It will then load kernel/unix as the default stand-alone startup program.

Type

```
boot [options]
```

When you specify explicit options with the boot command, the machine will use the specified arguments to start up from the default startup device.

Here's an example:

```
boot -a
```

The system will then ask for the name of the stand-alone program to load. If you specify kernel/unix, which is the default, you will be prompted to enter the directory that contains the kernel modules. (See the next section for details on kernel modules.)

Type

```
boot [OBP name] [options]
```

When you specify the boot command with an explicit startup device and explicit arguments, the machine will start up from the specified device with the specified arguments.

Here's an example:

```
boot disk3 -a
```

This example will give the same prompts as the previous example, except that you are now specifying a different startup device. The system will start up the bootblock from the disk drive defined by the devalias named disk3.

During the startup process, OpenBoot performs the following tasks:

- 1. The firmware can reset the machine if a client program has been executed since the last reset. The client program is normally an operating system or an operating system's loader program, but boot can also be used to load and execute other kinds of programs, such as diagnostics. For example, if you have just issued the test net command, when you next type boot, the system will reset before starting up.
- 2. The boot program is loaded into memory using a protocol that depends on the type of the selected device. You can start up from disk, tape, floppy, or the network. A disk startup might read a fixed number of blocks from the beginning of the disk, whereas a tape startup might read a particular tape file.
- 3. The loaded boot program is executed. The behavior of the boot program can be further controlled by the argument string, if one was passed to the boot command on the command line.

The program loaded and executed by the startup process is a secondary boot program, the purpose of which is to load the standalone program. The second-level program is either ufsboot, when starting up from a disk, or inetboot, when starting up across the network.

If starting up from disk, the bootstrap process consists of two conceptually distinct phases: primary startup and secondary startup. The PROM assumes that the program for the primary startup (bootblk) is in the primary bootblock, which resides in sectors 1–15 of the startup device. The bootblock is created using the installboot command. The software installation process typically installs the bootblock for you, so you won’t need to issue this command unless you’re recovering a corrupted bootblock.

To install a bootblock on disk c0t3d0s0, type the following:

```
installboot /usr/platform/'uname -i'/lib/fs/ufs/bootblk \
/dev/rdsk/c0t3d0s0
```

You cannot see the bootblock. It resides in a protected area of the disk that cannot be viewed. The program in the bootblock area will load the secondary startup program, named ufsboot.

When executing the boot command, if a filename was specified, this filename is the name of the stand-alone startup program to be loaded. If the pathname is relative (does not begin with a slash), ufsboot will look for the program in a platform-dependent search path. In other words, the relative path to the stand-alone program will be prefixed with /platform/<platform-name>. <platform-name> will be specific to your hardware.

NOTE
Use the uname -i command to determine your system's platform name. For example, on a SPARCstation10, the path will be /platform/SUNW,SPARCstation-10. Use the command uname -m to find the hardware-class-name of a system; for a SPARCstation10, the hardware-class-name will be sun4m. If you look in the /platform directory, you'll see that /platform/SUNW,SPARCstation-10 is merely a link to /platform/sun4m.

On the other hand, if the path to filename is absolute, boot will use the specified path. The startup program then loads the stand-alone program and transfers control to it.

The following example shows how to specify the stand-alone startup program from the OpenBoot ok prompt:

```
ok boot disk5 kernel/unix -s
```

In the example, the PROM will look for the primary boot program (bootblk) on disk5 (/iommu/sbus/espdma@f,400000/esp@f,800000/sd@0,0). The primary startup program will then load ufsboot. This will load the stand-alone startup program named /platform/SUNW,SPARCstation-10/kernel/unix using the -s flag. Typical secondary startup programs, such as kernel/unix, accept arguments of the form filename -flags, in which filename is the path to the stand-alone program and -flags is a list of options to be passed to the stand-alone program. The example will start up the operating system kernel, which is described in the next section. The -s flag will instruct the kernel to start up in single-user mode.

## KERNEL

The secondary startup program, ufsboot, which was described in the preceding section, loads the operating system kernel. The platform-specific kernel used by ufsboot is named /platform/`uname -m`/kernel/unix.

The kernel initializes itself and begins loading modules, using ufsboot to read the files. After the kernel has loaded enough modules to mount the root file system, it unmaps the ufsboot program and continues, using its own resources. The kernel creates a user process and starts the /sbin/init process, which starts other processes by reading the /etc/inittab file. (The /sbin/init process is described in Chapter 1.)

The kernel is dynamically configured in Solaris 8. It consists of a small static core and many dynamically loadable kernel modules. A kernel module is a hardware or software component that is used to perform a specific task on the system. An example of a loadable kernel module is a device driver that is loaded when the device is accessed. Drivers, file systems, STREAMS modules, and other modules are loaded automatically as they are needed, either at startup or at runtime. After these modules are no longer in use, they can be unloaded. Modules are kept in memory until that memory is needed. The modinfo command provides information about the modules currently loaded on a system.

When the kernel is loading, it reads the /etc/system file where system configuration information is stored. This file modifies the kernel's parameters and treatment of loadable modules. It specifically controls the following:

- The search path for default modules to be loaded at boot time, as well as the modules not to be loaded at boot time
- The modules to be forcibly loaded at boot time rather than at first access
- The root type and device
- The new values to override the default kernel parameter values

The following is an example of the default /etc/system file:

```
*ident      "@(#)system      1.18    97/06/27 SMI" /* SVR4 1.5 */
*
* SYSTEM SPECIFICATION FILE
*
* moddir:
*
*Set the search path for modules. This has a format similar to the
*csh path variable. If the module isn't found in the first directory
*it tries the second and so on. The default is /kernel /usr/kernel
*
*Example:
*moddir: /kernel /usr/kernel /other/modules
* root device and root filesystem configuration:
*
*The following may be used to override the defaults provided by
*the boot program:
*
*rootfs:          Set the filesystem type of the root.
*
*rootdev:         Set the root device. This should be a fully
                  expanded physical pathname. The default is the
                  physical pathname of the device where the boot
                  program resides. The physical pathname is
                  highly platform and configuration dependent.
```
