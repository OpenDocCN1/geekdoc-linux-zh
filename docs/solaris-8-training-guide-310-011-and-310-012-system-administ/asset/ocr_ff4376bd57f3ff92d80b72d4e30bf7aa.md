| Keyword | Description |
|---|---|
| remote_filesystem | Specifies an NFS file system on a remote system. The <path> must include the name or IP address of the remote system (host) and the absolute <path> to the NFS file system. The NFS file system must have read/write access. A sample <path> is sparc1:/home. |
| remote_system | Specifies a directory on a remote system that can be reached by a remote shell (rsh). The system being upgraded must have access to the remote system through the remote system's .rhosts file. The <path> must include the name of the remote system and the absolute path to the directory. If a user login is not specified, the login is tried as root. A sample <path> is bcalkins@sparc1:/home. |

Here are some examples:

```
backup_media local_tape /dev/rmt/0
backup_media local_diskette /dev/rdiskette0
backup_media local_filesystem /dev/dsk/c0t3d0s7
backup_media local_filesystem /export
backup_media remote_filesystem sparc1:/export/temp
backup_media remote_system bcalkins@sparc1:/export/temp
```

backup_media must be used with the upgrade option only when disk space reallocation is necessary.

# boot_device

boot_device designates the device where the installation program installs the root file system and consequently what the system’s startup device is. The EEPROM value also lets you update the system’s EEPROM if you change its current startup device so that the system can automatically start up from the new startup device.

Here’s the boot_device syntax:

```
boot_device <device> <eeprom>
```

The device and eeprom values are described in Table 21.6.