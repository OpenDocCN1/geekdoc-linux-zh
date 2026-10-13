| **TABLE 12.6 CONTINUED** |  |
|---|---|
| **lilo.conf File Entry** | **Description** |
| `message = /boot/message` | Contains the information that is to be displayed to the screen after LILO is run. |
| `default = name` | Image specified here is the default boot image. The first image listed in `/etc/lilo.conf` is the default if this option is omitted. |
| `image = /vmlinuz-pc97-2.2.14-modular` | The name of the Linux kernel. |
| `label = linux` | This label (name) is displayed at the boot prompt if the Tab key is pressed. It is used to distinguish between options if more than one OS is available to boot. |
| `root = /dev/hda1` | The root filesystem resides on the first partition of the first IDE drive. |
| `vga = 274` | Selects the display mode to be used when booting. |
| `read-only` | The root filesystem is mounted as read-only initially. It is remounted during the boot process as read-write. |
| `append = "debug=2 noapic nosmp"` | Appends options specified here to the string that is passed to the kernel—typically used for hardware parameters such as a hard disk geometry. |

The options available for the `/etc/lilo.conf` file correspond with the three major sections—general, Linux images, and other images. In fact, the options for other images actually apply to any bootable image. A comprehensive list of options for each of the three sections of the `/etc/lilo.conf` file is shown in Tables 12.7, 12.8, and 12.9.

| **TABLE 12.7 GLOBAL OPTIONS (GENERAL)** |  |
|---|---|
| **Option** | **Description** |
| `backup = filename` | Copies the original boot sector to the specified file. |
| `boot = boot_device` | Uses the boot sector from the specified device. |
| `change-rules` | Defines partition type numbers. |
| `compact` | Reads several adjacent sectors in a single read request. |
| `disk = device_name` | Sets non-standard parameters for the specified disk. |
| `fix-table` | Allows LILO to adjust 3D addresses in partition tables. |
| `force-backup = filename` | Same as the backup option, except an existing backup file is overwritten with this option. |
| `ignore-table` | Ignores partition tables that appear to be corrupt and allows LILO to install a boot sector. |
| `install = boot_sector` | Specified file is installed as the new boot sector. |
| `keytable = table_file` | The keyboard is remapped based on the settings in the specified file. |