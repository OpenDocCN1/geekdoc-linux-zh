# # Installing the Kernel and Setting Up GRUB 515

This command creates the file initrd-2.6.3-2.1.240custom.img in the /boot/ directory. You have to refer to this initrd file in the GRUB configuration file (/etc/grub.conf).

# ## Installing the Kernel and Setting Up GRUB

Fedora Core uses GRUB to load the Linux kernel from the disk. The configuration file (/etc/grub.conf lists the kernel binary file that GRUB runs. You can examine the contents of the GRUB configuration file by typing the following command:

```
cat /etc/grub.conf
```

Here is what I see when I run this command on one of my systems:

```
@ grub.conf
@ Note that you do not have a /boot after making changes to this file
@ NOTICE: This means that
@ all kernel and initrd paths are relative to /boot/, eg.
@ root=(hd0,2)
@ kernel/vmlinux-version root=/dev/hd5
@ @boot+=dev/hda
default=0
timeout=10
splashimage=(hd0,2)/grub/splash.xpm.gz
title Fedora Core (2.6.3-2.1.240)
root=(hd0,2)
vmlinux-2.6.3-2.1.240 root=LABEL=rhgb
initrd-2.6.3-2.1.240.img
title Windows XP
title rootoverify (hd0,1)
chainloader +1
```

Here's what the lines in /etc/grub.conf file mean (the lines that begin with # are comments):

+   - default=0: Specifies the first entry as the default that GRUB boots. If this line is set to 1, GRUB boots the second.
- timeout=10: Causes GRUB to boot the entry automatically after waiting for 10 seconds. If other boot entries are in the file, the user may select another from a boot menu GRUB displays.
- The four lines starting with title Fedora Core (2.6.3-2.1.240) constitute the first boot entry — and this entry defines a specific kernel file GRUB boot. You can make GRUB boot another kernel by adding a similar section to the configuration file. Here's the meaning of the lines in this entry:

![](bbox=[0.888, 0.315, 0.958, 0.465])