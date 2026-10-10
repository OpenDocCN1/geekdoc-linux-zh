
## Setting OS Boot Options

The two OS definitions in Listing 1.1 both begin with the keyword `title`, which provides a label for the OS that's displayed by GRUB when it boots. Subsequent lines may be indented to help distinguish between the OS definitions, but this indentation is optional. Important features of OS definitions include the following:

- **Root partition**: The `root` option identifies the GRUB root partition, which is the partition on which the GRUB configuration files reside. If you did not set aside a separate partition for `/boot` when you installed Linux, this line will identify the Linux root (`/`) partition, and subsequent file references will be relative to the Linux root partition. If you used a separate `/boot` partition, though, chances are the GRUB root partition will be the Linux `/boot` partition, and GRUB references to files in Linux's `/boot` directory will omit that directory name. Listing 1.1 identifies the GRUB root partition as `(hd0, 3)`, which is `/dev/hda4` on a PATA system.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_51_0.png)

GRUB can read files from several filesystems, including ext2fs, ext3fs, ReiserFS, FAT, and FFS. You can use any of these filesystems as your GRUB root partition. If you want to use another filesystem, such as JFS or XFS, as your Linux root partition, you should split off your GRUB root partition from the Linux root partition.

- **Linux kernel**: The `kernel` option identifies a Linux kernel or a kernel for certain other Unix-like OSs, such as a GNU Hurd kernel. This reference is relative to the GRUB root partition, as defined by `root`. You can also pass kernel options on this line. Note that the `root` option passed to the Linux kernel identifies the Linux root partition using a Linux device filename, but the `root` option in the GRUB OS definition identifies the GRUB root partition. The two might be the same, but they might not be. In the case of Listing 1.1, they aren't the same—the GRUB root partition is `(hd0, 3)`, or `/dev/hda4`, whereas the Linux root partition is `/dev/hda9`. Chances are `/dev/hda4` is the Linux `/boot` partition. The `ro` option passed on the kernel line tells the kernel to mount the root partition in read-only mode initially, just as the `read-only` line does in `lilo.conf`.

- **Root partition without verification**: The `root=noverify` option works just like the `root` option, except that it tells GRUB it shouldn't try to access files on the partition in question. It's most often found when booting non-Linux and non-Unix OSs, such as DOS or Windows.

- **Chain loader**: The `chainloader +1` line in Listing 1.1 tells the system to load the first sector of the root partition and pass execution to it. This option is common when booting DOS, Windows, or other OSs that place boot loader code in their boot sectors.

- **Boot directive**: The `boot` line tells GRUB to actually boot the kernel or boot sector for the OS in this definition. In practice, it can often be omitted.

In order to boot, the GRUB boot loader code must reside in the MBR, the boot partition's boot sector, or a floppy disk. You can do this by using the `grub` utility, which you launch from a text-mode login or `xterm`:

```bash
# grub
grub> root (hd0, 3)
grub> setup (hd0)
grub> quit
```

These commands set the GRUB root partition (the same as the one defined in your `menu.lst` or `grub.conf` file), install the boot loader code to the MBR of the hard disk (that is, to `hd0`), and exit from the utility. If you want to install the boot loader to a partition, you'd use `setup (hd0,3)` or some other partition identifier rather than using `setup (hd0)`. The `grub-install` program provides a simplified method of performing these steps:

```bash
# grub-install /dev/hda
```

This command installs GRUB to the MBR of the first disk. It should be able to locate the GRUB root partition automatically.

If you installed a distribution that uses GRUB by default, you shouldn't have to perform any of these steps; GRUB should already be installed and working. You might need to reinstall GRUB from an emergency boot system if it becomes corrupted, though, and you might want to replace the installed system if you learn of a serious GRUB bug. If you just want to add a new kernel or OS to your existing GRUB installation, you do *not* need to reinstall the boot loader code; you need only edit the `menu.lst` or `grub.conf` file.

### Adding a New Kernel or OS to GRUB

You can add a new kernel or OS to GRUB by copying an existing entry (or using one in Listing 1.1 as a model) and modifying it to suit your needs. When trying a new kernel, don't replace your old kernel; instead, add the new kernel to the `/boot` directory, and add a description of the new kernel to the GRUB configuration file. Remember to change the `title` line so that you can tell your two kernels apart. When you reboot the computer, you should be able to select the new kernel or OS from the list; there's no need to reinstall the GRUB boot loader code using the `grub` or `grub-install` tool.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_52_0.png)

## Troubleshooting Boot Problems

