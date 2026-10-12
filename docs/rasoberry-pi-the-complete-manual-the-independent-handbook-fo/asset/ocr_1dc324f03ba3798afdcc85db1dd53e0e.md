# Projects

# Picking an external USB drive

Speeding up your Raspberry Pi by migrating the root filesystem to an external USB drive is a start, but what sort of device should you use for the best performance? With a USB thumb drive you can add flash storage up to 16GB without running into any significant problems (the larger the drive, the greater the current is required to read/write). Anything larger is expensive and unnecessary. If you're planning to use an external HDD, there are no power issues as it will have its own power supply. As ever, your choice should suit your project.

Below Having your filesystem on a USB stick is great for booting as well as performance boosts

![](bbox=[0.08, 0.7, 0.92, 0.98])

# Supercharge your Pi

# Configure fstab for fast performance

+   07 Upon restarting, the virtual filesystem will be mounted and /var/log on the RAM disk. Other directories that can be moved to RAM include:

```
```
tmpfs  /tmp    tmpfs     defaults,noatime,nosuid,size=512m    0 0
tmpfs  /run    tmpfs     defaults,noatime,nosuid,size=512m    0 0
tmpfs  /var/log  tmpfs     defaults,noatime,nosuid,nosuid,mode=0755,size=100m  0 0
tmpfs  /var/spool  tmpfs     defaults,noatime,nosuid,mode=0755,size=10m  0 0
tmpfs  /var/spool/queue  tmpfs     defaults,noatime,nosuid,mode=0700,gid=12,size=30m  0 0
```
```

Add each to /etc/fstab in nano.

# Move your OS to a HDD

+   08 If you're concerned about the lifespan of the SD card, why not reduce your Raspberry Pi's reliance on it! Instead of using the SD card as a sort of budget SSD, change its role and add a HDD or USB stick to run the operating system, leaving the SD card for bootstrapping. This can give a marked performance boost to the SD card.

# Back up the SD card

+   09 Create a copy of your Pi's SD card. Shut down, remove the card and insert it into your desktop computer. In the command line run:

```
```
sudo dd bs=4M if=/dev/sdb of=/backup.img
```
```

The path /dev/sdb represents the SD card. Copying takes 5-10 minutes. When complete, remove the SD card and connect your USB device.

# Copy Raspbian to USB

+   10 Using a blank Ex4-format ted USB thumb drive (or external-HDD) as the destination drive, enter:

```
```
sudo dd bs=4M if=/backup.img of=/dev/sdc
```
```

Leave the backup on your computer, just in case something goes wrong. With an SD card and USB storage device sharing an identical disk image, it's time to consider what you're going to do next -- create a faster Raspberry Pi.