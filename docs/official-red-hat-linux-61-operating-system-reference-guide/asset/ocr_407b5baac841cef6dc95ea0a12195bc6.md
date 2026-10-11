# ## D.2.1 Add a New Hard Drive

The simplest way to make room for Red Hat Linux is to add a new hard drive to the computer and then install Red Hat Linux on that drive. For example, if you add a second IDE hard drive to the computer, the Red Hat Linux installation program will recognize it as hdb and the existing drive (the one used by Windows) as hda. (With SCSI hard drives, the newly installed hard drive would be recognized as sdb and the other hard drive as sda.)

If you choose to install a new hard drive for Linux, you don't need to read any further. After starting the Red Hat Linux installation program, just make sure you tell it to install Linux on the newly installed hard drive (hdb, sdb) rather than the one Windows uses.

# ## D.2.2 Use an Existing Hard Drive or Partition

The next simplest way to make room for Linux is to use a hard drive or disk partition that is currently being used by Windows. For example, suppose that Windows Explorer shows two hard drives, C: and D:. This could indicate either that the computer has