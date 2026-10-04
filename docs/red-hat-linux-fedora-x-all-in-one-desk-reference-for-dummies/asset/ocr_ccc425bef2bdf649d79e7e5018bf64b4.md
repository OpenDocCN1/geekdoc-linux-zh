# Partitioning the Disk for Fedora Core

Select the appropriate option and click Next. For example, if you select the first option, the Fedora installation program displays a dialog box to confirm your choice and to point out that all data in the existing Linux partitions will be lost. Click Next to continue. The installation program shows the partitions it has prepared, as shown in Figure 2-6. The exact appearance of the screen depends on your hard disk's current partitions.

This Disk Setup displays a list of disk drives and the current partition information for one of the drives. If you want to accept these partitions as is, click Next to proceed.

If your PC doesn't have enough memory (typically less than 128MB), the installer asks if you can write the partition title and activate the swap partition. After you do this, your hard disk partitions are changed. Click Yes only if you are committed to the new partitions and definitely want to install Fedora Core.

![](bbox=[0.135, 0.303, 0.225, 0.403])

![](bbox=[0.25, 0.423, 0.86, 0.803])

**Figure 2-6** Disk partitions created by the Fedora Core installer.

| drive:dev/sda (28616 MB) (Model: FUJITSU MHR200AT) | | | | |
|---|---|---|---|---||
| sda1 | | | 512 | | |
| sdb1 | | | 20638 | 7134 | |
| New | Edit | Delete | Reset | RAID | LVM |
|---|---|---|---|---|---||
| Device | Mount Point/Volume | Type | Size | RAID (MB) | Start End |
| Hard Drives | | | | | |
| /dev/sda | | | | | |
| | /dev/sda1 | | vfat | 51 | 4 |
| | /dev/sda2 | | nfs | | 20638 | 2645 |
| | /dev/sda3 | /boot | ext3 | 102 | 2646 | 2646 |
| | /dev/sda4 | Extended | | 7984 | 2649 | 3689 |
| | /dev/sda5 / | | | 7334 | 2649 | 3583 |
| | /dev/sda6 | swap | | 510 | 3584 | 3684 |
| Hide RAID device/LVM Volume Group members | | | | | |