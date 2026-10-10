# Tip

*If you need to reinstall your Stage 1 and Stage 2 boot loaders, you can do so by typing `disklabel /dev/name`, where `/dev/name` is the name of your FreeBSD slice, such as `/dev/ad0s2`. Ideally, this command should never be necessary, but it might be necessary if your disk has been damaged.*

From the point of view of somebody booting the computer, this stage of the boot process begins with a prompt such as

```
Hit [Enter] to boot immediately, or any other key for command prompt.
Booting [/boot/kernel/kernel] in 9 seconds...
```

The time in the second message counts down. If you press any key except ENTER before the countdown reaches 0, you can enter boot parameters to modify the way the system boots. These options include

+   ❚ `autoboot seconds` This option restarts the boot countdown, starting at the specified number of seconds.

+   ❚ `boot [-options] [kernelname]` You can boot the specified kernel and pass it any options you like with this command.

+   ❚ `load [-t type] modulename` You can load a kernel module with this option. A kernel module is a driver or other kernel extension, so you can use this option to get unusual hardware working. Kernel modules can be loaded after the system has booted, though, so you need this option only if the hardware is required for FreeBSD to boot, such as a driver for an otherwise unsupported disk controller.

+   ❚ `ls [-1] [path]` This option works much like the ls command once the system has booted; it displays files in a specified directory. You might not have access to all your partitions at this early stage in the boot process, though.

+   ❚ `lsdev [-v]` This option lists the devices from which you can load modules. Adding `-v` creates a more verbose report.

+   ❚ `lsmod [-v]` You can see a list of loaded modules with this command. As with `lsdev`, `-v` displays more information.

+   ❚ `more filename` This option displays `filename` a screenful at a time. You may need this feature in order to read documentation on modules you want to install.

+   ❚ `reboot` This command reboots the system.

+   ❚ `unload` You can unload all loaded modules with this command.

You can use these options to load an alternate kernel—say, for testing purposes after you've compiled a new kernel, as described in Chapter 12. You may also need to load or unload kernel modules to get your system to boot, or pass options to the kernel. (Chapter 12 includes additional information on some of these parameters.)