
`#network --bootstrap static --ip 192.168.0.1 --netmask`

`#255.255.254.0 --gateway 192.168.0.1 --nameserver 192.168.0.254`

下一个值标识 Red Hat 软件的位置：`cdrom`、`nfs`、`url` 或 `harddrive`。`cdrom` 值不需要任何选项。要从硬盘驱动安装，你必须识别包含发行版的分区和目录。对于 NFS 服务器，你必须识别服务器和目录。对于 `url` 安装，请提供一个包含安装软件的 HTTP 位置。`nfs` 服务器必须根据你的实际情况进行更改。

### 源位置
`#cdrom`
`#url --url http://<server>/<dir>`

```
#harddrive --partition /dev/sda2 --dir /home/dist/6.2/1386

nfs --server porkchop.redhat.com --dir /mnt/dist/6.2/1386
```

必需的 `keyboard` 命令默认识别美国 (`us`) 键盘。支持超过 70 种其他类型的键盘。

### 键盘配置
`keyboard us`

## 第 2 章 安装 Red Hat Linux

新安装和升级都需要进行分区。接下来的代码来自示例 `cs.cfg` 文件。`zerombr yes` 清除主引导记录（如需保留 MBR，请将此设置为 `no`）。`clearpart --linux` 移除现有的 linux 分区（或使用 `--all` 清除所有分区）。`part /boot`、`swap` 和 `/` 行设置了这些分区的大小（分别为 16MB, 127MB 和 1000MB）。根分区 (`/`) 可以增长到 `--maxsize 1400MB`（如果有足够的空间）。

### 分区信息

```
zerombr yes

clearpart --linux

part /boot --size 16

part swap --size 127

part / --size 1000 --grow --maxsize 1400
```

`install` 选项运行新安装。你可以使用 `upgrade` 关键字来替换现有系统。（对于升级，只需要语言、安装方法、安装设备、键盘和 LILOG 配置）。

`install`

必需的 `mouse` 值识别鼠标类型。示例显示了一个通用三键 PS/2 鼠标 (`generic-ps/2`)。你可以将其替换为双键串口鼠标 (`generic`)、双键 PS/2 鼠标 (`generic-ps/2`) 或微软 IntelliMouse (`msintel/2`)。对于串口鼠标，请识别设备（例如，针对 COM1 使用 `--device ttyS0`）。要配置其他类型的鼠标，你必须运行 `mouseconfig`。要查看其他鼠标类型，请运行 `mouseconfig --help` 命令。

### 鼠标配置

```
#mouse generic --device ttyS0

mouse generic-3ps/2
```

必需的 `timezone` 命令设置你的 Linux 系统的时区。然而，默认值是美国东部时区 (`US/Eastern`)。运行 `timeconfig` 命令可以查看其他有效时区。

### 时区配置

```
timezone --utc US/Eastern
```

可选的 `xconfig` 值可用于配置你的显示器和显卡。如果没有提供值，将设置最小分辨率 (`640x480`) 和颜色 (`8` 位色)。一旦安装了 X，运行 `Xconfig` 来改进你的 X 配置。在使用 `xconfig` 命令的同时，你可以根据显卡 (`--server`) 和显示器 (`--monitor`) 标识要使用的 X 服务器类型。（如果你完全不想配置 X，可以使用 `skipx` 命令）。

## 第一部分 在 Red Hat Linux 中入门

`rootpw` 命令将密码设置为随后的任何单词（在本例中为 `paSword`）。请理解，留下此密码存在安全风险，因此你应该在 Linux 安装后更改此密码（使用 `passwd` 命令）。

### 设置根密码
`rootpw paSword`

必需的 `auth` 命令设置用于保护用户密码的认证类型。`--usershadow` 选项允许 `/etc/shadow` 文件存储你的用户密码。

### 认证配置
`auth --usershadow --enablemd5`

`lilo` 命令设置 LILO 的位置。示例显示 `--location none`。

### Lilo 配置
`lilo --location none`

要指定要安装哪些包，以 `%packages` 开始。使用 `@` 符号表示组。

> 注意：升级操作不支持 `%packages` 命令。

### 软件包指定
`%packages`
`- Server`
`- Gnome Workstation`
`- X Window System`
`- ElectricFence`

## 第 2 章 安装 Red Hat Linux 35

你可以在 Red Hat CD 上找到软件包组和软件包的列表。位于目录下的 `comps` 文件。

`%post` 命令启动安装后部分。任何你想在安装完成后运行的 shell 命令都添加在 `%post` 命令之后。

### 安装后运行的命令
`%post`
`echo "This is in chroot" > /tmp/message`

如果你想了解 Kickstart 命令，请参阅 Red Hat 参考指南。该指南可以在 Red Hat Docs。它包含一个描述 Kickstart 命令的附录。如果没有 Red Hat Docs，可以查看 `http://www.redhat.com/mirrors.html`（站点）。

# 安装 kickstart 文件

一旦创建了 `ks.cfg` 文件，你需要将其放置在执行的计算机可以访问的地方。通常，你会将文件放在软盘上。然而，你也可以将其放在网络可用的计算机或硬盘上。

要将文件拷贝到软盘，按以下方式操作：

```
mcopy ks.cfg a:
```

执行 Red Hat 安装时，你必须携带此软盘。

将 `ks.cfg` 文件放在网络计算机上需要更多的配置。网络必须配置 DHCP 或 BOOTP 服务器，为新安装的计算机提供网络信息。包含 `ks.cfg` 文件的 NFS 服务器必须导出该文件，以便计算机访问。要从本地硬盘使用 `ks.cfg` 文件，你可以将其放置在任何 Windows (`VFAT`) 或 Linux (`ext2`) 分区上。

# 启动 kickstart 安装

如果 kickstart 文件 (`ks.cfg`) 已创建并放在可访问的位置，你可以启动 kickstart 安装。以下是使用 Red Hat Linux CD 和包含 `ks.cfg` 的软盘进行 kickstart 安装的示例：

- 插入 Red Hat Linux CD 并重启计算机。
- 当看到启动提示符时，插入包含 `ks.cfg` 的软盘并输入以下内容（要快，在安装自启动之前）：

```
boot: linux ks=floppy
```
