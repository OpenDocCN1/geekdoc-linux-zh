
优点是 Kickstart 提供了大量的数传输选项。使用 Jumpstart 时，NFS 是你唯一的选择。使用 Kickstart 时，你可以通过 NFS、FTP、CD-ROM 或客户端硬盘上的另一个分区将包和配置传输到客户端。仅 FTP 选项就值值了；通过高带宽连接，你可以轻松地通过互联网上的许多 Red Hat 镜像之一通过网络安装整个 Red Hat Linux 发行版。你只需要提供正确配置文件的 URL 即可。

# 站点镜像

镜像是互联网上的一个站点，包含另一个站点全部或部分的副本。它的目的是在互联网上传播高访问数据（如软件发行版）的副本，以至于所有人都不会因请求数据而导致单个站点过载。Red Hat 在互联网上有许多不同的镜像，访问 http://www.RedHat.com/mirrors.html 获取完整列表。

Kickstart 配置文件可以包含大量的硬件信息，因为 Linux 必须支持极其大量的第三方硬件。Kickstart 配置文件还包含许多用于分区、网络配置和要安装的软件包的指令。列表 3.2 显示了一个典型的 Kickstart 配置文件。

## 列表 3.2 示例 Red Kickstart 配置文件

```
## Installation Language
lang en us
# Use DHCP to obtain a network address
network --bootproto dhcp
# Install over the network from a NFS share
nfs --server installer.example.com --dir /usr/local/Red Hat/i386
# Use US keyboard configuration
keyboard as us
## zero out the master boot record
zerombr yes
# format all existing partitions
clearpart --all
## partition information
# /home --will grow to use the rest of the disk, up to 8000 MB
part /boot --size 35
part swap --size 128
part / --size 200
part /user --size 4000
part /home --grow --maxsize 8000
## perform the installation
install
# use a generic 3-button PS/2 mouse
mouse a generic3ps/2
## set your timezone
timezone --utc EST5EDT
## skip X configuration since this is a server
skippx
## set the root password
rootpw changeme
## reboot after installation
reboot
```

## 列表 3.2 续

```
# use shadow passwords with MD5 encryption
auth --usershadow --enablemd5
# install boot loader in master boot record
bootloader --location=mbr
# install packages (groups of packages begin with '@')
%packages
@ Base
@ Mail/WWW/News Tools
@ Networked Workstation
@ Network Management Workstation
@ C Development
@ Development Libraries
python
cftpp
bind-utils
```

# Kickstart 的图形界面

如果你不习惯编辑晦涩的配置文件，Kickstart 还有另一种配置方式。Red Hat 现在附带 Kickstart “配置器”——一个 Kickstart 配置工具的图形界面。

Kickstart 与其对应品 Jumpstart 不同，它要求从软盘、CD-ROM 或硬盘启动；这一个限制对于该安装包来说是一个严重的缺点。如果你没有硬编码启动选项，你必须手动输入它们才能启动。

# 制作启动介质的多个副本

为了避免在不同机器之间不断更换软盘或 CD-ROM，只需制作多个副本即可。

Kickstart 的另一个缺点是它缺乏。服务器没有办法根据时间进行更改。这个额外的步骤通常不会太麻烦，但应该认真考虑在。

# 安装应用程序

你可以通过多种方式在 Unix 平台上安装应用程序，这取决于应用程序及其包。某些包安装在预定的位置，而其他包则是。考虑到软件安装方法的多样性，跟踪内容是非常容易的。

![](img/894492738e87926732b8d6f9a04180_99_0.png)

# 记录安装详情

不要忘记记录你安装的每一件软件。你应该在日志本中为每个系统保留一个独立的章节，这样你就不需要阅读整个日志来查找单台机器上安装了什么。你应该包含的某些细节包括应用程序名称、版本号、已应用的补丁、供应商名称和网站、配置和编译选项（如果是从源码编译）、安装位置、安装后配置以及已知错误或问题。

# 管理未封装的软件安装

在系统上安装软件时，你必须能够跟踪安装以及它放置的所有应用程序文件。应用程序构建和安装过程类型决定了你必须在管理上投入多少精力。你通常通过以下方式之一接收应用程序：

- 源代码
- 程序和配置文件的 `tar` 包（使用 `tar` 创建的存档），你需要手动安装
- 由操作系统包管理软件安装的包

通过预包二进制分发安装应用程序对你来说工作最少；包会创建相应的目录及其其中的应用程序文件。但也有几个原因是你可能想要从源码构建应用程序安装：

- 你可能需要修改应用程序的功能。
- 应用程序可能安装在次优目录中，而你可能无法更改它。
- 你可能出于安全考虑审计源码。

## 第 3 章 · 部署你的系统

- 你可能需要通过更激进的编译器优化来提高应用程序的性能。
- 某些应用程序仅以源码形式分发。

从源码构建程序时，确定将软件存放在何处以及如何管理其包含的文件是你的责任。随着你在处理这些应用程序安装方面积累的经验，你将设计出属于自己的用于管理该过程的系统。但是，构建和管理软件仓库是许多系统管理员用于跟踪软件安装的有效方法。软件仓库是一个目录树，你可以在其中安装所有软件；它将所有内容都保放在一个地方，使得软件文件易于查找。

## Gnu C 编译器 (GCC)

Unix 上最流行的编译器是 GCC，即 Gnu C 编译器。虽然 GCC 生成的可执行文件并不总是比你操作系统自带编译器生成的文件更优化，但该编译器是免费的，并且几乎可以保证能够成功编译大多数第三方应用程序。你可以在 http://www.gnu.org/software/gcc/gcc.html 下载 GCC。

将仓库与系统上的任何其他软件安装位置分开。你不希望将应用程序与关键系统基础设施混合在一起。例如，`/usr` 可能不是存放新软件的最佳位置，因为系统软件存储在 `/usr/bin`，手册页存储在 `/usr/man`，而关键系统库存储在 `/usr/lib`。你还应该考虑类似 `/usr/local` 的位置，因为许多旧软件安装在该位置。最终，你应该咨询你所操作系统的文件系统标准，这些标准定义了文件系统中每个目录的用途以及特定类型的软件应该安装在何。你应该能在你操作系统的文档中找到这些信息。

让你的软件仓库对你的系统来说是唯一的，这样它就不会被系统软件或第三方包干扰。存储仓库的一种技术是在 `/usr` 中创建一个以你的组织命名的特殊目录。如果你的公司名称是 XYZ, Inc.，你可能想将此目录命名为 `/usr/xyz`，并将文件放在 `/usr/xyz/bin`、`/usr/xyz/man`、`/usr/xyz/lib` 以及任何你安装软件文件的地方。

## GNU Configure 将应用程序安装到指定位置

大多数软件都允许你指定安装位置，而许多开源发行版提供的流行的 GNU configure 接口非常适合这种存储解决方案。在包含源码的目录中执行以下 GNU configure 指令，将确保所有文件都使用 `/usr/xyz` 前缀进行安装：

```
/configure --prefix=/usr/xyz
```

你可以在 http://www.gnu.org/software/autoconf 了解更多关于 GNU configure 的信息。

# UNIX 系统管理入门增强版

许多管理员发现，当将软件安装到独立的仓库（如 `/usr/xyz`）时，他们仍然无法判断哪个文件属于哪个包。即使是最好的日志本也无法告诉你仓库中每个文件的位置。更令人困惑的是版本困境：你如何能轻松地看出仓库中安装了哪个版本的软件？解决这个问题的方案之一是对你的仓库进行分区，将其进一步分离为应用程序目录，甚至可能是版本目录。
