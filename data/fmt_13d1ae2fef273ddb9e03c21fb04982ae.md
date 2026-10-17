
在这个示例中，`qemu` 启动 `FC6-live.iso` 使其显示在桌面的窗口中。`-cdrom` 选项告诉 `qemu` 该文件是一个 CD-ROM 镜像。`-boot d` 选项表示镜像作为 El Torito CD 启动。`-m` 选项告诉 `qemu` 使用 768MB 的虚拟内存来启动 live CD（你应该根据可用内存尽可能多地使用）。

`qemu` 命令和刻录 ISO 镜像的过程将在附录 B“构建、测试和刻录 ISO”中进行更详细讨论。

## 自定义 live CD

虽然自定义 live CD 可以简单如选择 Fedora (anaconda) 般，但为了帮助理解其过程，这里是所发生的活动列表：

- 脚本和配置——`/usr/share/kadishi` 包含了 Kadishi 中的脚本和其他内容，你可能需要修改它们以适应你自己的 Fedora live CD。Kadishi 的配置文件（`kadishi.conf` 和构建标记文件）位于 `/etc/kadishi` 目录。

- 启动——`livecd-initrd.sh` 脚本创建 live CD 上使用的初始内存磁盘（`initrd.img`）。

- 压缩文件——任何需要保持可写的文件和文件夹将被复制到单个目录并压缩为 `.tar.gz` 文件。

- 构建目录——过程中创建的目录（名为 `/tmp/kadishi.xxx`）将被删除。它被一组随机数字和字母取代，因此每个 live CD 构建的名称都是唯一的。

更改消息文件、启动选项以及其他直接与 live CD 启动相关的功能（本章稍后将会有描述）。

- `kadichi.py`——这是当你启动 `kadichi` 命令（`/usr/bin/kadichi/`）时运行的 Python 脚本（同 `build.conf` 文件的内容一起运行）。如果你愿意，可以在此脚本中设置变量以添加选项（例如向 anaconda 传递参数）或覆盖设置（例如你的构建目录或 ISO 镜像的路径）。

自定义 Kadichi 创建你的 Fedora Live CD 的另一种机会是使用 `/usr/share/kadichi/post_install_scripts` 目录下的脚本。在 Fedora 软件临时安装在构建目录中后，kadichi 会运行带有数字编号的 `post_install_scripts`，数字表示它们执行的顺序。脚本包括：

- `0prelink.sh`——该脚本通过 `chroot` 在构建目录上运行 `prelim`。

- `02install.sh`——该脚本将启动脚本安装到 live CD，这些脚本用于解压文件并挂载启动 live CD 所需的文件系统。

- `03fstab.py`——该脚本修改 live CD 的 `/etc/fstab`，以包含需要挂载的文件系统。你可以向此脚本添加检测硬盘或存储介质分区的功能。

- `04userconfig.py`——该脚本运行 `authconfig` 和 `lockit` 命令来为 live CD 开启请求的安全功能。默认情况下，这些命令会启用密码并禁用防火墙和 SELinux 功能。此脚本还会运行 `ntsys` 命令，让 live CD 的用户选择开启或关闭哪些服务。

- `05fsclean.py`——该脚本删除或清理 live CD 上不需要目录和文件（例如临时文件和日志文件）。

- `06sysconfig.py`——该脚本创建 live CD 功能所需的特殊链接和目录。它还配置了 `firstboot`（让用户在 CD 启动时进行初始配置）和 `kicks`（在硬件检测时间，将 `RUN_FIRSTBOOT` 从 `YES` 改为 `NO` 是禁用 `firstboot` 过程的一种方法）。

- `07accounts.sh`——该脚本允许你向 live CD 中添加一个非 root 用户，这种方法是向 live CD 添加用户名和密码，该 live CD 需要运行 `firstboot` 并在 CD 完全启动前让用户输入自己的用户名。

你可以修改现有脚本或向此目录添加你自己的脚本，以更改 live CD 的设置方式。例如，你可以通过更改 `04auth.sh` 脚本来更改密码保护的类型。

## 第 7 章 构建基础 Fedora Live CD

### 更改启动参数和启动屏

与大多数 Linux CD一样，Fedora live CD 的初始启动过程由 Isolinux 引导加载程序引导。通过在 `/boot/isolinux` 目录中添加或修改文件，你可以添加选项、消息文件和启动屏，以更改 live CD 的外观和行为（有关 isolinux 如何工作的更多信息，请参见第 5 章“深入查看 Live CD 组件”）。

修改 live CD isolinux 文件的最佳方法可能是通过 `/usr/share/kadichi/install-boot.sh` 文件。除了将初始启动 CD 所的文件复制到 `/boot/isolinux` 目录外，它还会创建 `/boot/isolinux.cfg` 文件，该文件定义了初始启动屏幕和活动。

> 警告
>
> 在继续之前，请确保已拥有 `install-boot.sh` 文件的备份。如果此文件中出现错误，可能会导致你的 live CD 无法启动。

