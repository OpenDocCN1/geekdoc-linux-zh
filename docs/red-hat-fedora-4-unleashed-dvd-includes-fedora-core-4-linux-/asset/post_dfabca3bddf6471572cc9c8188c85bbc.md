
high-speed broadband connection. (A typical compressed kernel source file is nearly 30MB for a download time of about 10 minutes on a 512Kb DSL connection; adjust accordingly for your connection.) Whether you are patching existing sources or downloading the full source, the end results will be identical.

Patching the kernel is not a mindless task. It requires the user to retrieve all patches from her current version to the version she wants to upgrade to. For example, if you are currently running 2.6.1 (and have those sources) and want to upgrade to 2.6.8, you must retrieve the 2.6.2, and 2.6.3 patch sets, and so on. Once downloaded, these patches must be applied in succession to upgrade to 2.6.8. This is more tedious than downloading the entire source, but useful for those who keep up with kernel hacking and want to perform incremental upgrades to keep their Linux kernel as up-to-date as possible.

To patch up to several versions in a single operation, you can use the patch-kernel script located in the kernel source directory for the kernel version you currently use. This script applies all necessary version patches to bring your kernel up to the latest version.

The format for using the patch-kernel script looks like this:

```
patch-kernel source_dir patch_dir stopversion
```

The source directory defaults to /usr/src/linux if none is given, and the patch_dir defaults to the current working directory if one is not supplied.

For example, assume that you have a 2.6.6 kernel code tree that needs to be patched to the 2.6.8 version. The 2.6.7 and 2.6.8 patch files have been downloaded from ftp.kernel.org and are placed in the /patch directory in the source tree. You issue the following command in the /usr/src/linux-2.6 directory:

```
# scripts/patch-kernel /usr/src/linux-2.6.6 /usr/src/linux-2.6.6/patch
```

Each successive patch file is applied, eventually creating a 2.6.8 code tree. If any errors occur during this operation, files named xxx# or xxx.rej are created, where xxx is the version of patch that failed. You will have to resolve these failed patches manually by examining the errors and looking at the source code and the patch. An inexperienced person will not have any success with this because you need to understand C programming and kernel programming to know what is broken and how to fix it. Because this was a stock 2.6.6 code tree, the patches were all successfully applied without errors. If you are attempting to apply a nonstandard third-party patch, the patch might likely fail. When you have successfully patched the kernel, you are ready to begin compiling this code tree as if we started with a fresh, stock 2.6.8 kernel tree.

## Using the patch Command

If you have a special, nonstandard patch to apply—such as a third-party patch for a commercial product, for example—you can use the patch command rather than the special patch-kernel script that is normally used for kernel source updates. Here are some quick steps and an alternative method of creating patched code and leaving the original code alone.

1. Create a directory in your home directory and name it something meaningful, like `mylinux`.
2. Copy the pristine Linux source code there with `cp -ravd /usr/src/linux-2.6/*/ ~/mylinux`
3. Copy the patch file to that same directory with `cp patch_filename ~/mylinux`
4. Change to the `~/mylinux` directory with `cd ~/mylinux`
5. Apply the patch with `patch -p1 < patch_filename > mypatch.log 2>&1` (This last bit of code saves the message output to a file so that you can look at it later.)
6. If the patch applies successfully, you are done and have not endangered any of the pristine source code. In case the newly patched code does not work, you will not have to reinstall the original, pristine source code.
7. Copy your new code to `/usr/src` and make that special symbolic link described elsewhere in the chapter.

## Compiling the Kernel

If you want to update the kernel from new source code you have downloaded, or you have applied a patch to add new functionality or hardware support, you will need to compile and install a new kernel to actually use that new functionality. Compiling the kernel involves translating the kernel's contents from human-readable code to binary form. Installing the kernel involves putting all the compiled files where they belong in `/boot` and `/lib` and making changes to the bootloader.

The process of compiling the kernel is almost completely automated by the `make` utility as is the process of installing. By providing the necessary arguments and following the steps covered next, you can recompile and install a custom kernel for your use.

Here is a checklist of steps to compile and configure the kernel:

1. Verify a working bootdisk for the old kernel to be able to reboot your system in case something goes wrong with the new kernel.

