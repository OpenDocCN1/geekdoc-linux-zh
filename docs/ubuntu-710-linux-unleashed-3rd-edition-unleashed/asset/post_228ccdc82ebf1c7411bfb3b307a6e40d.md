
## CAUTION

Before making any changes to your current, working kernel, make sure that you have a backup copy on a floppy disk. This will allow you to boot into your system with a known working kernel in case something goes wrong during configuration. The command to do this is as follows:

```
# mkbootdisk --device /dev/fd0 `uname -r`
```

This assumes that your floppy drive is /dev/fd0. (Here is a good shell script tip: the ` character tells the shell to execute what is within ` first and then returns that output as part of the input of the mkbootdisk command.) On this machine, the result is

```
# mkbootdisk --device /dev/fd0 2.6.7-1
```

This command will not be echoed to your screen, but it is what the system will execute.

- 2. Apply all patches, if any, so that you have the features you desire. See the previous section for details.

- 3. Back up the .config file, if it exists, so that you can recover from the inevitable mistake. Use the following cp command:

```
# cp .config .config.bak
```

## NOTE

If you are recompiling the Ubuntu default kernel, the /usr/src/linux-2.6/configs directory contains several versions of configuration files for different purposes. Ubuntu provides a full set of .config files in the subdirectory configs, all named for the type of system they were compiled for. For example, kernel-2.6.7-10.686-smp.config is a configuration file for a multiprocessor Pentium-class computer. If you want to use one of these default configurations as the basis for a custom kernel, simply copy the appropriate file to /usr/src/linux-2.6 and rename it .config.

- 4. Run the make mrproper directive to prepare the kernel source tree, cleaning out any old files or binaries.

- 5. Restore the .config file that the command make mrproper deleted, and edit the Makefile to change the EXTRAVERSION number.

## NOTE

If you want to keep any current version of the kernel that was compiled with the same code tree, manually edit the Makefile with your favorite text editor and add some unique string to the EXTRAVERSION variable. You can use any description you prefer, however.

- 6. Modify the kernel configuration file using make config, make menuconfig, or make xconfig—we recommend the latter.

- 7. Run make dep to create the code dependencies used later in the compilation process.

## TIP

If you have a multi-processor machine, you can use both processors to speed the make process by inserting -jX after the make command, where as a rule of thumb, x is one more than the number of processors you have. You might try a larger number and even try this on a single processor machine (we have used -j8 successfully on an SMP machine); it will only load up your CPU. For example,

```
# make -j3 bzImage
```

All the make processes except make dep will work well with this method of parallel compiling.

- 8. Run make clean to prepare the sources for the actual compilation of the kernel.

- 9. Run make bzImage to create a binary image of the kernel.

## NOTE

Several choices of directives exist, although the most common ones are as follows:

zImage—This directive compiles the kernel, creating an uncompressed file called zImage.

bzImage—This directive creates a compressed kernel image necessary for some systems that require the kernel image to be under a certain size for the BIOS to be able to parse them; otherwise, the new kernel will not boot. It is the most commonly used choice. However, the Ubuntu kernel compiled with bzImage is still too large to fit on a floppy, so a smaller version with some modules and features removed is used for the boot floppies. Ubuntu recommends that you boot from the rescue CD-ROM.

bzDisk—This directive does the same thing as bzImage, but it copies the new kernel image to a floppy disk for testing purposes. This is helpful for testing new kernels without writing kernel files to your hard drive. Make sure that you have a floppy disk in the drive because you will not be prompted for one.

- 10. Run make modules to compile any modules your new kernel needs.

- 11. Run make modules_install to install the modules in /lib/modules and create dependency files.

- 12. Run make install to automatically copy the kernel to /boot, create any other files it needs, and modify the bootloader to boot the new kernel by default.

- 13. Using your favorite text editor, verify the changes made to /etc/lilo.conf or /boot/grub/grub.conf; fix if necessary and rerun /sbin/lilo if needed.
