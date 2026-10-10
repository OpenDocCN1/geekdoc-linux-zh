# Making a Bootable Recovery Disk

A boot disk is a basic recovery tool. To create a boot disk:

+   ▼ Copy the boot image on the CD. This image is called install-1.44, and is in a directory below / dists/progony/main/dskss-i386/ on the CD. Mount a floppy disk, then type: dd: if=PATH of=/dev/fd0 bs=1474560.

+   ▼ A floppy to use with a GRUB entry:

+   1 Mount the floppy.

+   2 Copy the kernel image to a floppy. Type: dd if=/boot/vmlinuz-2.2.18 of=/dev/fd0 bs=8192.

+   3 Make an entry for the floppy in /boot/grub/menu.lst. See “Basic Settings for a Floppy Drive in the GRUB Boot Manager,” page 380.

+   ▼ The utilities in the /tools directory of the CD to create a boot disk under Windows or DOS using raw write1 or rawwrite2.

# Configuring Networks

In Linux terms, the subject of networking includes not only a network of individual machines, but also internet connections.

This section covers the basics of Linux networking in Progeny Debian, starting with the hardware and how to configure a connection, and ending with how to configure e-mail:

+   ▼ Configuring an ethernet card.
+   ▼ Checking a modem connection.
+   ▼ Configuring a Network connection.
+   ▼ Configuring a Dialup connection.
+   ▼ Setting up electronic mail.