# Figure 6-13  Using a password in the GRUB configuration file

![](bbox=[0.33, 0.05, 0.95, 0.37])

can select a menu item too, you need to add the lock parameter within the appropriate title elements in the GRUB configuration file, as shown in this example:

```
```bash
fs2:~ $ cat /boot/grub/menu.lst
# Modified by YaST2. Last modification on Wed Jan 19 10:37:45 MST 2011
# THIS FILE WILL BE PARTIALLY OVERWRITTEN by perl-Bootloader
# Configure custom boot parameters for updated kernels in
/etc/sysconfig/bootloader

default 0
timeout 8
##YaST - generic_mbr
gfxmenu (hd0,1)/message
##YaST - activate
password natsas80l

###Don't change this comment -- YaST2 identifier: Original name: linux###
title Desktop -- openSUSE 11.3 -- 2.6.34-12
  lock
  root (hd0,1)
  kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 resume=/dev/sda1
  splash=silent quiet showopts vga=0x317
  initrd /boot/initrd-2.6.34-12-desktop
###Don't change this comment -- YaST2 identifier: Original name: failsafe###
title Failsafe -- openSUSE 11.3 -- 2.6.34-12
  lock
  root (hd0,1)
  kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 showopts sppm=off
  nomresume edd=off powersaved=off nohz=off highres=off processor.max_cstate=1
  nomodeset x11failsafe vga=0x317
  initrd /boot/initrd-2.6.34-12-desktop
###Don't change this comment -- YaST2 identifier: Original name: floppy###
title Floppy
  lock
  rootnoverify (fd0)
  chainloader +1
fs2:~ $ ```
```