以下步骤将引导你通过修改 `install-boot.sh` 脚本，来添加或更改出现在启动屏幕上的文本，例如，在你的初始启动屏幕上添加图像并更改内核参数：

1. 创建一个存放额外文件的目录。例如，我在我的主目录（`/home/chris`）中创建了一个名为 `myfiles` 的目录：
   ```bash
   mkdir $HOME/myfiles
   ```

2. 在此示例中，我在 `/home/chris/myfiles` 中创建了两个启动文件（这种在 CD 完全启动前需要运行 `firstboot` 并让用户输入自己的用户名的 live CD 中添加用户名和密码的方法是向 live CD 中添加一个非 root 用户），并将它们启动文件复制到 `/boot/isolinux` 目录的启动文件（除了将初始启动 CD 所的文件复制到 `/boot/isolinux` 目录外，它还会创建 `/boot/isolinux.cfg` 文件，该文件定义了初始启动屏幕和活动）。

   第一个文件是 `boot.msg` 如下：
   ```
   isolinux.cfg
   ```

3. 使用任何你喜欢的图像创建启动屏并将其转换为 `.lss` 文件。在此示例中，我使用了 `/home/chris/myfiles` 下的 `boot.msg` 文件。

4. 接下来，你需要在 `isolinux.cfg` 文件中识别两个启动屏幕和启动屏。为此，你需要将它们复制到 `/boot/isolinux` 目录。为此，你需要编辑创建 `isolinux.cfg` 的 `kadichi` 文件。例如，以 root 用户身份在 `install-boot.sh` 文件中添加了**加粗**的行：
   ```
   #!/bin/bash

   sysdir=$1
   csysdir=$2
   kernel=$3
   ```

**图 7-4** 为你的 live CD 创建了启动屏图像。

> 注意
>
> 关于 live CD 启动过程中可以使用的启动屏和消息文件（包括如何输入控制代码来更改颜色），请参见第 5 章。

### 从 Kickstart 文件构建

Fedora Core 支持的安装类型之一被称为 kickstart 安装（引导启动文件安装）。通过创建一个包含指引 Fedora Core 安装过程所需信息的 kickstart 文件，你可以跳过 anaconda 安装的部分（或全部）步骤。

Kickstart 文件通常用于 Fedora Core 的无人值守安装。如果你在多台计算机上安装 Fedora Core（特别是当它们的配置相似时），kickstart 安装可以确保你每次都获得你所需的确切安装结果。

使用 kickstart 文件通过 Kadischi 创建你的 Fedora live CD 具有多个优势。当你使用 Kadischi 调整和自定义 live CD 时，你希望尽可能使用 kadischi 进行持续重新构建。创建 kickstart 文件可以避免你反复点击安装界面。它还能确保你获得精确的软件包、语言设置、网络设置以及其他 Fedora 特性，以便你持续重新构建 live CD。

以下是你可以创建 kickstart 文件以制作 live CD 的几种方法：

- **示例 kickstart 文件**——你从一个带有 Kadischi 的最小 kickstart 文件开始。Kadischi 中的示例最小 kickstart 文件名为 `minimal-1livecd.cfg`，位于 `/usr/share/kadiski/ks_examples` 目录下。该目录下还有 `standard-livecd.cfg`（可以构建更复杂的桌面系统）和 `xen-livecd`（可以构建启用 Xen 内核的 live CD）。该目录下的另一个 kickstart 文件是 `standard-livecd`，它构建一个包含 Fedora Core 发行版大部分内容的 DVD  ISO 镜像。

- **system-config-kickstart**——运行 `system-config-kickstart` 工具来创建自定义 kickstart 文件。`system-config-kickstart` 软件包（包含同名工具）是 Fedora Core 的一部分，但它默认不会安装。

- **来自安装的 kickstart 文件**——在对硬盘进行常规永久 Fedora Core 安装后，anaconda 会 `/root` 目录下放置一个名为 `anaconda-cfg` 的 kickstart 文件。该文件包含了你在安装期间使用的设置。因此，本质上你可以使用该 kickstart 文件来重复相同的安装（无需逐个通过安装界面），或创建一个具有相同设置和软件包的 live CD。

要使用 `kadishi` 命令通过 kickstart 文件创建 live CD，需要先创建 kickstart 文件，然后使用 `--kickstart` 标识它。这里是一个使用我用来开始的最小 kickstart 文件的 kadishi 命令示例：
```bash
# cd /usr/share/kadishi/ks_examples
# cp minimal-livecd.cfg $HOME/mydata/
# cd
# kadishi /FC6/.FC6-live.iso --kickstart=./mydata/minimal-livecd.cfg
```

此处显示的 `kadishi` 命令将在没有你人工干预的情况下运行。然而，在安装软件包时，它会弹出 Fedora Core 安装界面。为了完全不显示安装界面（例如，当你运行在纯文本 shell 环境时），请在命令行（带有 kickstart .FC6/.FC6-live.iso）中添加 `-C` 选项，如下所示：
```bash
# kadishi -C /FC6/.FC6-live.iso --kickstart=./mydata/minimal-livecd.cfg
```

