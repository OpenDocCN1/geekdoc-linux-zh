Tip

Red Hat also allows you to create and format RAID drives during installation. At that time, you can create your RAID partitions and devices.

# RAID Devices and Partitions: md and fd

A RAID device is named an md, and uses the MD driver. These devices are already defined on your Linux system in the /etc/dev directory, starting with md0. /dev/md0 is the first RAID device, and /dev/md1 is the second, and so on. Each RAID device, in turn, uses hard disk partitions, where each partition contains an entire hard disk. These partitions are usually referred to as RAID disks, whereas a RAID device is an array of the RAID disks it uses.