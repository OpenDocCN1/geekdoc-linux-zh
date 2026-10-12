Because autofs is started at boot time and controls the automount daemon, simply do not run autofs. Use the checkconfig, ntsysv, or GUI clients to edit the startup scripts for your runlevel (see Chapter 14, “Automating Tasks,” for details).

# ## Relocating a File System

Many home users start with a single disk partition that mounts not only the root file system files, but also all the other files. Although this might work quite well for most home users, there might come a time when the physical disk becomes full. Adding another drive and moving part of the file system there is not difficult, but it is the source of many questions from new Linux users. This section of the chapter explains how to do this kind of file system relocation.

In this example, we will install a new IDE hard drive to /dev/hdb (the primary slave drive), create a single partition on it, format it as an ext3 file system, and move all of the user files located in /home to it. Once done, we will make it mount, by default, at the /home mount point by editing the /etc/fstab file.

# ### Installing the New Drive

First, physically install the drive, making certain that the master/slave jumpers are set correctly to set the drive as a slave drive. Also be certain that the jumpers are set correctly on the existing master drive. (Some drives require a different jumper setting, depending on whether they are a single master drive or a master drive with a slave drive; others offer a “cable-select” option to automatically set the drive status.) Failing to ensure that the jumpers are set correctly is a common error made even by people who are familiar with computer hardware.

After you have installed the drive, it must be correctly detected by the BIOS. Many modern BIOSes have an autodetect feature, or you can manually enter the drive CHS information in the BIOS (found on the drive label or documentation).

> **NOTE**
> 
> Linux can ignore the BIOS-provided CHS information and use information that you provide when loading the kernel, passing it as a kernel argument. Although this is a very powerful Linux option, it is now only used when working with obsolete BIOSes from more than three or four years ago and when you are attempting to use a hard drive that is larger than the BIOS was designed to address. In these cases, the CHS information helps the bootloader program know where the kernel is on the disk and helps the kernel understand how the data on the drive is organized, enabling Linux to make older hardware remain useful long after it has become obsolete. For more detailed information, you can look at the Large Disk HOWTO and the BootPrompt HOWTO if you have problems with drive geometry and the BIOS.

Most modern large drives use the LBA setting (Logical Block Addressing) to deal with the BIOS size limitations. If the drive is not detected, check the power connection, the IDE cable connection (the red stripe usually goes next to the power connector, but always