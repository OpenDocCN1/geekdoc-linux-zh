
After successfully running the new kernel for a few days you can delete the old kernel and old modules by executing the following commands:

```bash
# rm -f /vmlinuz.old
# rm -f /lib/modules.old
```

## PATCHING THE KERNEL

As bugs in the kernel are fixed, kernel patches are released. The kernel naming convention is of the type `kernel-name-major.minor.patch-level`. For instance, the kernel `linux-2.2.12` is named linux, has a major release number of 2, a minor release number of 2, and a patch level of 12. When a patch for this kernel is released it will become available at kernel.org and other mirror sites as `patch-2.2.13.gz`.

Download the patch from `ftp.kernel.org` or a mirror site and change to the directory `/pub/linux/kernel`. Depending on what version of kernel you are running, change to that directory; for instance, if you are running version 2.2, change to the directory `v2.2`. Listing of this directory will show the various kernel packages and patch files. Download the particular patch file you are interested in, such as `patch-2.2.13.gz`.

Copy the patch file to `/usr/src`. Before applying the patches it is advisable to save a copy of source tree, in case something goes wrong and you need to start over. First run `make clean` and then save the source tree as a compressed tar archive:

```bash
# cd /usr/src/linux
# make clean
# tar czvf linux.old.tar.gz linux
```

Next, apply the patches to the source tree using the following commands:

```bash
# cd /usr/src/linux
# zcat patch-2.2.13.gz | patch -p0 2>&1 | tee patch.out
```

The patches will be applied to the source tree, a process that will generate considerable output to the screen reporting on all the patches that are being applied. If you want less voluminous output you can add a `-s` flag to the patch command which tells the patch program to only report errors. With the tee command we can send the output to a file as well as to the screen. If patch encounters errors it will create reject files that are named with `.rej` extensions. You can find all of them by running the following command:

```bash
# find . -name '*.rej' -print
```

If patch produces errors, one of the likely causes is that it found a `config.in` file that is not exactly as patch expected it to be. This is because possible customizations have been done to this file during an earlier kernel build process. To fix this problem, take a look at the `config.in.rej` file. The `.rej` file indicates what part of the patch remains to be applied. The changes are typically marked with `+` and `-` at the beginning of the line. If you are familiar with how the UNIX program diff works, this will not seem unfamiliar.

![](img/6c13bcf02a08ad7923caab46f051d96a_221_0.png)

The `+` symbol indicates the line should be added to the `config.in` file and the `-` indicates that the line should be deleted from `config.in`. Edit the `config.in` file accordingly and reapply the remainder of the `config.in.rej` file with the following command:

```bash
# patch -p0 < config.in.rej
```

If there are no errors reported, you can delete the `config.in.rej` file. It is not deleted automatically by patch. Next you can proceed with the configuration and compilation steps, as we have discussed in the “Configuring the Kernel” and “Compiling the Kernel” sections earlier in the chapter.

Installing patches out of order or applying non-standard patches is another reason for errors. If you continue to get more errors, it is better to start from scratch with a clean source tree that you have not modified in any way. For example, unpack the original `linux-2.2.12.tar.gz` that you used to build your current version. Run `make mrproper` to clean up the source tree and then apply `patch-2.2.13`.

### Cleaning Up After Patching

After patching source trees a few times, you will notice file names with `.orig` extensions starting to accumulate. You can remove these by running a find command as follows:

```bash
# cd /usr/src/linux
# find . -name '*.orig' -exec rm -f {} \;
```

An earlier version of patch created tilde files instead of `.orig` files. To remove these you can run the following find command instead:

```bash
# find . -name '*~' -exec rm -f {} \;
```

### Understanding Modules

Since Linux 2.0.x, modules have been introduced. These change the way kernels are built. In the past, any device driver or file system type that you needed access to had to be compiled into the kernel. For certain system configurations where the kernel had to occasionally support a lot of different devices, the kernel size would get very big, demanding a lot of system resources and resulting in performance degradation. To remedy this situation, modularized kernels were designed. This allows for building modules for infrequently used drivers or file systems. These modules can be loaded on demand, and later unloaded when they are no longer needed.

Good candidates for modules are a variety of Ethernet drivers, CD-ROM drivers, certain file system support drivers, and miscellaneous other modules.

