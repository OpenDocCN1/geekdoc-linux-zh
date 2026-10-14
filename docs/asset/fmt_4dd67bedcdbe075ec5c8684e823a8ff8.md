
# 第二部分：安装 TurboLinux

## 第 5 章：安装：进入最后冲刺

### 修改分区类型

当 `fdisk` 创建分区时，默认创建 Linux 原生分区。有许多种的文件系统可用，如图 5-14 所示。你选择的文件系统决定了放在磁盘分区上的操作系统、目录的最大大小、文件名的长度以及该分区可以存放多少文件。

图 5-14：可选的文件系统

```text
Command (m for help): l

| | | | | | | |
|---|---|---|---|---|---|---|
| 0 | Empty | AI boot | PC/CD | Linux swap | BDI | |
| 1 | DOS 12-bit FAT | 75 BDI | Linux native | System | |
| 2 | NTFS root | 32-63 Novell | Linux swap | | |
| 3 | Linux ext2 | 31 C3m | MacOS Boot | F2 | |
| 4 | DOS 16-bit | 62 GNU MBR | Linux native | F2 secondary | |
| 5 | Swap | 65 Novell Nature | 84 Linux | Memory | |
| 6 | DOS 16-bit | 32-63 | 80836 | 86 | |
| 7 | MFS | | | | | |
| 8 | AIX | | | | | |
```

5. 现在输入代表你想要的文件系统/分区的数字代码。

由于我们需要一个交换分区（swap partition），所以你输入了 `82`。

请在创建分区以及稍后为各种系统选择分区时，记住哪些分区（例如 `/dev/hda2` 或 `/dev/sdb3`）被用于文件系统（例如 `/usr` 或 `/tmp`）。

6. 输入 `p` 以显示分区表并检查结果。

7. 如果你想定义更多交换分区，请重复步骤 2 到 6。

到此阶段，你可能已经完成了对文件系统分区的更改，因为大多数其他文件系统可以保持 Linux 原生格式。

输入 `p` 显示分区表：

```text
Command (m for help): p

Disk/dev/sda: 33 heads, 61 sectors, 1018 cylinders

Units = cylinders of 2013 * 512 bytes

Device Boot  Begin  Start  End  Blocks      System

/dev/sda1 *       1     300 301919 & DOS 16-bit >=32M

/dev/sda2       301    301 504 205326 83 Linux native

/dev/sda3         505    505 635 131851+ 83 Linux native

/dev/sda4         636    636 1018 385489+ 83 Linux native
```

输入 `l` 列出可用类型，并指定分区 3：

```text
Command (m for help): l

Partition (1-4): 3

Hex code (type L to list codes):

0 Empty            9 AIX boot      75 PC/IX      b7 BSDI fi
1 DOS 12-bit FAI   n /dev/Mast Boot 00 OLD MIX b8 BSDI swap
2 XFS partition      77 FR32 b8 Linux/MINIX
3 XENIS us               82 Linux swap  a6 CF/M
4 DOS 16-bit<32M 51 Novel7   83 Linux native  a1 DOS access
5 Extended           52 Microsoft 93 Amoeba     e3 R/O root
6 DOS 16-bit<32 S 63 Linux       94 Amoeba     f2 DOS secondary
7 HFS               64 Network     e5 850/386     ff BBT
8 AIX                 65 Novell Never
```

在 `Hex code (type L to list codes):` 提示符后输入 `82`，将分区 3 的系统类型更改为 `82 (Linux swap)`。

再次输入 `p` 验证更改：

```text
Command (m for help): p

图-5: dev/sda: 33 heads, 61 sectors, 1018 cylinders
Units = cylinders of 2013 * 512 bytes

Changing partition type from Linux to swap.

Device Boot  Begin  Start  End  Blocks      System

/dev/sda1 *       1     300 301919 & DOS 16-bit >=32M
/dev/sda2       301    301 504 205326 83 Linux native
/dev/sda3         505    505 635 131851+ 83 Linux swap
/dev/sda4         636    636 1018 385489+ 83 Linux native
```

```text
Command (m for help):
```

### 修改启动标记

如果该列中没有星号，或者星号位于分区 1 以外的磁盘分区上，你就必须对其进行更改。在图 5-16 的示例中，我们首先消消并清除了分区 1 的启动标记，只是为了向你展示可以使用相同的步骤清除或设置启动标记。

输入 `p` 显示分区表：

```text
Command (m for help): p

Disk /dev/sda: 33 heads, 61 sectors, 1018 cylinders

Units = 2013 * 512 bytes

| Device Boot | Begin | Start | End | Blocks | Id System |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda * | 1 | 300 | 30199* | 6 | DOS 16-bit >=32M |
| /dev/sda2 | | 301 | 504 | 205236 | 83 Linux native |
| /dev/sda3 | | 505 | 635 | 131851* | 82 Linux swap |
| /dev/sda4 | | 636 | 1018 | 385489* | 83 Linux native |
```

输入 `a` 设置启动标记：

```text
Command (m for help): a

Partition (1-4): 1
```

再次输入 `p` 显示分区表：

```text
Command (m for help): p

Disk /dev/sda: 33 heads, 61 sectors, 1018 cylinders

Units = 2013 * 512 bytes

| Device Boot | Begin | Start | End | Blocks | Id System |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda * | 1 | 300 | 30199* | 6 | DOS 16-bit >=32M |
| /dev/sda2 | | 301 | 504 | 205236 | 83 Linux native |
| /dev/sda3 | | 505 | 635 | 131851* | 82 Linux swap |
| /dev/sda4 | | 636 | 1018 | 385489* | 83 Linux native |
```

```text
Command (m for help): p

Partition (1-4): 1
```

```text
Command (m for help): p

Disk /dev/sda: 33 heads, 61 sectors, 1018 cylinders

Units = 2013 * 512 bytes
```