> **CAUTION**
>
> Before making any changes to your current, working kernel, make sure that you have a backup copy on a floppy disk. This will allow you to boot into your system with a known working kernel in case something goes wrong during configuration. The command to do this is as follows:
> `# mkbootdisk --device /dev/fd0 `uname -r``

This assumes that your floppy drive is `/dev/fd0`. (Here is a good shell script tip: the ` character tells the shell to execute what is within ` first and then returns that output as part of the input of the mkbootdisk command.) On this machine, the result is
`# mkbootdisk --device /dev/fd0 2.6.7-1`

This command will not be echoed to your screen, but it is what the system will execute.

2. Apply all patches, if any, so that you have the features you desire. See the previous section for details.

3. Back up the .config file, if it exists, so that you can recover from the inevitable mistake. Use the following cp command:
   `# cp .config .config.bak`

> **NOTE**
> If you are recompiling the Fedora Core default kernel, the `/usr/src/linux-2.6/configs` directory contains several versions of configuration files for different purposes.
> Fedora Core provides a full set of .config files in the subdirectory configs, all named for the type of system they were compiled for. For example, `kernel-2.6.7-1686-smp.config` is a configuration file for a multiprocessor Pentium-class computer. If you want to use one of these default configurations as the basis for a custom kernel, simple copy the appropriate file to `/usr/src/linux-2.6` and rename it .config.

4. Run `make mproper` directive to prepare the kernel source tree, cleaning out any old files or binaries.

5. Restore the .config file that the command `make mproper` deleted, and edit the Makefile to change the `EXTRAVERSION` number.

> **NOTE**
> If you want to keep any current version of the kernel that was compiled with the same code tree, manually edit the Makefile with your favorite text editor and add some unique string to the `EXTRAVERSION` variable.
> You can use any description you prefer, however.

6. Modify the kernel configuration file using `make config`, `make menuconfig`, or `make xconfig`—we recommend the latter, but read the “Choosing a Configuration Interface” section for details.

7. Run `make dep` to create the code dependencies used later in the compilation process.

### TIP

If you have a multiprocessor machine, you can use both processors to speed the make process by inserting `-jx` after the make command, where as a rule of thumb, x is one more than the number of processors you have. You might try a larger number and even try this on a single processor machine (we have used -j8 successfully on an SMP machine); it will only load up your CPU. For example, `# make -j3 bzImage`

All the make processes except make dep will work well with this method of parallel compiling.

8. Run `make clean` to prepare the sources for the actual compilation of the kernel.
9. Run `make bzImage` to create a binary image of the kernel.

### NOTE

Several choices of directives exist, although the most common ones are as follows:

- `zImage`—This directive compiles the kernel, creating an uncompressed file called zImage.
- `bzImage`—This directive creates a compressed kernel image necessary for some systems that require the kernel image to be under a certain size for the BIOS to be able to parse them; otherwise, the new kernel will not boot. It is the most commonly used choice. However, the Fedora kernel compiled with bzImage is still too large to fit on a floppy, so a smaller version with some modules and features removed is used for the boot floppies. Fedora recommends that you boot from the rescue CD-ROM.
- `bzDisk`—This directive does the same thing as `bzImage`, but it copies the new kernel image to a floppy disk for testing purposes. This is helpful for testing new kernels without writing kernel files to your hard drive. Make sure that you have a floppy disk in the drive because you will not be prompted for one.

10. Run `make modules` to compile any modules your new kernel needs.
11. Run `make modules_install` to install the modules in `/lib/modules` and create dependency files.
12. Run `make install` to automatically copy the kernel to `/boot`, create any other files it needs, and modify the bootloader to boot the new kernel by default.
13. Using your favorite text editor, verify the changes made to `/etc/lilo.conf` or `/boot/grub/grub.conf`; fix if necessary and rerun `/sbin/lilo` if needed.
14. Reboot and test the new kernel.
15. Repeat the process if necessary, choosing a Configuration Interface.

Over time, the process for configuring the Linux kernel has changed. Originally, you configured the kernel by responding to a series of prompts for each configuration parameter (this is the `make config` utility described shortly). Although you can still configure
