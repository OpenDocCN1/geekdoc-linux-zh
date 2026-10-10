functions. This means that if you install Linux on a notebook, and you find a partition that looks like this to the Linux fdisk command:

```
282 838 13680a0 IMK ThinkPad hibernation /dev/hda4
```

you should leave it alone! This example is a save-to-disk partition used to support a notebook that has 128MB of RAM, and it’s designed to hold the contents of the memory during hibernation. Other save-to-disk schemes might have the contents of memory saved to a specific file on a Windows partition. One common DOS utility used in conjunction with the creation and management of these files and partitions is the Phoenix PHD disk.EXE command.

If hibernation operations do not work on your notebook, despite having an APM-compatible BIOS and using an APM-enabled Linux kernel, suspect the absence of this hibernation file or partition. You can generally re-create this partition or file by booting your notebook with a DOS diskette and then running the PHD disk utility.

Another source of problems, according to Tuxtops, a Linux laptop distributor, can be the XFree86 X11 server, which can lock up systems using a Mach64 chipset. This problem exists on notebooks such as various Dell Inspiron models. One workaround, according to Tu xtops, is to use the chvt command before issuing a suspend. Another fix is to install a modified X11 server by Steve Hsieh, found at http://www.eecs.umich.edu/inspiron.

# # Tracking Time Between Suspends and Hibernation

Time can be very important, and for mobile Linux users, having the correct time set on your notebook can be critical. There are two types of time on a notebook: the hardware time, maintained by your notebook’s power and internal batteries; and the system time, maintained by the Linux kernel.

The Linux APM driver updates the Linux system time from your notebook’s hardware clock when recovering from a suspend or hibernation. However, there might be instances in which, depending on how you configure APM, the driver might not be able to properly update the system. If you need to obtain the correct or hardware time for your system, and you’re not on a network, you can use the hwclock command. For example, to see the hardware time, use hwclock and its --show option:

```
Wed Mar 1 21:30:01 2000 -0.349767 seconds # hwclock --show
```