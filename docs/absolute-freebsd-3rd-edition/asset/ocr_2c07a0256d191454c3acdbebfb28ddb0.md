puts a backup copy of the partition table on the last sector of the disk so you can more easily recover from damage.

GPT requires allocating a partition for bootstrap code. The PMBR boot code searches the disk for a FreeBSD boot partition. This boot partition must be larger than the boot code, smaller than 545KB, and reserved for the FreeBSD boot loader. FreeBSD has two GPT boot loaders, `gptboot(8)` and `gptzfsboot(8)`. You must install one of these on the boot partition.

Use `gptboot(8)` to start UFS-based systems. At system boot, `gptboot` searches for a FreeBSD partition marked with the `bootme` or `bootonce` attributes.

Use `gptzfsboot(8)` on systems running ZFS.

Use `gpart(8)` and its many subcommands to view, create, edit, and destroy GPT partitions.

# # GPT Device Nodes

Each disk partition has a device node. GPT partition device nodes are an extension of the geom they’re built on, indicated by the letter *p* and the partition number. If you’ve created GPT partitions directly on the disk `ada0`, the first partition will be `/dev/ada0p1`, the second `/dev/ada0p2`, and so on.

Many systems put their partitions on an upper-layer geom. One of my systems uses SATA RAID and offers the disk as `/dev/raid/r0`. The partitions on this drive are `/dev/raid/r0p1`, `/dev/raid/r0p2`, and so on. You might also put partitions on a device by its GUID or disk ID, giving you partitions like `/dev/diskid/DISK-WD-WCAW36477062p1`.

# # GPT Partition Types

When you create a GPT partition, you must mark it with a *partition type*. The type indicates the partition’s intended use. FreeBSD makes decisions based on the partition types, so assign them correctly.

Strictly speaking, a partition type is another 128-bit GUID. FreeBSD marks GUIDs used as partition types with a leading