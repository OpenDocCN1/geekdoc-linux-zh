# mkswap

**Purpose**: Create swap space storage.

**Usage syntax**: `mkswap [OPTIONS] [DEVICE]`

```
# mkswap /dev/sdb1
Setting up swap space version 1, size = 522076 KiB
no label, UUID=cc5b16c-985f-4723-a5c4-e4dd2377aad
Creating swap storage using the mkswap command
```

The `mkswap` command creates swap space on Linux systems. Swap storage is used to store data in memory that is rarely accessed. This frees up RAM for active programs. In the above example, the `mkswap` command is used to create swap storage on the `/dev/sdb1` partition.

> **Tip**
> Swap utilization has a significant impact on system performance. If a system is utilizing swap space heavily, it should be upgraded with additional memory to increase performance. Additionally, creating swap storage on its own dedicated disk is a good practice that is used to prevent degraded performance.

`mkswap` is a Linux command. Similar commands exist on other platforms and are detailed in the following cross-reference table.

| AIX | BSD | HP-UX | Linux | Solaris |
|---|---|---|---|---|
| mkfs | swaptc1 | lvcreate | mkswap | swap |
Swap command cross reference

Common usage examples:

| | |
|---|---|
| `mkswap [DEVICE]` | Create swap space on the specified device |
| `mkswap -c [DEVICE]` | Check the device for bad blocks before formatting |