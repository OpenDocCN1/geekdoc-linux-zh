# OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-h` | Display available options |
| `-n` | Unmount without altering /etc/mtab |
| `-r` | Try to remount as read only if unmounting fails |
| `-t type` | Unmount only on the specified filesystem type |
| `-V` | Display the version number |

# EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `umount -t vfat /dev/hda3` | Unmounts the vfat filesystem contained on /dev/hda3 and mounted at /mnt/ |
| `/mnt/windoze` | windoze. |
| `umount /dev/cdrom` | Unmounts the CD-ROM drive by specifying the device name. |
| `umount /mnt/cdrom` | Unmounts the CD-ROM drive by specifying the mount point. |