Linux normally boots correctly immediately after installation; however, sometimes it doesn't. What's more, boot problems can develop after installation. Knowing how to handle such problems can be a necessary skill. You can interact with GRUB to enter options at boot time and use rescue discs to modify your working system. You can use several different methods to reset the root password, should you forget what it is—an extremely important skill, should the need arise! Finally, you can examine boot messages to help identify and debug boot problems.

### Setting Kernel Options in GRUB

When GRUB loads, it normally presents a series of kernel and OS options, as defined in the `menu.lst` or `grub.conf` configuration file. You highlight the line with the title of the kernel or OS you want to boot and press the Enter key to boot.

Rather than accept the default options, though, you can edit them: instead of pressing the Enter key, you can type `e` (without pressing Enter) to edit the entry. Once you do this, GRUB presents the options from the configuration file related to the entry you've selected. You can use the keyboard's arrow keys to select a line and then type `e` again to edit that line. Alternatively, you can type `0` or `o` to create a new blank line before or after the selected one. Once you've made any changes you desire, type `b` to boot the entry.

> When you edit a GRUB entry during the boot process, the changes you make are temporary. If you want to make permanent changes, you must edit the configuration file as described earlier in “Configuring GRUB.”

Ordinarily, Linux boots into a full multiuser mode in which any authorized user may log in. Sometimes, though, you may want Linux to boot into a simpler mode in which just the root user may access the system. This single-user mode is useful for performing recovery and system maintenance tasks because the processes run by ordinary users, including system software that may run automatically when the system boots in the normal multiuser mode, can interfere with maintenance tasks such as low-level disk checks. To enter single-user mode, follow these steps:

1. Select the Linux entry you want to boot in the GRUB menu.
2. Type `e`, as described earlier, to edit the entry.
3. Select the line that begins with the word `kernel` and type `e` to edit it.
4. Use the arrow keys to move to the end of the line.
5. Press the spacebar, type `single`, and then press the Enter key to accept this change. (Typing 1 will also work.)
6. Type `b` to begin booting the system.

When the computer boots, it will boot directly into a text-mode root Bash prompt. You can use this prompt to change configuration files or otherwise manage the system. When you’re done, you can reboot the system or type `telinit 2`, `telinit 3`, or `telinit 5` to start normal system services. (Which number you type depends on your distribution. The `telinit` command is described in more detail in Chapter 4, “Managing System Services.”)

![](img/9903a4d3f7abd8dcbef1035fa04a3406_54_0.png)

> If your system boots normally, you may enter single-user mode from a normal boot by typing `telinit 1` at a root Bash prompt. Using GRUB to enter single-user mode is most useful if the system doesn’t boot normally.

## Using Rescue Discs

If Linux won’t boot at all, even into single-user mode, you can use a Linux rescue disc to boot a working Linux installation and use it to recover your normal system. Rescue discs are available on CD-ROMs, DVD-ROMS, USB flash drives, and other removable media. They enable you to boot from the removable medium and make changes to your nonworking installation on your hard disk. Examples of Linux rescue discs include the following:

- **Your distribution’s installation media**: Most distributions’ installation media include some form of rescue mode. Check your documentation, or study the options presented by the boot disc when you boot it. Sometimes distributions provide a separate rescue disc, so you may want to check your distribution’s Web site.

- **Knoppix**: This package, based at http://www.knoppix.net, is a full-fledged Linux installation based on Debian. You can download images that can be burned to CD-R or DVD-R media. Once booted, Knoppix is an unusually complete Linux system, although it’s rather sluggish when run from optical media.

- **SystemRescueCd**: This package is a dedicated rescue system available as a CD-R image. In many respects it’s similar to Knoppix, but it’s targeted explicitly as a rescue system, whereas Knoppix serves a broader purpose. SystemRescueCd is based on Gentoo Linux. Check http://www.sysresccd.org/Main_Page for more details.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_54_1.png)

> You can use a rescue disc that’s based on a distribution other than the one you use—for instance, Knoppix works fine to recover a Fedora system. Some files’ ownership may seem to change when you use a rescue disc, though. Don’t try to correct such changes, since they’re probably artifacts of different configurations of the rescue disc and your normal installation.

Once your rescue disc boots, you’ll probably be presented with a root shell, in either a text-mode session or a GUI login. The rescue disc might or might not detect and mount your normal Linux system, so you may need to perform this task manually. (Chapter 6 describes how to do this.) Once your normal system is mounted, you can edit configuration files to overcome whatever problem is preventing your normal installation from booting.
