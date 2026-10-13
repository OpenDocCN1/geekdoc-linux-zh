# TABLE 6-7

# Logical Volume Commands
(continued)

| Logical Volume Command | Description |
|---|---|
| lvrename | Renames an LV. |
| lvresize | Resizes an LV; can be done by -L for size. For example, lvresize -L 4GB volume01/lvol01 changes the size of lvol01 to 4GB. |
| lvs | Lists all configured LVs. |
| lvscan | Scans for all active LVs. |

Here's an example how this works. Try the vgscan command. You can verify configured volume groups (VGs) with the vgdisplay command. For example, Figure 6-4 illustrates the configuration of VG volgroup.

While there are a number of lvm* commands installed, just four of them are active: lvm, lvmlconf, lvmdiskscan, and lvmdump. The lvm command moves to an lvm> prompt. It's rather interesting, as the help command at that prompt provides a nearly full list of available LVM commands.

The lvmlconf command can modify the default settings in the related configuration file, /etc/lvm/lvm.conf. The lvmdiskscan command scans all available drives for LVM-configured partitions. Finally, the lvmdump command sets up a configuration report in the root administrative user's home directory (/root).

# FIGURE 6-4
Configuration of a volume group (VG)

```
[root@server1 ~]# vgdisplay
--- Volume group ---
  VG Name               volgroup
  System ID             
  Format                lvm2
  Metadata Areas        4
  Metadata Sequence No  2
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                4
  Act PV                4
  VG Size               1.92 GiB
  PE Size               4.00 MiB
  Total PE              492
  Alloc PE / Size       0 / 0
  Free  PE / Size       492 / 1.92 GiB
  VG UUID               B8nWng-IWT1-MBT3-KPwS-Ye31-TsaJ-8TwjZ6

[root@server1 ~]#
```