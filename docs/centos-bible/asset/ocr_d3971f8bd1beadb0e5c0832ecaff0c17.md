# Installing CentOS 2

# Partioning with Disk Setup during Installation

During installation, you are given the opportunity to change how your hard disk is partitioned. It is recommended that you use the Disk Setup. The Disk Setup screen is divided into two sections. The top shows general information about each hard disk. The bottom shows details of each partition. Figure 2-2 shows an example of the Disk Setup window.

![](bbox=[0.13, 0.27, 0.84, 0.72])

For each of the hard disk partitions, you can see:

+   - **Device** — The device name is the name representing the hard disk partition in the `/dev` directory. Each disk partition device begins with two letters: `sd` for IDE disks or SCSI disks, `ed` for ESDI disks, or `xd` for XT disks. After that is a single letter representing the number of the disk (Disk 1 is `a`, Disk 2 is `b`, Disk 3 is `c`, etc.). The partition number for that disk (1, 2, 3, etc.) follows the letter.