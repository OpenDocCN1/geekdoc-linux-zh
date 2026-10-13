
安装完成后，你必须确保在每次启动 Linux 时都插入了该软盘。拔掉软盘并重启以启动 Windows。

完成无分区安装后，你可以通过删除 Windows 根目录下的两个文件将其从硬盘中删掉：`redhat.img`（Red Hat 文件系统）和 `rh-swap.img`（交换区域）。

# Kickstart 安装

如果你在多台计算机上安装 Red Hat Linux，可以通过预先配置安装过程中提问的答案来节省一些麻烦。这种自动化安装过程的方法被称为 kickstart 安装。

# 第 2 章 ✦ 安装 Red Hat Linux

执行 kickstart 安装的一般步骤如下：

- 1. 创建 kickstart 文件。kickstart 文件命名为 `ks.cfg`，包含了输入到安装过程中的问题答案。
- 2. 安装 kickstart 文件。你必须将 `ks.cfg` 放在软盘、硬盘上或通过网络提供。
- 3. 启动 kickstart 安装。启动时，识别文件的位置。

## 创建 kickstart 文件

最好的方法是使用安装程序附带的示例 `ks.cfg`。使用文本编辑器对其进行编辑。这里有一个示例：

```
cp /mnt/cdrom/sample.cfg /tmp/ks.cfg
```

所需的数值标识源文件位置：`cdrom`, `nfs`, `url`, 或 `harddrive`。`cdrom` 值不需要选项。要从硬盘安装，你必须指定分区和目录。对于 NFS 服务器，你必须指定服务器和目录。对于 `url`，你必须提供 URL。（示例可以根据实际情况更改。）

### 源位置

```
#cdrom
  --url http://<server>/dir
  --harddrive /dev/sda2 --dir
nfs  --server <server> --dir
```

### 语言规范

### 键盘配置

安装需要分区，升级是可选的。以下代码来自示例 `ks.cfg` 文件。`zerober` 值会清除主引导记录（如需保留 MBR，则使用 `clearpart --linux` 移除 Linux 分区）。`/boot`、`swap` 和 `/` 行分别将分区的大小设置为 16、127 和 1000。根分区（`/`）可以增长到最大为 1400（如果有足够的空间）。

### 分区信息

```
zeromber yes
clearpart --linux
part /boot --size 16
part swap --size 127
part --size 1000 --grow --maxsize 1400
```

`install` 运行新安装。可以使用 `upgrade` 关键字升级现有系统。（对于升级，只需要语言、安装方法、安装设备、键盘和 LILO 配置。）

```
install
```

所需的鼠标值标识鼠标类型。示例显示了一个通用三键 PS/2 鼠标类型（`generic3ps/2`）。你可以将其替换为双键串口鼠标（`generic`）、双键 PS/2 鼠标（`genericps/2`）或微软智能鼠标（`msintellis/2`）。对于串口鼠标，识别设备（例如用于 COM1 端口的 `tty0`）。要配置其他类型的鼠标，运行 `mouseconfig`。要查看其他鼠标类型，运行 `mouseconfig`

### 鼠标配置

```
#mouse generic --device ttyS0
mouse generic3ps/2
```

## 第 2 章 ✦ 安装 Red Hat Linux 35

必需的 `timezone` 命令用于为您的 Linux 系统设置时区。此处显示的默认时区是美国东部时区 (`US/Eastern`)。运行 `timeconfig` 命令可以查看其他其他有效时区。

### 时区配置

`timezone --utc US/Eastern`

可选的 `xconfig` 值可用于配置您的显示器和显卡。如果没有提供任何值，将设置为最小分辨率（640 × 480）和颜色（8 位色）（系统安装完成后，请运行 `Xconfig` 来优化您的 X 配置）。配合 `xconfig` 命令，您可以根据显卡（`--server`）和 `--monitor`）来确定要使用哪种 X 服务器。（如果您完全不需要配置 X，可以使用 `skip` 命令代替。）

### X 配置

