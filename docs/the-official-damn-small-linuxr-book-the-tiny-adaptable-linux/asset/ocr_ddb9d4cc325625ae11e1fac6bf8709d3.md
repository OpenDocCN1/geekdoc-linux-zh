# NOTE

If you are planning to do a Frugal Lilo installation, you should also mark the Primary Linux partition as Bootable. Frugal Grub type installations use the the master boot record and so no such mark is necessary. You may wish to fully read the next two sections to better understand the differences before you commit your cfdisk setup. Of course, it is always easy to start cfdisk again solely for the purpose of marking a partition as bootable.

+   5. If you are sure you are ready to erase everything on your hard disk, choose Write and press Enter.
+   6. After the warning, if you still think it is a good idea, type yes and press Enter.
+   7. Choose Quit and press Enter to exit from Cfdisk.

Upon return of the DSL Install Options screen, select option 0 (Quit). This takes you to the system prompt where you can format the swap partition using the following command:

```
# mkswap /dev/hda1
```

Of course, the mkswap command needs to be adjusted if you did not choose the first hard drive for the swap partition. Because you have changed the partition table, you must reboot to continue with your installation options. Don't forget to boot as follows:

```
boot: install
```

You may need to add some boot options to the install command. For example, type install nopcmcia if you don't think that your computer hardware's PCMCIA interface is being properly detected and configured.

# Frugal Grub Hard Drive Install

If you want easy access to later change boot options, or if you have a typical pre-existing Windows installation, you should choose the Grub installation. This installation script provides an easy installation for most systems. If you have multiple drives, it is incumbent upon you to make the final edit required by your system for Grub.