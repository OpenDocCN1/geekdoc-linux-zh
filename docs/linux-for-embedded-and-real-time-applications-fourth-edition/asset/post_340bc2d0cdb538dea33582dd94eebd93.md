
The value of an environment variable is referenced by enclosing it in `{}`. An environment variable can contain one or more u-boot commands separated by `;`. Such a variable can be "executed" with the `run` command. A variable can also contain the `run` command, allowing it to execute other variables.

U-boot has a very extensive command set, much of which is detailed in Appendix A. For now, type help to see a complete list.

Note the message:

```
*** Warning - readenv() failed, using default environment
```

U-boot tries to read its environment from a NAND flash that is not installed on the BBB. That fails, and so it uses a default environment built into u-boot itself. One consequence of this is that we cannot permanently modify the default environment without modifying and rebuilding u-boot itself. We can, of course, modify variables each time we boot.

But note the variable `bootenv = uEnv.txt`. When u-boot has finished setting up the default environment, it reads the file specified by `bootenv` for additional instructions. This file resides in the eMMC’s boot partition that is visible in your workstation.

Issue the `boot` command to let Linux boot up. Mount the boot partition, and open `uEnv.txt` with an editor. The interesting piece is down at the end, the variable `uenvcmd`. This is the last variable u-boot executes, and so it should boot up the kernel in some fashion.

In the default case, `uenvcmd` loads three files from the eMMC: the kernel, the initial RAM disk image (initrd), and something called a *flattened device tree* (fdt). `mmcargs` sets the `bootargs` variable, which is passed to the kernel as it boots. The `bootz` command transfers control to the kernel, passing it the addresses of the initrd and fdt. So, to modify how the root file system gets mounted, we modify `uEnv.txt`, or perhaps better, supply a different one.

In your samples/ directory, open the file `uEnvnet.txt` and find `uenvcmd`. About the only thing that is different is it runs `netargs` instead of `mmcargs`. `netargs` sets up `bootargs` to specify the file system type as nfs, and provides the location of the server and path to the file system directory. Up around the middle of the file is a set of variables that define the address of the server and the path to the root file system, which you will probably want to change. Historically, I’ve always defined a fixed IP address for the target board. For some reason that does not work with the BBB, and so you see at the tail end of `netargs` `ip=dhcp`.

In principle, you should be able to write directly to the boot partition from your workstation, but I found that to be less than reliable. What I did was to create a directory on the BBB under `/home`, and then mount my workstation’s home directory there over NFS.

But, before you can do that, you have to install a package called `nfs-common`. Your BBB must be connected to the Internet. Then execute:

```bash
sudo apt-get update
sudo apt-get install nfs-common
cd /home
sudo mkdir doug
sudo mount -t nfs -o nolock 192.168.1.2:/home/doug doug
```

Of course, if you are logged in as root, you can drop the sudo. You might want to put the mount command into a shell script, as you may be executing it a number of times. Now you can copy `uEnvnet.txt` from the workstation to `/boot/uboot` on the BBB:

```bash
cp doug/samples/uEnvnet.txt /boot/uboot
sync
```

Always execute `sync` after changing the `/boot/uboot` directory, or your changes may not get to the flash before you reboot. I suggest you do not flat out replace the original `uEnv.txt` just yet and in fact, you might want to keep a copy of it.

## Differences Between Version 7.4 and Version 8.7

Now that we understand the boot process, I can say a little about the differences between Debian 7.4 and the latest release, 8.7. The principal difference I see between the two is in how the boot code is structured. As described above, version 7.4 splits the eMMC into two partitions, one for booting and one for the root file system. In version 8.7, there is only the ext4 root partition that includes the kernel image, the initrd, and device table files. The u-boot image is not visible. It is clearly there, but it is hidden.

The default u-boot environment has expanded substantially. In 7.4 it is 4.6 KB, and in 8.7 it is 20.5 KB. The intention is to make it easier to write `uEnv.txt` files, which is fine, but it also makes the default environment itself much harder to understand.

## The Root File System Image

Even though we will be mounting the root file system over NFS, you will need to load an `image` file to the eMMC in order to create a boot partition. But first you need to load the image file to a microSD card. A 4 GB card is sufficient. You should use a USB card reader, as there have been reports that the built-in readers on some laptops are not reliable under Linux. The card should show up as `/dev/sdb`. If not, you can execute:

