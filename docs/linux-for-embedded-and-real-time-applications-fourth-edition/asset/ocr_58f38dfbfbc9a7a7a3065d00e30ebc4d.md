Browse to `debian.beagleboard.org/images` and download `BBB-eMMC-flasher-debian-7.4-2014-04-14-2gb.img.xz`. Uncompress the file with the `xz` command thus:

```
xz-d BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img.xz
```

This yields one file, `BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img`. Write this file to the microSD card with the `dd` command:

```
dd if=BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img of=/dev/sdb
```

This will take a fairly long time. When it is finished, there will be two partitions on `/dev/sdb`; a bootable FAT partition named BEAGLEBONE, and an ext4 partition named eMMC-flasher. This image is specifically for flashing the eMMC.

Insert the microSD into your unpowered BBB. The BBB documentation says that to boot from the microSD card, you must hold down the boot pushbutton while applying power. In my case, the mere presence of a microSD card causes the board to boot from the card. Power it up. The kernel will boot up as normal, and present a login prompt. But the pattern of the LEDs indicates that something else is going on. That something else is flashing the eMMC. When the four LEDs come on steady, the flashing is finished. Power down the board, remove the microSD card and repower the board. It boots Debian 7.4 from the eMMC.

Finally, you need to get the target root file system on to your workstation under your home directory. You do not want to copy it from the microSD card, because that image is specifically intended for flashing the eMMC. What you can do is copy from the BBB eMMC over the network to your workstation. Create a subdirectory under your home directory to match what you specified for `rootpath` in `uEnvnet.txt`. Now copy the entire target file system into that directory. I suggest copying each top level directory separately, rather than everything in one big `cp -r` command. Note, incidentally, that there are several top level directories that are empty. You can just execute a `mkdir` command for these. A few directories require some special attention:

+   - `/boot` — Do not copy the `/uboot` directory. Just create an empty directory.
+   - `/dev` — You only want the part of `/dev` that is on the microSD card. The remainder of `/dev` is populated by a program called `udev`.
+   - `/home` — Do not copy your home directory that you mounted over NFS.

You will need to edit `/etc/fstab` as root user. There will be a line that looks something like this:

```
UUID=3bb11f04-4b37-49fd-a118-fla71c14cf d7 / ext4 noatime,errors=remount-ro 0 1
```

Your UUID will probably be different. This line is trying to mount the root file system from a disk drive, which not surprisingly interferes with mounting over NFS. Just comment the line out and save the file.