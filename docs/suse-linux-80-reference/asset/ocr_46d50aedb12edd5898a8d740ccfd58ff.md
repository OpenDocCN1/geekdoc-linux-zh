> > **Tip**
> >
> > The boot sectors installed by LILO contain a byte sequence similar to that which is characteristic for boot sector viruses. Therefore, it is not unusual for DOS virus scanners to claim to have detected the AIRCOOP boot sector virus in files such as `/boot/chain.b` or `/boot/os2_d.b`.

+   - the heart of the LILO code, localized in `/boot/boot.b`
+   - a map file, normally `/boot/map`, where LILO enters the location of Linux kernels and other data during its installation
+   - optional: a message file, the contents of which are shown in the opening message preceding the LILO boot selection. It is usually located in `/boot/message` (or similar)
+   - the different Linux kernel and boot sectors that LILO should offer

> > **Caution**
> >
> > Any write access (even through file movements) to any of these files corrupts the map file, requiring you to reinstall LILO (see *Installation After Changing the Configuration* on page 103). This is especially important when changing kernels.

# LILO Locations

This section refers to the *first stage* of LILO mentioned above. Consider this general restriction: depending on the BIOS version on your computer, it may be required that the kernel image `/boot/vmlinuz` be located on the *first 1024 cylinders* of the hard disk. This can be achieved with a small extra partition that can be “mounted” in the directory `/boot`, all of which is located within the first 1024 cylinders.

For many BIOS versions still available, only these first 1024 cylinders can be accessed by the BIOS drivers during the boot phase. In most cases, only the *first two hard disks* can be used. If you have a very old BIOS, it is possible that the existence of (E)IDE hard disks could prevent your SCSI devices from booting.