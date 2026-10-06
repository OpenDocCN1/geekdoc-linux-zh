the two boot loaders are so similar, I describe GRUB Legacy first and in more detail; the upcoming section, "Using GRUB 2 as the Boot Loader," focuses on its differences from GRUB Legacy. In the following pages, I describe how to configure, install, and interact with GRUB Legacy.

# Configuring GRUB Legacy

The usual location for GRUB Legacy's configuration file on a BIOS-based computer is /boot/grub/menu.1st. Some distributions (such as Fedora, Red Hat, and Gentoo) use the filename.cfg rather than menu.1st. The GRUB configuration file is broken into global and per-image sections, each of which has its own. Before getting into details, though, you should understand a few GRUB quirks.

![](bbox=[0.143, 0.335, 0.243, 0.381])

GRUB Legacy officially supports BIOS but not EFI. A heavily patched version, maintained by Fedora, provides support for EFI. If you're using this version of GRUB, its configuration file goes in the same directory on the ESP that houses the GRUB Legacy binary, such as /boot/efi/redhat for a standard Fedora or Red Hat installation.

# GRUB Numerclature and Quirks

Listing 5.1 shows a sample GRUB configuration file. This file provides definitions to boot OSs--Fedora on /dev/sda5, Debian on /dev/sda6, and Windows on /dev/sda2. Fedora and Debian share a boot partition (/dev/sda1), on which the GRUB configuration resides.

# Listing 5.1: a sample GRUB configuration file /menu.conf

```
# grub.conf/menu.1st
#
# Global Options:
#ndefault=0
splash=/grub/bootimage.xpm.gz
#
# Kernel Image Options:
#title Fedora (3.4.1)
root (hd0,0)
kernel /vmlinuz-3.4.1 root=/dev/sda5 mem=4096M
initrd=/initrd-3.4.1
```