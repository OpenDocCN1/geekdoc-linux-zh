# OpenBoot Device Aliases

Device pathnames can be long and complex to enter. The concept of device aliases, like UNIX aliases, allows a short name to be substituted for a long name. An alias represents an entire device pathname, not a component of it. For example, the alias disk0 might represent the following device pathname:

```
/sbus@1,f8000000/esp@0,40000/sd@3,0:a
```

OpenBoot has the predefined device aliases listed in Table 2.5 for commonly used devices, so you rarely need to type a full device pathname.

# TABLE 2.5

# Predefined Device Aliases

| Alias | Device Pathname |
|-------|-----------------|
| disk | /pci@1f,0/pci@1,1/ide@3/disk@0,0 |
| disk0 | /pci@1f,0/pci@1,1/ide@3/disk@0,0 |
| disk1 | /pci@1f,0/pci@1,1/ide@3/disk@1,0 |
| disk2 | /pci@1f,0/pci@1,1/ide@3/disk@2,0 |
| disk3 | /pci@1f,0/pci@1,1/ide@3/disk@3,0 |
| cdrom | /pci@1f,0/pci@1,1/ide@3/cdrom@2,0:f |

> NOTE Device pathnames can vary on each platform. The device aliases shown in Table 2.5 are from a Sun Ultra5 system.

If you add disk drives or change the target of the startup drive, you might need to modify these device aliases. Table 2.6 describes the devalias command, which is used to examine, create, and change OpenBoot aliases.

# TABLE 2.6

# devalias

| Command | Description |
|---------|-------------|
| devalias | Displays all current device aliases. |
| devalias_alias | Displays the device pathname corresponding to alias. |
| devalias_alias device-path | Defines an alias representing device-path. |

> NOTE If an alias with the same name already exists, the new value overwrites the old.