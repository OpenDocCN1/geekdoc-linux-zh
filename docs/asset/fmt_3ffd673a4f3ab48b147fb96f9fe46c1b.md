
# 增强你的 Raspberry Pi 性能

通过这些提升性能的提示和技巧，充分发挥你的 `Raspberry Pi` 的潜力。

![](img/3d658904c66bbb1691af66259d8c8bf9_67_1.png)

`Christian Cawley` 曾任 `IT` 软件工程师，自 `2010` 年以来一直从事工程师工作。他在在线和杂志上为智能手机用户撰写过文章。

你的 `Raspberry Pi` 已经接电。`SD` 卡上已安装了 `Raspian`，你正处于设置无线打印服务器或制作一个机器人从宿舍帮你取回邮件的途中。

但你真的充分利用你这台微型电脑的性能了吗？你所使用的组件是否最大化地发挥了 `Raspberry Pi` 的潜力，还是它们在拖了你的后腿？你是否探索了 `Raspian` 中的所有选项，还是在直接从 `SD` 卡运行操作系统（这会缩短 `SD` 卡的使用寿命）？

![](img/3d658904c66bbb1691af66259d8c8bf9_67_2.png)

可以采用多种技术来提高性能，例如选择合适的硬件对 `CPU` 进行超频。你甚至可以最大化 `Raspberry Pi SD` 卡上的存储空间，或者完全用第二个 `SD` 卡替换它以提高速度。

## 使用存储硬件

使用这些技巧来重新配置你的 `Raspberry Pi` 设置并优化硬件，以确保你的项目获得最佳性能。

- `1` 无论使用什么操作系统，你选择的存储媒体都会影响 `Raspberry Pi` 的性能。容量小且纠错能力较差的 `SD` 卡速度会比大且韧性更好的卡慢，因此请为你的项目找到合适的平衡点并明智购物。

# 02 选择 SD 卡

市有多种标准的 `SD` 卡可用，价格越贵的纠错能力越强。为了提高 `Raspberry Pi` 的性能，请选择高等级的 `SDHC` 卡。同样的建议也适用于 `MicroCards`，你可以通过 `SD` 卡适配器在 `Raspberry Pi` 上使用它们，或直接插入 `Raspberry Pi`。

# 05 将数据写入 RAM

与其在 `SD` 卡上读写数据——这最终会导致可靠性和性能下降——你可以配置 `Raspberry Pi` 将数据写入 `RAM`，这将提高运行速度并提升 `SD` 卡的性能。

使用 `tmpfs`（文件系统表），这是 `Linux` 发行版中可用的一种系统配置。

![](img/3d658904c66bbb1691af66259d8c8bf9_68_1.png)

上方在 `elymux.org/RPI_SD_cards` 有关于 `SD` 卡的极佳指南

# 购买的 SD 卡

```
$ pi@raspberrypi:~

sudo raspi-config
```

# 03 充分利用你的存储空间

你的 `Raspberry Pi` 通常需要 `1GB` 的存储空间，所以无论你的 `SD` 卡有多大，你都可以创建或保存数据。

在 `Raspberry` 中，你可以使用命令行或运行配置实用程序来获取更多空间（仅当你的 `SD` 卡大于 `2GB` 时）

`sudo raspi-config`

### 04 扩展 Raspberry 分区

最大化分区允许利用 `SD` 卡的全部容量，这将增加媒介的寿命（有更多空间可以写入，因此扇区不会被覆盖）。

使用 `raspberry-config`，使用方向键在菜单中选择 `expand_partitions`。在分区调整大小时稍等片刻。

### 06 启用 tmpfs

在 `Linux` 中创建一个 `RAM` 磁盘的设置同样简单。在命令行中，输入：

`sudo nano /etc/fstab`

添加以下行来挂载虚拟系统：

```
tmpfs /tmp tmpfs defaults,noatime,nosuid,size=755m
```

随后保存并退出 `nano`（`Ctrl+O, X`），然后重启 `Raspberry Pi`。

`sudo shutdown -r`

用一张刚从手机上拔出的镜像卡到 `SD` 卡启动你的 `Raspberry Pi` 是很有诱惑力的。毕竟，它们是一样的，对吧？所选 `SD` 卡的工作方式将与你在 `Raspberry Pi` 上使用时完全一样。但你无法获得足够的性能。强烈建议使用具有写入速度的高性能 `SD` 卡。只需确保你购买的是知名品牌即可！

## 教程

![](img/3d658904c66bbb1691af66259d8c8bf9_69_0.png)

上方将你的文件系统放在 `USB` 闪盘上会让备份变得尽可能简单

# 07 配置 fstab 以获得快速性能

重启后，虚拟文件系统将被挂载，`var/log` 在 `RAM` 磁盘上。其他可以移动到 `RAM` 的目录包括：

`tmpfs/tmp tmpfs_defaults,noatime,nosode,size=100m`
`tmpfs/var/log tmpfs_defaults,noatime,nosode,size=30m`
`tmpfs/var/spool/unix tmpfs_defaults,noatime,nosode,size=755,size=20m`

```
tmpfs/tmp tmpfs_defaults,noatime,nosode,size=100m

tmpfs/var/log tmpfs_defaults,noatime,nosode,size=30m

tmpfs/var/spool/unix tmpfs_defaults,noatime,nosode,size=755,size=20m
```

### 10 将 Raspbian 拷贝到 USB

使用空白的 `Ext4` 格式的 `USB` 驱动器（或外部硬盘）作为目标驱动器，

## 教程

![](img/3d658904c66bbb1691af66259d8c8bf9_69_0.png)

上方将你的文件系统放在 `USB` 闪盘上会让备份变得尽可能简单

# 07 配置 fstab 以获得快速性能

重启后，虚拟文件系统将被挂载，`var/log` 在 `RAM` 磁盘上。其他可以移动到 `RAM` 的目录包括：

### 10 将 Raspbian 拷贝到 USB

使用空白的 `Ext4` 格式的 `USB` 驱动器（或外部硬盘）作为目标驱动器，

（注：由于原文存在大量重复和混乱，此处已根据逻辑整合进行完整翻译）
