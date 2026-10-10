**Table 3.1 (Continued)**

| Linux Directory | Tradeoff |
| :--- | :--- |
| `/opt` | The `/opt` directory is used to support the installation of add-on application software packages. The directory should reside under the root directory. |
| `/tmp` | The `/tmp` directory is used to support programs that require temporary file space that is volatile. It can reside under the root directory; but if temporary files grow quickly, then your root directory may run out of disk space. This can easily be the result of system or application core dumps. In addition, from a security perspective, the `/tmp` directory is readable, writeable, and executable by all users and applications. Therefore, a hacker may be able to upload and execute programs in the `/tmp` directory. Therefore, assigning it to another partition should be considered as an option. |
| `/usr` | The `/usr` directory is a shareable read-only data directory to allow Filesystem Hierarchy Standard (FHS)-compliant hosts access to the same information. It is the largest repository of data. The `/usr` directory contains user documentation, binaries, libraries, software header files, and X Window material and libraries. |
| `/var` | The `/var` directory contains system- and application-generated information as a result of spooling, logging, and system temporary files. The `/var` directory should be placed on a separate partition, if possible. It is normally a subdirectory underneath the root directory. The primary reason why it should be separate is due to the possible growth of the log files and user mailboxes. This approach would reduce the size of the root partition. |


![](bbox=[0.09, 0.57, 0.62, 0.71])

The recommended partitioning schema, first introduced in Chapter 2, represents the most common approach, as shown in Figure 3.6. This approach entails having two primary partitions and one extended partition. Figure 3.7 presents the same partitions using the Linux `fdisk -l` command. The two primary partitions support the Linux `root` partition and the Linux `swap` partition. The extended partition supports the `home` partition.

# EXERCISE 3.3: Adding a New VFAT Partition Type

For this exercise, you will enter the Linux `fdisk` command to add and implement a VFAT filesystem partition type. For the exercise, the secondary Small