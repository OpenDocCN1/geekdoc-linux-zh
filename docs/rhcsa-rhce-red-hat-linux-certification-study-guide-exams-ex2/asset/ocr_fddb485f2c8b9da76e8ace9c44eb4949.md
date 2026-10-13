Each partition is associated with a Linux device file. At least that is straightforward; for example, the device filename associated with the first logical partition on the first SATA drive is /dev/sda5.

A volume is a generic name for a formatted segment of space that can be used to contain data. Volumes can be partitions, RAID arrays, or those logical volumes associated with Logical Volume Management (LVM).

A filesystem is the way a volume is formatted to allow it to store files. For example, Red Hat uses the fourth extended filesystem (ext4) as the default format for its volumes. The standard way to access data in Linux is to first mount that filesystem onto a directory. For example, when the /dev/sda1 partition is formatted to the ext4 filesystem, it can then be mounted on a directory such as /boot. It is common to say something like “the /dev/sda1 filesystem is mounted on the /boot directory.” For more information, see Chapter 6.

# Separate Filesystem Volumes

Normally, you should create several volumes for RHEL 6. Even in the default configuration, RHEL is configured with at least three volumes, for a top-level root directory (/), a /boot directory, and Linux swap space. Additional volumes may be suitable for directories such as /home, /opt, /tmp, and /var. They're also suitable for any custom directories such as for web sites, dedicated groups of users, and more.

While it's important to configure the /boot directory on a regular partition, other directories can readily be configured on logical volumes or RAID arrays.

Dividing the space from available hard drives in this manner keeps system, application, and user files isolated from each other. This helps protect the disk space used by the Linux kernel and various applications. Files cannot grow across volumes. For example, an application such as a web server that uses huge amounts of disk space can't crowd out space needed by the Linux kernel. Another advantage is that if a bad spot develops on the hard drive, the risk to your data is reduced, as is recovery time. Stability is improved.

While there are many advantages to creating more volumes, it isn't always the best solution. When hard drive space is limited, the number of partitions should be kept to a minimum. For example, if you have a 4GB hard drive and want to install 3000MB of packages, a dedicated /var or even a /home volume could lead to situations where disk space runs out far too quickly.