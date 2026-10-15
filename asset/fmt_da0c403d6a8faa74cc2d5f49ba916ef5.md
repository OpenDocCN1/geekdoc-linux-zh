
15. 选择软件包。选择你想要在系统中安装的软件包。选择 `GRP` 软件包以使用预编译的二进制文件。这将加速安装过程。点击“下一步 (`Forward`)”进入“服务 (`Services`)”屏幕。

16. 选择服务。开启将在启动时运行的服务。点击“下一步 (`Forward`)”进入“其他设置 (`Other Settings`)”屏幕。

17. 选择设置。选择与显示管理器、键位以及你感兴趣的功能相关的设置。你还可以选择将 BIOS 时钟设置为 UTC 时间。点击“下一步 (`Forward`)”继续进入“用户 (`Users`)”屏幕。

18. 分配 root 密码。输入你的 root 密码。选择“添加用户 (`Add User`)”为普通用户添加账户。点击“下一步 (`Forward`)”查看“检查 (`Review`)”屏幕。

19. 检查选项。仔细检查你选择的安装内容。点击“保存 (`Save`)”保存设置供以后安装。这是你在擦除磁盘并安装软件包之前退出的最后机会！安装 Gentoo 将重新格式化你的硬盘并安装 Gentoo。安装过程需要很长时间才能完成。可能需要非常久！

20. 完成安装。看到“安装完成 (`Install Complete!`)”消息后关闭安装程序。

21. 退出并重启。选择注销，然后重启电脑。系统关机后，移除 Live CD 并重启新安装的 Gentoo 系统。

此时，你可以使用 `emerge` 命令向你已安装的 Gentoo 系统添加额外的软件包。请参阅本章节后半部分的“使用 emerge 获取软件”内容。

# 从最小化 CD 开始安装 Gentoo

以下是使用本章中的最小化程序进行 Gentoo 安装的最低计算机配置要求：

- 1.5GB 硬盘空间
- 256MB 内存 (`RAM`)
- 一个 686 处理器（或更高）
- 256MB 交换空间 (`swap space`)

如果你的处理器较慢，考虑获取预编译软件包，因为整个编译过程可能需要长时间。

请使用附录 A 中提到的随书 CD。有了这张 CD 后，在你的电脑上安装 Gentoo 的方法如下：

1. 插入 CD。将 CD 插入电脑的 CD 或 DVD 驱动器中。
2. 重启。重启你的电脑。

# 第三部分：选择并安装 Linux 发行版

3. 启动 CD。在启动提示符处按回车键。（如果你无法启动安装介质，按 `F1` 或 `F2` 查看其他可能帮助你启动的安装选项。）在启动提示符处输入 `gentoo`：启动 Gentoo Live CD，或按指定的 Gentoo 功能键查看运行 Gentoo 的其他选项。

Gentoo 应该会检测你的计算机硬件，启动安装过程并显示启动提示符。

4. 设置日期。输入 `date` 命令以确保日期和时间正确。如果需要更改，使用 `date` 命令（带有选项）来更改它们。例如，要将日期设置为 2008 年 6 月 15 日上午 8:15，输入：

```
# date 06150152008
```

5. 加载模块。如果某些硬件未被自动检测到，你可能需要加载访问硬件所需的模块。使用 `modprobe` 命令并加上要加载的模块名称。例如，要加载 Orinoco 无线网卡的模块，你可以执行：

```
# modprobe orinoco
```

> 在网络上搜索“Linux”和未检测到的硬件名称，以找到需要加载的模块。

6. 配置网络。使用 `ifconfig eth0` 查看第一块以太网卡的互联网连接是否正常运行。然后尝试 ping 一 互联网上的某台计算机以确保你可以访问外部（例如 `ping www.gentoo.org`）。如果你无法获取到 DHCP 服务器来自动连接互联网，你可以通过输入以下命令手动设置：

```
# net-set eth0
```

请参阅第 8 章安装过程中的网络配置信息，以帮助你回答关于手动设置互联网连接的问题。