`xconfig --server "SVGA" --monitor viewsonic g7733`

`rootpw` 命令将密码设置为其随后的任何单词（在本例中为 `paSword`）。请注意，留下此密码存在安全风险，因此在 Linux 安装后您应该（使用 `passwd` 命令）更改此密码。

### Root 密码指定

`rootpw password`

必需的 `auth` 命令用于设置保护用户密码的认证类型。`--usehadow` 选项启用 `/etc/shadow` 文件存储您的密码。`--enablemd5` 选项允许长 256 个字符的密码。（通常会使用两者。）

### 认证配置

`auth --usehadow --enablemd5`

`auth --enablemd5`

`lilo` 命令设置 LILO 启动加载程序的位置。例如，`--location mbr` 将 LILO 添加到主引导记录。使用 `--location none` 添加 LILO。

### Lilo 配置

`lilo --location mbr`

`lilo --location none`

要指定要安装哪些软件包，请以 `%packages` 命令开始一个章节。以下是几个示例：默认安装组、单独组或单独软件包。在 `%packages` 之后，使用 `@` 符号开始一个软件包组条目，并在单独的一行中通过名称添加每个单独软件包。示例执行了服务器安装，添加了所有 X 软件包，并添加了 `ElectricFence` 软件包。

更多内容见 `www.united.com`

## 第一部分 | Red Hat Linux 入门

> 注意

升级时不支持 `%packages` 命令。

### 软件包指定

`%packages`

# 使用这些完整安装组之一：

@ Server

## KDE Workstation

## Gnome Workstation

# 添加一个单独的组，例如 X Window System：

@ X Window System

## 添加一个单独的软件包，例如 ElectricFence

`ElectricFence`

```
```

您可以在 Red Hat 安装光上找到软件包组和单独软件包的列表。在 `RedHat/base` 目录可以找到 `comps` 文件。

`post` 命令启动安装后部分。您任何想在安装完成后运行的 shell 命令都可以添加在 `post` 命令之后。

```
### 安装后要运行的命令
%post

echo "This is in the chroot" > /tmp/message
```

如果您想了解更多关于 Kickstart 命令的信息，请参阅《Red Hat Linux 参考指南》。该指南在 Red Hat Docs 光盘上提供。它包含一个描述 kickstart 命令的附录。如果没有 Red Hat Docs 光盘，请在任何 Red Hat 镜像站的 `doc/` 目录下查找参考指南和 Kickstart 示例文件（`sample.ks`）（请访问 `http://www.redhat.com/mirrors.html` 查看站点列表）。

## 安装 kickstart 文件

一旦创建了 `ks.cfg`，您需要将其存放在执行的计算机可以访问的地方。通常，您会将文件放在软盘上。然而，您也可以将文件放在网络可访问的计算机或硬盘上。

要将文件拷贝到软盘，请创建一个 DOS 软盘并按如下拷贝文件：

```
mcopy ks.cfg a:
```

在进行 Red Hat 安装时，您必须随身携带此软盘。

将 `ks.cfg` 放在计算机上需要对网络进行更多配置。网络必须配置一个 DHCP 或 BOOTTP 服务器，用于为新安装的计算机提供网络信息。包含 `ks.cfg` 文件的 NFS 服务器必须导出该文件，以便从本地硬盘使用 `ks.cfg` 文件；您可以将文件存放在任何 Windows (`VFAT`) 或 Linux (`ext2`) 分区上。

## 启动 kickstart 安装

如果 kickstart 文件 (`ks.cfg`) 已创建并安装在可访问的位置，您就可以启动 kickstart 安装。以下是如何使用 Red Hat Linux 光盘和包含 `ks.cfg` 文件的软盘进行 kickstart 安装的示例：

- 1. 插入 Red Hat Linux 光盘并重启计算机。
- 2. 当看到启动提示符时，插入包含 `ks.cfg` 文件的软盘并输入以下内容（在您的安装启动之前快速输入）：

```
boot: linux ks=floppy
```