你可以尝试这个最小 kickstart 文件。使用之前所示命令行，将使用最小 Fedora Core 安装来创建 live CD（压缩后总大小约为 163MB）。`minimal-livecd.cfg` 文件包含以下内容，其中 `\` 表示该行超过了我们的页面宽度，实际上应显示在同一行：
```bash
# Kickstart file automatically generated by anaconda.

install
lang en_US.UTF-8
langsupport --default=en_US.UTF-8 en_US en_US.UTF-8 en_US \
  en_US.UTF-8 en_US en en_US.UTF-8 en_US en
#xconfig --card RIVA TNT2" --videoram 4096 --hsync 31.5-37.9 \
  --vsync 50-70 --resolution 800x600 --depth 16
#network --device eth0 --bootno --proto dhcp \
  #hostname fedora.livecd
#network --device sit0 --bootno --proto dhcp \
  #hostname fedora.livecd
rootpw --iscripted $1XM/kV2A1GMYPu/4MrPKKKqbneMeL.
firewall --enabled
elinux --disabled
authconfig --enabledmd5
timezone Europe/Belgrade
bootloader --location=none
# 以下是你请求的分区信息
# 注意，你删除的任何分区都不会在此处表示
# 除非你先清空所有分区，否则
# 不保证能够正常工作
```

## 第 7 章 构建基础 Fedora Live CD

#clearpart --linux

# 我们不应该期望在完成后被提示，就让它不要发生吧。

reboot

%packages

# 为了形成最小包集而排除的软件包

- atk

- bind

- bind-libs

- bind-utils

- bluez-libs

- bluez-pin

- bluez-utils

- caching-nameserver

- cairo

- cyrus-sasl-plain

- expat

- freeglut

- GConf2

- htmlview

- irda-utils

... (剩余文本根据提供的 OCR 遵循相同逻辑)

### 实时版 Linux CD

> 提示
>
> 排除文档

通过排除 Fedora 软件包自带的文档，你可以为你的实时 CD 节省一些空间。Fedora Core 的全量安装程序会在 `/usr/share/` 下产生超过 200MB 的文档、手册页（man pages）和信息文件。若要排除安装到实时 CD 的软件包中的文档，应将 `%packages` 标记为 `%packages --excluded`。

%post

你可以在 `%post` 指令之后，分行添加你想要在软件包安装后运行的脚本。这是对你的实时 CD 进行一些初始配置的好地方。例如，你可以使用 `useradd` 添加一个用户。使用早些为 root 创建的加密密码，以下是在 `%post` 行之后添加用户的某些命令：
```
%post
/usr/sbin/useradd chris
/usr/sbin/usermod -p $1$oB11gYQPhb0JqjHyTYRcxrEwKN0 chris
/usr/bin/chfn -f "Chris Jones" chris
```

在所示的示例中，用户名被添加到实时 CD 中，并默认创建了家目录 `/home/chris`。`usermod` 命令为 chris 输入了密码。最后，`chfn -f` 将用户的全名设置为 Chris Jones。

要查找更多关于此项以及你在 kickstart 文件中可以设置的其他选项，请参阅 `/usr/share/doc/anaconda*` 目录下的 `kickstart-docs.txt` 文件。要获取该文件，你必须安装 `anaconda` RPM 软件包。

#### 添加安装后脚本

你可以更改任何安装后脚本（位于以下目录：`/usr/share/kadischi/post_install_scripts`），以修改你正在创建的 Fedora Core 实时 CD 内容。Fedora Core 被复制到构建目录，并在文件系统压缩并制作成 ISO 镜像之前进行。同样，你也可以将自己的脚本添加到 `post_install_scripts` 目录中。

运行安装后脚本时会将构建目录（包含新安装的 Fedora Core 实时 CD 系统）作为参数。脚本名称以数字开头，用指示每个脚本运行的顺序。

### 为你的 Fedora 实时 CD 选择软件包

要选择在 Fedora 实时 CD 上安装的软件包，你可以在 `%packages` 行之后指定软件包组或单个软件包。你也可以指定所选软件包不从已选的组中安装。

在大多数情况下，你可能想添加软件包组。使用 `@` 符号加组名（如 `Window System`）或 ID（如 `base-x`）来指示组。对于单个软件包，只需输入不带 `@` 符号的包名。以下是你你可以考虑添加到实时 CD 的组名列表（若要安装所有组，仅需使用 `@ Everything` 即可）：

- %packages

- @ Basic X Window System

- @ GNOME Desktop Environment

- @ KDE (K Desktop Environment)

- @ Editors

- @ Engineering and Scientific

- @ Graphical Internet

- @ Text-based Internet

- @ Office/Productivity

- @ Sound and Video

- @ Authoring and Publishing

- @ Graphics

- @ Games and Entertainment

- @ Server Configuration and Tools

- @ Web Server

- @ Mail Server

- @ Windows File Server

- @ DNS Name Server

- @ FTP Server

- @ PostgreSQL Database

- @ MySQL Database

- @ News Server

- @ Network Servers

- @ Legacy Network Server

- @ Development Tools

- @ X Software Development

- @ GNOME Software Development
