```
3053371392 bytes (3.1 GB) copied, 746.211 s, 4.1 MB/s
```

That's it! You can now boot into a Kali Live / Installer environment using the USB device.

Creating a Bootable Kali USB Drive on OS X

OS X is base on UNIX, so creating a bootable Kali Linux USB drive in an OS X environment is similar to doing it on Linux. Once you've downloaded and verified your chosen Kali ISO file, you use dd to copy it over to your USB stick.

WARNING: Although the process of imaging Kali on a USB drive is straightforward, you can just as easily overwrite a disk drive you didn't intend to with dd if you do not understand what you are doing, or if you specify an incorrect output path. Double-check what you're doing before you do it, it'll be too late afterward.

Consider yourself warned .

Without the USB drive plugged into the system, open a Terminal window, and type the command diskutil list at the command prompt.

You will get a list of the device paths (looking like /dev/rdisk0, /dev/rdisk1, etc.) of the disks mounted on your system, along with information on the partitions on each of the drives.

Plugin your USB device to your Apple computer's USB port and run the command diskutil list a second time. Your USB drive's path will most likely be the last one. In any case, it will be one which wasn't present before. In this example, you can see that there is now a /dev/disk6, which wasn't previously present.

Unmount the drive (for this example, the USB stick is /dev/disk6 — do not simply copy this, verify the correct path on your system!):

```
diskutil unmount /dev/disk6
```

Proceed to (carefully!) image the Kali ISO file on the USB device. The following command assumes that your USB drive is on the path