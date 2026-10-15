These days, prices on hard drives are so low, they’re insane, so don’t skimp. Better to have too much space than not enough. You can always fill it, but buying yet another drive is a hassle.

You can also invest in a SCSI card. (You can get a good deal for $40 or less, and most SCSI cards work well in Linux.) SCSI drives as a rule are more expensive than IDE drives, but they can also be easily mounted in an external case, something you would never want to do with an IDE drive.

# Allocating Drive Space

Now that you have gigabytes upon gigabytes of free space, you have to choose what to do with it.

You can stick with 2GB virtual disks. They’re easy to make, because when they expand they probably won’t always consume the full 2GB, and they’re also the most well-supported form of storage in VMware. Because the virtual machine’s IDE and SCSI controller can combine to give you 22GB of storage, that might be enough.

# Raw Disks

If you need more than 2GB in your virtual machine and you don’t want to do it by attaching loads of 2GB virtual drives, you have a couple of other options. I mentioned raw disks in an earlier chapter. When you use raw disks, you give VMware direct control of a real hard drive and real hard drive partitions. This is more difficult to configure (discussed in Appendix A, “Advanced VMware Configuration”) but provides a speed gain as well as the ability to break the 2GB-per-partition barrier.

Not only is raw disk support more complicated to set up than disk images, but it is also considered experimental on SCSI drives. You should familiarize yourself with VMware using virtual disks before you attempt to set up raw disks, especially on SCSI drives.

If you do decide to set up a raw disk, it’s probably easiest to start with a newly installed hard drive or at least one that can be completely erased and dedicated to VMware. Not only is it easier to work with and less heartbreaking if you make a mistake, but also it allows you to set up the first, primary partition as a Windows boot drive for a Windows virtual machine. Windows insists on booting from the first partition on a drive.