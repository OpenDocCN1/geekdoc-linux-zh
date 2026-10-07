# ## Dedicated Linux Hard Disk

With a dedicated Linux installation or a Linux boot by default (and despite other operating systems on the hard disk), the Master Boot Record can be replaced with the Linux LILO boot sector. LILO will then boot straight into Linux from the Master Boot Record without touching partition boot sectors. In some cases, though, you may have to explicitly specify the boot sector, at the boot: prompt you may have to specify `boot=/dev/hda` (or whichever device holds the modified Master Boot Record) if the default values do not work.

> **WARNING**

If you replace the Master Book Record with LILO for a dedicate Linux system and then later remove Linux, you will have to low-level format the hard drive or restore the old MBR before the drive can be used by another operating system such as DOS.

To install LILO as a dedicated Linux boot, follow these steps:

+   1. Boot Linux as usual. Make sure you have a boot floppy disk in case of problems.
2. Copy your existing Master Boot Record to a floppy in case of problems. The command to copy the MBR from the main drive (`/dev/hda`) to a floppy using 512 character blocks (the default) is
   ```
   dd if=/dev/hda of=/fd/MBR bs=512 count=1
   ```
3. Use the setup or LILO installation program to copy LILO into the boot sector, setting LILO in the Master Boot Record.
4. Reboot the machine to boot from the Master Boot Record.

Your machine should load Linux automatically. If Linux does not boot, use your boot floppy to start Linux and either repeat the process or restore the original Master Boot Record from the floppy using the following command:

```
```
dd if=/fd/MBR of=/dev/hda bs=446 count=1
```
```

# ## Using BOOTACTV

A slight modification of the last boot process is replacing the MBR with a utility called BOOTACTV which prompts for the partition to boot from. This requires a non-DOS-compatible copy of the boot sector to be written, so it should be used only when Linux will be the dominant operating system and when LILO is not booting the other operating systems properly.