Some changes in how modules are supported by the kernel have been made. In earlier kernels, a kernel daemon would load and unload modules on demand. In current kernels, `kerneld` has been replaced by `kmod`. `kmod` also loads and unloads modules on demand but does not require an external program to be running; it runs as a thread within the kernel. When the kernel needs a module to be loaded, kmod wakes up and spawns a modprobe process that actually loads the module.

kmod offers several advantages over kerneld, including the following:

- kmod does not require Sys V IPC support unlike kerneld. This allows Sys V IPC itself to become a module.
- Removing kerneld from Sys V IPC made it 40% smaller.
- kmod runs as a kernel thread unlike kerneld, which ran as a separate daemon.
- kmod reports errors using the normal kernel mechanisms, unlike kerneld which needed Unix domain sockets and thus could not be modularized.

To periodically unload unused modules, you can create a crontab entry for the root user as follows:

```
0-59/5 * * * * /sbin/rmmod -a
```

Add this line to the root user’s crontab file as outlined in Chapter 7, “Scheduling Tasks.”

In order for kmod to be able to spawn modprobe, the kernel must know the path to modprobe. This can be set using the /proc pseudo file system as follows:

```bash
# echo "/sbin/modprobe" > /proc/sys/kernel/modprobe
```

## UNDERSTANDING THE /proc File System

The /proc file system is a pseudo file system which acts as a window into the internal data structures of the kernel. It can be used to collect information about the kernel and also to modify certain kernel parameters at run time. If you change directory into /proc and do a directory listing, you will find one sub-directory per running process. To get information about a specific process you can list its various attributes, which appear as sub-directories and files within the process directory. Consider the following sample listing of the /proc file system.

```text
# ls /proc
1    304   421   441   476   bus        interrupts  misc      slabinfo
2    332   422   460   481   cmdline    ioports     modules   sound
22   355   423   467   482   cpuinfo    kcore       mounts    stat
251  377   424   468   5     devices    kmsg        net       swaps
262  379   425   469   540   dma        ksyms       partitions sys
276  388   426   470   541   filesystems loadavg     pci       tty
290  4     430   471   543   fs         locks       scsi      uptime
3    420   431   472   545   ide        meminfo     self      version
```

To look at information pertaining to the process with PID 1, list the contents of /proc/1:

```text
# ls /proc/1
cmdline  cwd  environ  exe  fd  maps  mem  root  stat  statm  status
```

If you want to view the status information for the init process (PID 1), view the contents of /proc/1/status:

```text
# cat /proc/1/status
Name:   init
State:  S (sleeping)
Pid:    1
PPid:   0
Uid:    0       0       0       0
Gid:    0       0       0       0
Groups:
VmSize:         1096 kB
VmLck:             0 kB
VmRSS:             0 kB
VmData:           32 kB
VmStk:             8 kB
VmExe:            24 kB
VmLib:          1000 kB
SigPnd: 0000000000000000
SigBlk: 0000000000000000
SigIgn: 7fffffffffd7d8fc
SigCgt: 0000000000002603
CapInh: 00000000ffffffff
CapPrm: 00000000ffffffff
CapEff: 00000000ffffffff
```

The information generated by /proc file and directory listings and file contents is similar to the types of data which can be reported with the ps command.

You can obtain a lot of information about your kernel by listing various subdirectories of the /proc file system. For example, to list the modules currently loaded by your system you view the contents of /proc/modules:

```text
# cat /proc/modules
ppp_deflate             40536   0 (unused)
bsd_comp                 3620   0 (unused)
```

### TUNING KERNEL PARAMETERS WITH /proc

A very useful feature of /proc is the capability to change kernel parameters. Of course, this can also be a dangerous privilege if not used with care.

To change a value you simply write the new value into the appropriate pseudo file in the /proc hierarchy. To make the change permanent you add this action to your system startup scripts so that every time the system reboots the kernel reinitializes with the new values you have supplied.

The files in /proc/sys can be used to tune certain kernel parameters. For instance, you can increase the size of the file table in the kernel by altering the contents of /proc/sys/fs/file-max and /proc/sys/fs/inode-max. As the following commands show, these files each contain a single integer number:

```text
# cd /proc/sys/fs
# ls
binfmt_misc  dquot-max  file-max  inode-max  inode-state  super-nr
dentry-state dquot-nr   file-nr   inode-nr  super-max
```
