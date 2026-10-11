| **Table 8-2 (continued)** |  |
|---|---|
| **Entry** | **Function** |
| `linear` | Generates linear addresses instead of sector/head/cylinder addresses. This is required for some SCSI disks. |
| `lock` | Tells LILO to remember the last boot command line and use it as the default until another is manually entered. |
| `map=<map file>` | Specifies which map file to use. By default this is `/boot/map`. |
| `menu-title=<menu title>` | Specifies the title for the boot menu. |
| `menu-scheme=<color scheme>` | Specifies the boot menu color scheme. |
| `message=<message file>` | Specifies a text file with a message that is displayed before the boot prompt. |
| `nowarn` | Disables warnings about possible problems. |
| `prompt` | Instructs LILO to show the boot prompt, instead of booting the default image right away. |
| `serial=<parameters>` | Allows you to boot the system from a serial interface instead of a normal monitor. |
| `timeout=<tenths of seconds>` | Tells LILO to wait the specified number of tenths of seconds for keyboard input at the boot prompt before booting the default image. |
| `verbose=<number>` | Enables verbose messages. The level of verbosity can be set from 1 to 5. |

| **Table 8-3** |  |
|---|---|
| **Per-Image lilo.conf Entries** |  |
| **Entry** | **Function** |
| `image=<path name>` | The path to the device or file containing the kernel boot image. |
| `other=<device name>` | Used to boot another operating system, such as Windows. The device name should point to the partition or disk of the other operating system. |
| `label=<name>` | The name of the boot image as shown in the boot menu. |
| `alias=<name>` | A second name for a boot image. |
| `lock` | Same as the global entry, but applies only to this image. |