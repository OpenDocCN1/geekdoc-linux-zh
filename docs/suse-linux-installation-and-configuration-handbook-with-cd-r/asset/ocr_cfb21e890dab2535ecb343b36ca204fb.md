The following are not supported:

+   - Parallel port SCSI adapters
+   - Non-Adaptec-compatible DTC boards (327x, 328x)

# Hard Drives

Linux supports all hard drives, as long their controllers are supported. All direct access SCSI devices with a block size of 256, 512, or 1024 bytes should work. Other block sizes will not work. Large IDE (EIDE) drives work fine with newer kernels, but the boot partition must lie in the first 1024 cylinders because of PC BIOS limitations.

Some Conner CEP1060S drives might have problems with Linux and ext2fs. The symptoms are inode errors during e2fsck and corrupt filesystems. Conner has released a firmware upgrade to fix this problem, though.

# Tape Drives

Linux supports several tape drives. The following is a list of supported drives:

+   - SCSI tape drives
+   - Seagate Sidewinder 50 AIT (on ICP 6527 RAID-controller)
+   - QIC-02 drives
+   - Iomega DITTO internal (ftape 3.04c and newer)
+   - * QIC-117, QIC-40/80, QIC-3010/3020 (QIC-WIDE) drives

In addition to those drives listed previously, most tape drives using the floppy controller should work with Linux.

# ATAPI Tape Drives