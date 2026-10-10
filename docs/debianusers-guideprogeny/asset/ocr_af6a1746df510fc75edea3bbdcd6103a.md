# Column Settings in /etc/fstab (Mounting Filesystems)

| Column | Contents | Choices |
| :--- | :--- | :--- |
| 5 | Whether the filesystem should be backed up when the dump command is used. | **0:** The device is not backed up<br>**1:** The device is backed up.<br>Since **dump** is not often used today, most filesystems can be set to 0. |
| 6 | The order in which filesystems are checked for errors when the system starts. | **0:** No check is done. This option can start the system faster.<br>**1:** The device is checked first. The root partition should always use this setting.<br>**2:** The device is checked after any filesystems set to 1. |

# Mounting Filesystems Temporarily

+   1  If necessary, log in as root.
+   2  If necessary, create the directory needed for the mount point using the **mkdir** command.
+   3  If the kernel does not currently support the type of filesystem, enable support. Type: **modprobe -t TYPE**.