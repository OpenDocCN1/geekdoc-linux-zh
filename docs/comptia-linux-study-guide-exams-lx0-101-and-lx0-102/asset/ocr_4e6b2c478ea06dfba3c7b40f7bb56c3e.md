19. What filesystem options might you specify in /etc/fstab to make a removable disk (USB flash drive, Zip disk, floppy disk, and so on) mountable by an ordinary user with a UID of 1000? (Select three.)

+   A. user

+   B. users

+   C. owner

+   D. owners

+   E. uid=1000

20. What is the minimum safe procedure for removing a USB flash drive, mounted from /dev/sdb1 at /media/usb, from a Linux computer?

+   A. Type umount /media/usb, wait for the command to return and disk-activity lights to stop, and then unplug the drive.

+   B. Unplug the drive, and then type mount /media/usb to that Linux registers the drive's removal from the system.

+   C. Unplug the drive, and then type sync /dev/sdb1 to flush the caches to ensure problems don't develop.

+   D. Type usbdrive-remove, and then quickly remove the disk before its activity light stops blinking.

+   E. Type fsck /dev/sdb1, wait for the command to return and disk-activity lights to stop, and then unplug the drive.