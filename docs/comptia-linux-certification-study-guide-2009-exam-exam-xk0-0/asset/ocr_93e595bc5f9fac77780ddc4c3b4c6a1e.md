The creation of a separation partition for log files will make it easy to backup, restore, secure, and provide remote access to external systems, if necessary.

■ **Volatile/temporary data** Computers and associated applications are constantly creating volatile and temporary data. In most systems, this data now resides on the partition storage device (not just in memory). This created temporary data is a result of the ability of the system and applications to read/write/and execute information located within the temporary directories and swap space. The Linux system automatically creates a swap partition. However, there are other directories (for example, /tmp) that traditionally reside underneath the root directory. These other directories can also outgrow the disk space capacity of the partition.

■ **System maintenance** The creation of separate partitions for system administration and maintenance purposes can also make the job easier – for example, the recovery of corrupted partitions and the backup and restoration of data.

For the Linux professional, the decision to create a partition or not to create a partition is a tough job. Clearly, a single-partition system is not a sound system design. However, partitioning of every directory is not feasible, either. Therefore, the Linux professional must find the mean between the two extremes. Table 3.1 provides more insight into the tradeoffs the Linux professional must make.

# **Table 3.1** Tradeoffs for Specific Linux Directories

| Linux Directory | Tradeoff |
| :--- | :--- |
| /swap | The Linux swap partition is used as swap space. It functions as virtual memory. The /swap directory is a predefined partition that has its own predefined filesystem. This directory provides additional memory to your system to run large programs. |
| /boot | The /boot directory contains files and configuration information needed during the Linux boot process. This includes the mini Linux kernel. The implementation of /boot under a different partition would make system rescues and repairs easier. |
| /home | The /home directory is normally implemented to host users’ account directories and user-specific files. The /home directory should be assigned a separate partition. The reason why this directory should be created on a separate partition is due to multiuser file space growth. In addition, performing backup and restore functions is a lot easier if dynamically changing user files reside on a separate partition. |
| **(Continued)** | |