```bash
dmesg | tail
```

just after inserting the card, and it should show what device was just recognized.

Browse to `debian.beagleboard.org/images` and download `BBB-eMMC-flasher-debian-7.4-2014-04-14-2gb.img.xz`. Uncompress the file with the `xz` command thus:

```
xz -d BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img.xz
```

This yields one file, `BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img`. Write this file to the microSD card with the `dd` command:

```
dd if=BBB-eMMC-flasher-debian-7.4-2014-03-26-2gb.img of=/dev/sdb
```

This will take a fairly long time. When it is finished, there will be two partitions on `/dev/sdb`; a bootable FAT partition named BEAGLEBONE, and an ext4 partition named eMMC-flasher. This image is specifically for flashing the eMMC.

Insert the microSD into your unpowered BBB. The BBB documentation says that to boot from the microSD card, you must hold down the boot pushbutton while applying power. In my case, the mere presence of a microSD card causes the board to boot from the card. Power it up. The kernel will boot up as normal, and present a login prompt. But the pattern of the LEDs indicates that something else is going on. That something else is flashing the eMMC. When the four LEDs come on steady, the flashing is finished. Power down the board, remove the microSD card and repower the board. It boots Debian 7.4 from the eMMC.

Finally, you need to get the target root file system on to your workstation under your home directory. You do not want to copy it from the microSD card, because that image is specifically intended for flashing the eMMC. What you can do is copy from the BBB eMMC over the network to your workstation. Create a subdirectory under your home directory to match what you specified for `rootpath` in `uEnvnet.txt`. Now copy the entire target file system into that directory. I suggest copying each top level directory separately, rather than everything in one big `cp -r` command. Note, incidentally, that there are several top level directories that are empty. You can just execute a `mkdir` command for these. A few directories require some special attention:

- `/boot` — Do not copy the `/uboot` directory. Just create an empty directory.
- `/dev` — You only want the part of `/dev` that is on the microSD card. The remainder of `/dev` is populated by a program called `udev`.
- `/home` — Do not copy your home directory that you mounted over NFS.

You will need to edit `/etc/fstab` as root user. There will be a line that looks something like this:

```
UUID=3bb11f04-4b37-49fd-a118-f1a71c14cf d7 / ext4 noatime,errors=remount-ro 0 1
```

Your UUID will probably be different. This line is trying to mount the root file system from a disk drive, which not surprisingly interferes with mounting over NFS. Just comment the line out and save the file.

## Boot to the NFS File System

Reset the board into the u-boot prompt if you are not already there. Execute the following commands:

```
setenv bootenv uEnvnet.txt
boot
```

The reason for not overwriting uEnv.txt right now is that there might be something wrong with your uEnv.txt, in which case you will need to boot back into the eMMC file system. When you are confident that uEnvnet.txt is working correctly, you can rename it uEnv.txt and boot directly into the NFS file system.

Interestingly, the boot up seems to be somewhat more verbose with the NFS file system than with the eMMC file system.

As a final step, move the samples/ directory into your target file system under /home.

## What Can Go Wrong?

It is not unusual to encounter difficulties when bringing up an embedded target board such as the BeagleBone Black, even though the designers have gone to great lengths to make the process as painless as possible. The most common problems fall into two broad categories. The first is the serial port. Make sure the baud rate is set correctly. This is generally not a problem, because 115 kbaud seems to be the default for minicom. A more common problem is not turning off hardware flow control.

Common networking problems include having Security Enhanced Linux enabled, and/or the firewall turned on. This will prevent the target from NFS mounting its root file system. As a starting point, disable SELinux, and turn off the firewall. Later on you can configure either of these features to allow NFS mounting, but still provide some level of protection.

Make sure the IP address is correct. Actually, this should not be a problem, because you will be getting an IP address through DHCP.

With the target board fully configured and connected to the workstation, we can turn our attention to the task of writing applications. That’s the subject of the next chapter.

## Resources

- beagleboard.org — web site for the BeagleBoard series of boards
- debian.beagleboard.org/images — A collection of root file system images for BeagleBoards.
