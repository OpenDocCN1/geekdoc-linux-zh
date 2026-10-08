# THE LINUX BOOT LOADER 55

```
# timeout until the start of the default image
timeout = 30

# Boot a Linux kernel from /dev/hda2
title= Linux Boot
root=(hd0,1)
kernel=(hd0,1)/boot/mlinuz-2.0.0

# Boot Windows NT OR DOS
title= Windows NT 3.5/DOS boot menu
root=(hd0,1)
makeactive=
chainloader=+1
```

3.2 A simple grub configuration.

The configuration file for grub is a regular text file, in either UNIX or DOS format (they differ in the encoding of line end: UNIX uses a line feed, DOS uses carriage return and line feed). Comments start with a number sign (#) in the first column.

grub has, like LILO, global and local options. Global options are for grub itself or all images. The global options are:

timeout=number
time that grub waits before it starts the default image.

default=number
Number of the default image. The count starts with zero, so that the default zero starts the first image in the grub configuration.

fallback=number
If GRUB can't start the chosen image it tries to start the fallback image. This will only work when the error occurs in grub and not in the already started system.

password=password_new_configuration
Without this entry every user can change images or create new entries. It is also possible to select a kernel without any restriction and start it with any parameters. This entry disables these functions until the correct password is entered. After that grub uses the new configuration file where you may have entered images for the single-user mode.