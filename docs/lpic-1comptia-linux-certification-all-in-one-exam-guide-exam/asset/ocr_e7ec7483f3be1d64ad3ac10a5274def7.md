+   16. You need to mount a USB flash drive on your Linux system. Given that your Linux system currently has one SATA hard drive installed, which device file represents the flash drive?
+   A. /dev/hdb
+   B. /dev/usb0
+   C. /dev/sdb
+   D. /dev/sda
+   E. /dev/sdc

+   17. Which type of backup backs up all files modified since the last full backup and does not flag the files as having been backed up?
+   A. Full
+   B. Incremental
+   C. Differential
+   D. Partial

+   18. You need to create a backup of /etc to a removable hard disk drive mounted at /mnt/USB. Which tar command will do this?
+   A. tar -cf /mnt/USB/backup.tar /etc
+   B. tar -xfv ~/backup.tar /etc
+   C. tar -xzcf /mnt/USB/backup.tar /etc
+   D. tar -cfv /mnt/USB/backup.tar ~/etc

+   19. You want to create a compressed cpio archive of all the files in the Projects directory within your home directory to /mnt/usbdrive/Projectsbackup.cpio.gz. Which command will do this?
+   A. cpio -ov ~/Projects | gzip > /mnt/usbdrive/Projectsbackup.cpio.gz
+   B. ls ~/ Projects | cpio -ovz | > /mnt/usbdrive/Projectsbackup.cpio.gz
+   C. ls ~/ Projects | cpio -ov | gzip > /mnt/usbdrive/Projectsbackup.cpio.gz
+   D. cpio -ovz ~/Projects > /mnt/usbdrive/Projectsbackup.cpio.gz

+   20. Which command can be used to create an image of your /dev/sda2 partition in the /mnt/usb/volback file?
+   A. dd if=/dev/sda2 of=/mnt/usb/volback
+   B. cp /dev/sda2 /mnt/usb/volback
+   C. dd if=/mnt/usb/volback of=/dev/sda2
+   D. dd if=/dev/sda of=/mnt/usb/volback

# Answers

+   1. B. The fdisk /dev/sdd command uses the correct syntax to create a partition the fourth SATA hard drive in your system.

+   2. B. Type 82 defines a Linux swap partition.