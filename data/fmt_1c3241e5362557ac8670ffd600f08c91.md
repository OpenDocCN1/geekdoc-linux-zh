
## Task 2

Have a peek at `/boot/grub/grub.cfg`. This is a rather long file, but you should recognize parts of it if you have done Lab 28 and customized `GRUB` boot commands.

If you are running this on a Linux system that's already fully installed, the next step won't be necessary. However, if you ever wish to boot a secondary disk, you might need to run `grub-install` on that disk. `grub-install` installs `GRUB` to a disk's master boot record (MBR) so that a BIOS can boot it successfully.

## Task 3

Finally, reboot your computer/VM and see/hear your shiny new `GRUB` boot menu. From here you may hit `e` to edit boot commands or `c` to enter a command prompt, as in Lab 28.

## Answer 1

```
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=menu
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT=""
GRUB_CMDLINE_LINUX=""
GRUB_INIT_TUNE="480 440 1"
# This file must be placed in the /boot/grub directory first
GRUB_BACKGROUND="/boot/grub/image.png"
```

### Notes

There have been multiple common bootloaders, including `LILO` and `GRUB Legacy`. `GRUB2` is the most common and recommended bootloader today.
