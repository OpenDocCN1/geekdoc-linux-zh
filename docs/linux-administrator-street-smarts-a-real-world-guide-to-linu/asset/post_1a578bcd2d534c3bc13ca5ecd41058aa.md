
# Listing 5.2: Sample lilo.conf File

```text
boot=/dev/hda
prompt
delay=40
map=/boot/map
install=/boot/boot.b
default=linux
lba32

message=/boot/message
image=/boot/bzImage-2.6.10
   label=linux
   root=/dev/hda9
   append="mem=256M"
   read-only

other=/dev/hda3
   label=windows
   table=/dev/hda
```

It’s possible to configure LILO to boot either of two or more kernels using the same distribution. This can be very convenient when you want to test a new kernel. Rather than eliminate your old working configuration, you install a new kernel alongside the old one and create a new `lilo.conf` entry for the new kernel. The result is that you can select either the old kernel or the new one at boot time. If the new kernel doesn’t work as expected, you can reboot and select the old kernel. This procedure allows you to avoid otherwise ugly situations should a new kernel not boot at all.

Assuming you don’t need to change kernel options or other features, one procedure for adding a new kernel to LILO is as follows:

- 1. Install the new kernel file, typically in `/boot`. Ensure that you *do not* overwrite the existing kernel file, though. You should have done this as part of the kernel recompilation in Phase 2.
- 2. Copy the stanza for the existing kernel file in `/etc/lilo.conf`. The result is two identical stanzas.
- 3. Modify the name (`label`) of one of the stanzas to reflect the new kernel name. You can use any name you like, even a numeric one, such as `26177` for the `2.6.17.7` kernel.
- 4. Adjust the `image` line in the new kernel’s stanza to point to the new kernel file.
- 5. If you want to make the new kernel the default, change the `default` line to point to the new kernel.

![](img/f430a19bdf014c43ad7c2d594afd5b21_251_0.png)

It’s generally best to hold off on making the new kernel the default until you’ve tested it. If you make this change too early and then can’t get around to fixing problems with the new kernel for a while, you might find yourself accidentally booting the bad kernel. This is normally a minor nuisance.

- 6. Save your `/etc/lilo.conf` changes.
- 7. Type `lilo` to install LILO in the MBR or boot partition's boot sector.

At this point, your new kernel is set up and ready to be tested, as described shortly in “Testing Your Changes.”

## Adding a Kernel to GRUB

LILO was designed expressly for Linux, but GRUB was designed with a broader set of OSs in mind. Thus, it does things a bit differently, which can be confusing at times. In particular, GRUB introduces a new way of referring to hard disks and their partitions. Rather than Linux device files, such as `/dev/hda` and `/dev/hda9`, GRUB uses strings of the form `(hd x, y)`, where `x` is a disk number and `y` is a partition number. (The `y` and preceding comma may be omitted to refer to an entire disk or its MBR.) Both the `x` and the `y` are numbered starting from 0, which contrasts with Linux’s numbering partitions starting with 1. Thus, Linux’s `/dev/hda9` is GRUB’s `(hd0,8)`. GRUB doesn’t distinguish between ATA and SCSI disks; `hd0` is the first disk recognized by the BIOS, `hd1` is the second disk, and so on.

Listing 5.3 shows a typical GRUB configuration file. Like the LILO configuration file, it consists of a series of global options followed by stanzas (beginning with the keyword `title`) for the OSs or kernels it boots. You should be able to figure out what most of these options mean, even if a few of them remain mysterious.

## Listing 5.3: Sample GRUB Configuration File

```plain
default=0
timeout=4

splashimage=(hd0,3)/grub/splash.xpm.gz

title Linux (2.6.10)
    root (hd0,3)
    kernel /bzImage-2.6.10 ro root=/dev/hda9 mem=256M
    boot

title Windows
    rootnoverify (hd0,1)
    chainloader +1
    boot
```

The procedure for adding a kernel to GRUB is very similar to the procedure to add a kernel to LILO:

- 1. Install the new kernel file, typically in `/boot`. Ensure that you do *not* overwrite the existing kernel file, though. You should have done this as part of the kernel recompilelation in Phase 2.
- 2. Copy the stanza for the existing kernel file in your GRUB configuration file. The result is two identical stanzas.

- 3. Modify the name (`title`) of one of the stanzas to reflect the new kernel name. You can use any name you like, but it’s typical to use a moderately long and descriptive name.

- 4. Adjust the `kernel` line in the new kernel’s stanza to point to the new kernel file. Note that the kernel file reference is relative to the GRUB root directory, which is specified by the `root` option. This will be the Linux root (/) directory unless you have a separate `/boot` partition, in which case the GRUB root directory is the Linux `/boot` directory. In Listing 5.3, the kernel is specified without the `/boot` directory name, so the system presumably uses a separate `/boot` partition.

- 5. If you want to make the new kernel the default, change the `default` line to point to the new kernel. GRUB numbers its stanzas starting with 0.

![](img/f430a19bdf014c43ad7c2d594afd5b21_253_0.png)

> It’s generally best to hold off on making the new kernel the default until you’ve tested it. If you make this change too early and then can’t get around to fixing problems with the new kernel for a while, you might find yourself accidentally booting the bad kernel. This is normally a minor nuisance.

- 6. Save your GRUB configuration file changes.

There’s no need to re-install your MBR code in the way you do with LILO. The existing GRUB MBR code should find your GRUB configuration file changes and implement them. If your GRUB installation is damaged and you’ve booted using an emergency disk, however, you can re-install GRUB using the `grub-install` command:

```
# grub-install (hd0)
```

This command installs the GRUB MBR code to the MBR of the first disk, `(hd0)`—normally `/dev/hda` or `/dev/sda`. If your setup is odd or complex, you may need to use the interactive grub utility instead. Consult its `info` page for details.

## Testing Your Changes

At this point, you should be able to test your changes. Shut down and reboot your computer. You should see your new kernel appear as a menu option (or as an option you can type at a `lilo:` or `boot:` prompt; in the case of simpler LILO configurations). Selecting this option should boot you into your new kernel. Once you’ve booted and logged in, type `uname -a`. This command produces a line or two of output summarizing various system information, including the kernel version number. Verify that the kernel version number matches what you expect. If it doesn’t, review your boot loader configuration to be sure you remembered to change the kernel filename.

If the kernel doesn’t boot, or if it begins to boot but then hangs before finishing, it’s possible that your boot loader configuration is incorrect. Reboot into your old kernel and check to be sure you didn’t introduce any typos, particularly in the `LILO root=` line or in the `GRUB root=` option on the `kernel` line. It’s also possible that your freshly compiled kernel is lacking a critical driver or filesystem. Remember that the kernel must be able to read your root (/) filesystem, which means it needs drivers for your disk controller and the file system you used on your root partition. If necessary, go back to Phase 2, review your kernel configuration, and recompile it.

If you’ve gotten everything working, then you may want to go back to the boot loader configuration procedures described earlier. For both LILO and GRUB, repeat the steps beginning with step 5 to make your new kernel the default. Thereafter, your system should boot into the new kernel. You might even want to delete or comment out old kernel configurations. This is particularly helpful if you upgrade your kernel regularly, to keep your boot loader configuration uncluttered.

## Criteria for Completion

To complete this task, you should have successfully added a new kernel (the one you compiled in Phase 2) to your boot loader’s configuration. This task requires you to identify which boot loader your system uses, modify its configuration file, re-install the MBR code (for LILO only), and test the configuration by rebooting into your new kernel.