7. 硬盘分区。对你的硬盘进行分区，为接收 Gentoo 安装做准备工作。使用 `fdisk` 工具创建一个 6MB 的启动卷（ext2 文件系统）、一个大小为内存两倍的交换分区，以及一个大的根（/）分区（Reiser 文件系统）。通过输入你的第一个硬盘的名称启动 `fdisk`（例如，第一个 IDE 或 SCSI 硬盘分别为 `/dev/hda` 或 `/dev/sda`）。然后输入 `h` 显示命令列表。（有关使用 `fdisk` 硬盘分区的信息请参见第 7 章。）

```
# fdisk /dev/hda
```

重新分区磁盘会破坏硬盘上的数据。在开始此程序之前，请备份任何数据。确保不要删除或更改任何包含你想要的数据的分区。

# 运行 Gentoo Linux

8. 创建文件系统。要在你的磁盘分区上创建适当的文件系统，请使用 `mk2fs` 和 `mkswap` 命令。例如，对于第一个分区为启动分区（`/dev/hda1`）、第二个为交换分区（`/dev/hda2`）、第三个为根（/）分区（`/dev/hda3`）的 IDE 硬盘，你可以输入：

```
# mk2fs /dev/hda1
# mkswap /dev/hda2
# mk2fs /dev/hda3
```

9. 开启交换。使用 `swapon` 命令开启交换。例如：

```
# swapon /dev/hda2
```

10. 挂载根（/）分区。使用 `mount` 命令挂载根分区。例如：

```
# mount /dev/hda3 /mntoo
```

11. 挂载启动分区。使用 `mount` 命令挂载启动分区。例如：

```
# mkdir /mntoo/boot
# mount /dev/hda1 /mntoo/boot
```

12. 获取 stage 1 包。使用 `wget` 命令下载包。例如：

```
# wget http://gentoo.org/releases/x86/2007.0/stage3.tar.bz2
```

13. 解压包。使用 `tar` 命令解压包。

14. 选择镜像站点。使用 `mirrorselect` 命令选择 Gentoo 镜像并将其添加到 `make.conf` 文件。

```
# mirrorselect -s -o | grep GENTOO_MIRRORS >> /etc/make.conf
```

> **注意** 如果之后运行 `emerge` 命令时发现找不到任何下载文件，你可能需要在 `make.conf` 中添加其他镜像站点。

15. 挂载文件系统。挂载 `/proc` 文件系统。

```
# mount -t proc /mntoo/proc
```

16. 切换目录。使用 `chroot` 命令将 `/mntoo` 变为你的根目录。

```
# cp /etc/resolve.conf /mntoo/etc/resolve.conf
# chroot /mntoo /bin/bash
```

17. 更新 Portage 树。输入以下命令获取最新的软件包信息：

```
# emerge -sync
```

18. 更新环境。读取环境变量。

```
# env-update: source /etc/profile
```

19. 修改 `make.conf` 文件。使用 `nano` 编辑器修改 `make.conf` 文件。

```
# nano -w /etc/make.conf
```

20. 引导 Gentoo。运行 `bootstrap.sh` 来引导 Gentoo。

```
# cd /usr/portage/ ; scripts/bootstrap.sh
```

# Gentoo Linux

21. 安装 Gentoo。在运行下一个命令之前，请理解这可能需要很长的时间才能完成。使用旧电脑和慢速的互联网连接，可能需要几小时到几天时间不等。如果你可以接受，请运行以下 emerge 命令来安装 Gentoo：

```bash
# emerge -e system
```

如前所述，`emerge -e system` 完成需要很长时间。如果它在完成之前失败，请检查你的 `make.conf` 文件中的设置是否正确。

22. 设置时区。使用以下命令：

```
# ln -sf /usr/share/zoneinfo/path /etc/localtime
```

你需要将路径替换为计算机所在时区的文件路径。例如，美国中部（Central）的条路径为 `/usr/share/zoneinfo/US/Central`。（如果你的日期和时间设置错误，可以运行 `hwclock` 命令从 BIOS 设置系统日期和时间。）

23. 创建文件系统表。将你希望在启动时自动加载的文件添加到 `/etc/fstab` 文件中。这是一个示例：

```bash
# nano -w /etc/fstab
```

这里的 `/etc/fstab` 看起来如下（假设在本示例步骤之前已经创建了分区）：
