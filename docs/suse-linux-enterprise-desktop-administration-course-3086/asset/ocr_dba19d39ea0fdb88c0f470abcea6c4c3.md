If you want to prevent access to the machine as described previously, you can change the boot configuration to require a password before the kernel command line can be edited.

In the /boot/grub/menu.lst file, the following line within the general options makes sure that the choices defined further below in the file (title SLED 10, etc.) can only be selected in unmodified form:

```
Password secret
```

The use of additional kernel parameters requires the password secret. Because the graphical boot menu could be used to circumvent the password feature, it is automatically disabled when the entry password appears in the configuration file.

GRUB can also handle MD5-encrypted passwords that are generated as follows:

```
da10:~ # grub-md5-crypt
Password:
Retype password:
$1$FTeTk1$qaV.tOrzbg3EYAgVfNup40
```

This string can be copied to the /boot/grub/menu.lst file with the following syntax:

```
password --md5 $1$FTeTk1$qaV.tOrzbg3EYAgVfNup40
```

The lock parameter within a title section can be used to force the password query before these title entries can be selected.

```
title Floppy
    lock
    chainloader (fd0)+1
```

Selecting Floppy in the boot menu is now only possible after entering the password. The parameter password can also be used in individual title entries to define a special password for those title entries.

Please note that the password feature only moderately enhances security because it does not prevent booting the computer from another medium, such as the SLED 10 rescue system, and then accessing the files on the hard disk.

![](bbox=[0.122, 0.713, 0.313, 0.791])

If you want to decide for each service (postfix, sshd, etc.) whether or not to start it during booting, use the confirm parameter at the boot prompt.

![](bbox=[0.047, 0.805, 0.234, 0.879])

# Exercise 11-1: Manage the Boot Loader

In this exercise, you practice booting into a shell and modifying /boot/grub/menu.lst.

Enter init=/bin/bash at the boot prompt, modify /boot/grub/menu.lst to require a password before kernel parameters can be modified, and test the new GRUB configuration.