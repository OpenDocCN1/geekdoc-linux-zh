If you want to prevent access to the machine as described above, you can change the boot configuration to require a password before the kernel command line can be edited.

In the file /boot/grub/menu.lst, the line

**password** *seceret*

within the general options makes sure that the choices defined further below in the file (title SUSE SLES 10, etc.) can only be selected in unmodified form. The use of additional kernel parameters requires the password *`seceret`*.

As the graphical boot menu could be used to circumvent the password feature, it is automatically disabled.

GRUB can also handle MD5-encrypted passwords that are generated as follows:

```
gal0:~ # grub-md5-crypt
Password:
Retype password:
$1$FtTeKl$qaV.tOrzbg3EYAgVfNup40
```

This string can be copied to the file /boot/grub/menu.lst, with the following syntax:

**password** -md5 $1$FtTeKl$qaVtOrzbg3EYAgVfNup40

The parameter **lock** within a title section can be used to force the password query before these title entries can be selected.

```
title Floppy
lock
chainloader (fd0)+1
```

Selecting Floppy in the boot menu is now only possible after entering the password.