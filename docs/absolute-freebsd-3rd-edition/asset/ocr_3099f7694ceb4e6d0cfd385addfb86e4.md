| Device node | Man page | Description |
|---|---|---|
| `/dev/da*` | `da(4)` | SCSI-style direct access disks (USB storage, SAS, etc.) |
| `/dev/md*` | `md(4)` | Memory disks |
| `/dev/mmcsd*` | `mmcsd(4)` | MMC and SD memory cards |
| `/dev/nvd*` | `nvd(4)` | NVM express drives |
| `/dev/vtbd*` | `virtio_blk(4)` | Virtio-based virtual machine disk |
| `/dev/xbd*` | `xen(4)` | Xen virtual disks |

Many RAID controllers present their RAID containers as SCSI devices, so they show up as `/dev/da` device nodes. Others present their disks as “SCSI plus special vendor topping,” so they get special device node names such as `/dev/raid` (ATA RAID), `/dev/mfid` (certain LSI MegaRAID cards), and so on. Check the man page for your RAID controller to see the device node it presents.

# ## The Common Access Method

The *Common Access Method* (*CAM*) is a standardized device driver architecture originally written to support the complex command set of 20th-century SCSI-2 disks. The idea was that standardizing based on this architecture would simplify writing device drivers. Only FreeBSD and DEC OSF/1 actually shipped with CAM, however, and each filled in the specification’s gaps differently.

FreeBSD 9 and later consolidates management of all physical disks that support CAM in the CAM interface. Use `camcontrol(8)` to gather information from disks and issue commands to them. The `camcontrol(8)` command has a variety of subcommands that let you issue instructions to hard drives.