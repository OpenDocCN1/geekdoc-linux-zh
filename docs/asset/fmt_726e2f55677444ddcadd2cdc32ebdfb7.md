
- 反泛洪

- 许多其他功能

> 注意：有关 `netfilter` 的更多信息，请参考以下网站：`http://netfilter.org`

## 备份安全

另一种获取访问的方法是窃取你的备份。在这种情况下，有人可能读取你的信息但无法修改它。备份服务器有两种方法：

- 直接连接到服务器的磁带或带库
- 连接了磁带或带库的备份服务器

确保将磁带锁在安全的地方，如果你使用备份服务器，请务必使用用户名和密码恢复文件。请查看第425页的“备份”获取有关备份数据和不同备份解决方案的更多信息。

## 操作系统更新

`SuSE` 和 `RedHat` 都提供了简单的方法让系统保持最新的补丁。更多信息请参阅 `YaST` 或 `RHN`。

# 3.2 Linux 管理

管理 Linux 服务器并不困难。在本节中，我们将讨论基本管理任务，例如创建分区、创建文件系统、创建脚本和修改 `crontab`。

## 3.2.1 分区

创建、删除或修改分区的工具是 `fdisk`。为了能够使用它，以 `root` 身份登录 `shell` 并输入 `fdisk /dev/sda`，其中 `sda` 是第一个磁盘。如果你没有使用 `SCSI`，则第一个磁盘将是 `hda`。要列出 `SCSI` 磁盘上的分区，输入 `fdisk /dev/sda -l`，如示例 3-5 所示。

**示例 3-5 `fdisk -l` 分区列表**

```
Disk /dev/sda: 240 头, 63 扇区, 2584 柱体

Units = 15120 * 512 bytes

| Device | Boot | Start | End | Blocks | Id System |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | * | 1 | 821 | 620628 | 7 HPFS/NTFS |
| /dev/sda2 | | 822 | 2584 | 13328280 | f Win95 Ext'd (LBA) |
| /dev/sda5 | | 1365 | 2584 | 9223168* | b Win95 FAT32 |
| /dev/sda6 | | 822 | 1329 | 3840417 | 83 Linux |
| /dev/sda7 | | 1330 | 1364 | 264658* | 82 Linux swap |
```

分区表项并非按磁盘顺序排序

> 重要：你的磁盘分区可能与示例不同。

Linux 采用以下分区编号系统：

- 从 1 到 4 是主分区
- 从 5 到 16 是逻辑分区

要查看所有 `fdisk` 命令，交互式启动 `fdisk /dev/sda`，然后输入 `m`，如示例 3-6 所示。

**示例 3-6 命令列表**

```
Command (m for help): m
Command action
a toggle a bootable flag
b edit bs disklabel
toggle the dos compatibility flag
delete a partition
l list known partition types
 print this menu
a add a new partition
o create a empty DOS partition table
p print the partition table
```

- `q` 退出不保存更改
- `s` 创建一个空的 `Sun` 磁盘
- `t` 更改分区的系统 ID
- `u` 修改显示/条目单位
- `v` 验证分区表
- `w` 将表写入磁盘并退出
- `x` 额外功能（仅限专家）

若要删除分区，请参考示例 3-7。

## 示例 3-7 删除分区

```
命令 (m 帮助): d
分区编号 (1-7): 7
命令 (m 帮助):
```

若要创建一个逻辑分区，请参考示例 3-8。

## 示例 3-8 创建分区

```
命令 (m 帮助): n
命令操作
1 逻辑分区 (5 或以上)
p 主分区 (1-4)
起始磁道 (1330-2584, 默认 1330)
使用默认值 1330
结束磁道，或 +size 或 +sizeM 或 +sizeK (1330-1364, 默认 1364)
使用默认值 1364
命令 (m 帮助):
```

> 注意：只有在已经创建了扩展分区的情况下，逻辑选项才会出现在新分区中。

创建分区后，你可以更改分区的类型。在 Linux 中，分区类型被编码为数字或 ID。默认情况下，Linux 创建的分区 ID 为 `83`，这意味着它被指定为 Linux 分区。

在第 153 页的示例 3-9 中，你可以看到此时 Linux 支持的所有分区类型。

## 示例 3-9 Linux 支持的所有分区

```
命令 (帮助): t
分区编号 (1-7): 6
十六进制代码 (L 列出代码): 1

| | | | | | | | |
|---|---|---|---|---|---|---|---|
| 0 | Empty | 1b 隐藏 Win9 FA | 64 | Novellare | bb | Boot Wizard hid |
| 1 | FAT12 | 1c 隐藏 Win9 FA | 65 | Novellare | c1 | DRDOS/sec (FAT- |
| 2 | XENIS root | 1e 隐藏 Win9 FA | 70 | DiskSecure Mult | c4 | DRDOS/sec (FAT- |
| 3 | XENIS usr | 24 DEC DOS | 75 | PC/IX | c6 | DRDOS/sec (FAT- |
| 4 | FAT16 <32M | 39 | Plan | 80 | Old Minix | c7 | Cyril |
| 5 | Extended | 33 | Partition Mag | 81 | Minix / Old Lin | da | Non-FS data |
| 6 | FAT16 | 40 | NTFS 8028 | 82 | Linux swap | db | CP/M / CTOS - |
| 7 | HPFS/NTFS | 41 PPC PreP Boot | 83 | Linux | de | Dell Utility |
| 8 | AIX | 42 | SFS | 84 | OS/2 hidden C: | df | BootII |
| 9 | AIX table | 46 | NTFS.4 | 85 | Linux extended | ee | dOS Access |
| a | OS/2 Boot Mang | 46 | NTFS.4 2nd part | 86 | NTFS volume set | ei | DOS R/O |
| b | WinFAT32 | 46 | NTFS.4 3rd part | 87 | NTFS volume set | e | SpeedStor |
| c | WinFAT32 (LB) | 50 | Ontrack DM | 88 | Linux Lyman | eb | Beos FS |
| e | WinFAT16 (LB) | 51 | Ontrack DM Aux | 93 | Amoeba | ef | EFI GPT |
| f | WinFAT16 Ext'd (LB) | 52 | CP/M | 94 | Amoeba BBT | ee | EFI (FAT-12/ |
| 10 | OPUS | 53 | Ontrack DM6 | 95 | BSD/OS | f1 | SpeedStor |
| 11 | Hidden FAT12 | 54 | Ontrack DM6 | a0 | IBM Thinkkink hip | f2 | DOS secondary |
| 12 | Hidden FAT14 | 55 | EZ-Drive | a5 | BSD356 | fe | Linux raid auto |
| 14 | Hidden FAT16 <3 | 56 | Golden Bow | a6 | OpenBSD | ff | LANep |
| 15 | Compaq signif | 57 | Priam Edisk | a7 | NEXTSTEP | |
| 16 | Hidden FAT16 | 61 | SpeedStor | b7 | BSDI fs | |
| 17 | Hidden HPFS/NTF | 63 | GNU HURD or Sys | b8 | BDI swap | |
| 18 | AST SmartSleep | | | | | | |
```

在你创建并设置分区后，按下 `w` 将更改写入硬盘。

> 注意：你对分区所做的更改在按下 `w` 之前不会被提交；或者在出错时，可以按下 `q` 而不保存更改。
