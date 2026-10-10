# Reading /proc Files

The /proc directory contains several files that are useful when you are configuring or troubleshooting your system.

# Information Files in the /proc Directory

| File | Information |
| --- | --- |
| /proc/cpuinfo | General information about the system, including the processor type, its speed, and cache size. |
| /proc/interrupts | Maps IRQ addresses to devices. |
| /proc/parport | Information about parallel ports and the devices attached to them. |
| /proc/sound | The system’s sound configuration, including the drivers installed. |

**Warning**
Changing these files can damage your system. Regular users should not have write permission to these files, and the root user should be careful about changing them.

# Reading Log Files

Log files record messages about all activities on your system. Some can be viewed by regular users, but many can only be viewed by the root user.