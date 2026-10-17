
`mount`命令报告以下内容：

- 所有已挂载的设备
- 设备在你的 Linux 文件系统或目录结构中的挂载位置
- 设备上使用的文件系统
- 你是否可以对设备进行读写 (`rw`) 或只读 (`ro`)

另参

- 有关挂载文件系统的其他方法，请参见第 454 页。

# 第二部分 配置你的系统

# 第7章 使用硬盘

## 文件系统支持并不意味着格式化

尽管 Linux 支持许多不同的文件系统以允许文件的读取和写入，但你可能仍需要使用另一个操作系统以非 Linux 文件系统格式化新硬盘。Linux 并没有带用于大多数其他文件系统的磁盘格式化工具（DOS 除外；更多信息请参阅 `mtools` 手册页）。

## 选择文件系统

当你向系统添加硬盘并想同时使用 Linux、DOS 或 Windows 时，请使用 `ext2` 和 `mdos` 或 `vfat` 文件系统。虽然你可以对 DOS 分区使用 `mdos` 文件系统，但对于 Windows 95 分区你应该使用 `vfat` 文件系统，这样你可以获得更大的分区并获得长文件名支持。如果你在 Linux 目录下挂载 `vfat` 分区，`ls` 命令将显示如下的文件文件名：

```bash
# ls /mnt/dos/windows/*.bmp
/mnt/dos/windows/Black_Thatch.bmp /mnt/dos/windows/Pinstripe.bmp
/mnt/dos/windows/Blue_Rivets.bmp /mnt/dos/windows/Red_Blocks.bmp
/mnt/dos/windows/Bubbles.bmp /mnt/dos/windows/Sandstone.bmp
/mnt/dos/windows/Carved_Stone.bmp /mnt/dos/windows/Setup.bmp
/mnt/dos/windows/Circles.bmp /mnt/dos/windows/Stitches.bmp
/mnt/dos/windows/Clouds.bmp /mnt/dos/windows/Straw_Mat.bmp
/mnt/dos/windows/Forest.bmp /mnt/dos/windows/Tiles.bmp
/mnt/dos/windows/Gold_Weave.bmp /mnt/dos/windows/Triangles.bmp
/mnt/dos/windows/Houndstooth.bmp /mnt/dos/windows/Waves.bmp
/mnt/dos/windows/Metal_Links.bmp
```

DOS 分区不支持长文件名。如果你使用 `mdos` 分区并挂载它，然后从你的 Linux 文件系统复制文件到 DOS 分区，`ls` 命令将显示如上例所示的文件：

```bash
# ls /mnt/dos/windows/*.bmp
/mnt/dos/windows/black-1.bmp /mnt/dos/windows/pinstr-1.bmp
/mnt/dos/windows/bluer-1.bmp /mnt/dos/windows/redbio-1.bmp
/mnt/dos/windows/bubbles.bmp /mnt/dos/windows/sandst-1.bmp
/mnt/dos/windows/carved-1.bmp /mnt/dos/windows/setup-1.bmp
/mnt/dos/windows/circles.bmp /mnt/dos/windows/stitches.bmp
/mnt/dos/windows/clouds.bmp /mnt/dos/windows/straw-mat.bmp
```

## 添加硬盘

## 识别硬盘与设备

[139]

## 使用 fdisk 命令分区硬盘

使用 `fdisk` 命令为新硬盘准备一个或多个分区。`fdisk` 不是最直观的命令，但它可以快速准备驱动器备用。

> 不要覆盖你正在运行的分区
> 如果你需要对正在使用的硬盘进行重新分区，请确保先卸载它。如果必须对你挂载的硬盘进行重新分区，你应该先进入单用户模式。

另参

- 有关运行级别的更多信息，请参见第 355 页。

1. 以 root 用户身份登录。在命令行中指定设备名称，使用 `fdisk` 命令准备并分区硬盘：
```bash
# fdisk /dev/sda
```
2. `Command (m for help): m`
`fdisk` 在识别你的设备后会打印提示符。按 `M` 显示 `fdisk` 命令列表。程序响应如下：
```
Command action
a 切换启动标记
b 编辑 bs 标签
c 切换 dos 兼容性标记
d 删除分区
l 列出已知分区类型
m 显示此菜单
n 添加新分区
p 打印分区表
q 不保存更改退出
t 更改分区系统 ID
u 更改显示/输入单位
v 验证分区表
w 写表并退出
x 额外功能（仅限专家）
```
3. 按 `N` 添加新分区表。`fdisk` 程序响应如下：
```
Command (m for help): n
Command action
e 扩展
p 主分区 (1-4)
```
4. 你只想在该硬盘上使用一个分区，所以按 `P` 选择主分区。`fdisk` 程序响应如下：
```
p Partition number (1-4):
```
5. 输入数字 `1`，并按回车。`fdisk` 如下响应：
```
分区编号 (1-4): 1
起始磁道 (1-96):
```
6. 注意，根据磁道数量所示，这是一个小型硬盘（小于 100MB）。输入数字 `1` 并按回车。`fdisk` 请求分区的结束磁道数：
```
起始磁道 (1-96):
末尾磁道或 +size 或 +sizeM 或 +sizeK [1-96]
```
7. 输入 `96`。如果你输入的是 `50`，设备上仍会有 `46` 个磁道，你可以创建一个从磁道 `51` 到 `96` 的新分区，这大约占硬盘存储容量的一半。
```
末尾磁道或 +size 或 +sizeM 或 +sizeK [1-96]: 96
```
8. 按 `P` 创建分区表：
```
Command (m help): p
Disk /dev/sda: 64 头部, 32 扇区, 96 磁道
Units = cylinders of 2048 * 512 bytes
```
```
Device Boot  Begin  Start  End  Blocks  Id System
/dev/sda       1      96  98288 b8 Linux native
Command (m help):
```
9. 要更改分区大小，请按 `T`。
```
Command (m help): t
```
10. `fdisk` 请求要更改的分区编号。输入 `1`。
```
分区编号 (1-4): 1
```
11. `fdisk` 请求选择一个，代表一种文件系统类型。要查看你可以使用的类型，请按 `L`，`fdisk` 会提供如下列表：
```
十六进制代码 (按 L 列出代码):
```
```
0 Empty        AIX bootable  75 PC/IX         b7 BSD-fi
1 DOS-12 FAT      a 0/2 Boot M0 80 Old MINIX     b8 BSD swap
2 XENIS root      b Win95 FAT      81 Linux/UNIX   c7 Syntax
3 XENIS user      40 Novell B2086 82 Linux       db CP/M
4 DOS-16 -<32M 51 Novell7       83 Linux native  e1 DOS access
5 Extended        52 Microsoft    93 Amoeba      d5 DOS/RO
6 DOS-16 >+32 63 GNU Hard     94 Amoeba BBT  f2 DOS secondary
7 OS/2 HPFS      64 Novell Navarre a5 BSD/386     ff BBT
8 AIX             65 Novell Netware
Hex code (type L to list codes):
```
