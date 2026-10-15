
# RHCE - RH302 红帽认证工程师认证考试备考课程：首次通过 RHCE-RH302 红帽认证工程师考试的备考指南

![](img/01872e44e0db1c79895b45feb5b484a6_0_0.png)

这本针对 RHCE - RH302 红帽认证工程师考试的自学备考指南包含了自测和通过考试所需的所有内容。涵盖了所有考试考点、深度解析和内部秘籍、对所有 RHCE 主题的完整解释、考试技巧和提示、250 多道真实的模拟题，以及旨在加强对 RHCE 概念的理解并帮助你首次尝试通过考试的练习。

你能想象自己如此看重这本书，以至于给作者写“感谢信”吗？

本书包含了以前从未印刷过的新练习和模拟题。通过提供大量的模拟题、节省时间的技巧以及其他地方无法获得的信息，本书将帮助你**首次**尝试通过 RHCE - RH302 红帽认证工程师考试。

购买它。阅读它。然后通过 RHCE - RH302 红帽认证工程师考试。

本书对所有考试目标提供了精准的关注，对 RHCE - RH302 红帽认证工程师实验考试中的所有主题进行了贯、简洁且全面的覆盖。

它包含了 250 多道模仿真实考试的题目（附带答案），以及“考试快速备习”功能，该功能可以在考前最后一个小时的准备中回顾所有要点。

涵盖了所有 RH302 考试考点，包括：

- 硬件安装与配置
- 启动过程
- Linux 文件系统管理
- 包管理与 Kickstart
- 用户和组管理
- 系统管理工具
- 内核服务与配置
- Apache 和 Squid
- 网络文件共享服务 (NFS、FTP 和 Samba)
- 域名系统 (DNS)
- 电子邮件 (服务器和客户端)
- 扩展 Internet守护进程 (xinetd)、Secure 包和 DHCP
- X 窗口系统
- 防火墙、SELinux 和故障排除

## 安装与硬件配置

### 1.1.概述

Red Hat Linux 是市场上主要的商业 Linux 发行版之一。Fedora Core Linux 是 Red Hat 的一个开源项目。Fedora Linux 每六个月发布一个新版本。

### 1.2.安装

Anaconda 是 Red Hat Linux 的默认安装程序。安装过程根据所使用的安装方法大致分为几个部分：

- DVD
- 网络
- 硬盘

#### 1.2.1. 使用 DVD

若要使用 DVD 开始安装，请将 DVD 介质放入电脑的 DVD 光驱中，并将 BIOS 设置为从 DVD 光驱启动。该过程的步骤如下：

- 检查 DVD 介质。
- 选择安装期间使用的语言。
- 选择键盘布局。
- 选择安装类型。

对于新安装：

- 选择要安装的软件包。
- 选择分区方案（自动分区或手动分区）。
- 选择分区方式（硬盘上的可用空间、使用当前分区和自定义分区）。
- 如果选择自定义分区，请至少创建一个 `/` 分区和一个交换分区（swap partition）。
- 将引导程序安装到 MBR。
- 配置网络设备。
- 设置防火墙选项。
- 选择系统支持的语言。
- 选择系统时区。
- 输入 root 密码。
- 选择软件包。

安装完成后，从光驱中取出 DVD 介质。用户必须接受许可条款、配置防火墙并配置声卡。

对于现有安装：

#### 1.2.2. 使用硬盘

对于硬盘安装，假设 Red Hat Linux 已经在电脑上运行。在硬盘安装中，将 DVD 的所有文件复制到安装期间使用的分区中。

然后将 DVD 介质的 `vmlinuz` 和 `initrd` 文件复制到 `/boot` 目录。这些文件是启动安装过程所需的。Red Hat 默认安装 GRUB 作为引导程序。为了启动安装过程，需要告知引导程序 `/boot` 目录中的文件。

在 `/boot/grub/grub.conf` 文件中添加以下条目来实现此目的：

```
title Red Hat-Installation
root (hd0,7)
kernel /vmlinuz
initrd /initrd.img
```

`root(hd0,7)` 表示 `/boot` 分区位于第一个硬盘的第八个分区。

完成上述步骤后，重启电脑。在 Grub 菜单上选择 Red Hat Installation 以开始安装过程。

随后，登录屏幕会提示用户输入用户名和密码。

#### 1.2.3. 使用网络

对于网络安装，应将安装文件复制到作为安装服务器的电脑上。

- 如果是 Web 服务器或 HTTP 服务器，文件需要复制到 `/var/www/html` 目录。
- 如果是 NFS 服务器，应使包含安装文件的目录可用。
- 如果是 FTP 服务器，将文件复制到 `/var/ftp/pub`。

## 启动文件 (Kickstart File)

注意：当从网络或硬盘安装时，请在安装过程的第一个屏幕上选择文本模式并选择 INSTALL OR UPGRADE（安装或升级）。在启动提示符处输入命令：

```bash
boot
```

成功安装 Red Linux 后，将根据用户在安装过程中选择的选项创建一个 `/root/anaconda-ks` kickstart 文件。

## 创建 Kickstart 文件

用户可以选择使用图形化工具创建 kickstart 文件，也可以打开文本编辑器编写命令。

### 文本文件

- `install`
- `cdrom`
- `lang=en_UTF-8`
- `keyboard`
- `config --startx`
- `network --device eth0 --boot dhcp`
- `rootpw`
- `firewall --enabled`
- `authconfig`
- `selinux --enforcing`
- `timezone`
- `bootloader --location=mbr --driveorder=sda --append="quiet"`

`install` 选项表示是新安装还是对现有系统的升级。`cdrom` 显示安装方法，NFS、FTP、HTTP 是其他可用于 NFS、FTP、硬盘的选项。

- 对于 FTP 方法，使用 `-url` 指定 FTP 名称
- 对于 HTTP 方法，使用 `-url` 指定 HTTP 名称
- 对于硬盘，使用 `harddrive --dir=/path=partition`
- 对于 NFS 方法，使用 `-nfs --servername --dir=directory` 目录

第三行显示安装期间使用的语言。第四行选择键盘布局。`config` 用于配置显示器和显卡。`network` 命令用于配置网络。在上述情况下，它配置以太网接口。`rootpw` 表示密码。`firewall` 设置标签——`enable` 表示启用，`option` 表示禁用。`selinux` 用于设置增强 Linux 安全选项——`enforcing`、`permissive`。`timezone` 用于选择时区。`bootloader` 命令用于设置默认引导加载程序安装的分区。

## 图形化工具

打开终端并输入命令 `system-config-kick` 开始配置。

```bash
root@localhost ~]# system-config-kick
```

用户可以使用图形界面选择选项，系统将自动生成 kickstart 文件。要使用 kickstart 安装，请遵循以下步骤：

- 创建 kickstart 文件
- 从光驱、网络或本地硬盘拷贝 kickstart 文件
- 在安装期间的启动提示符上使用上述命令

```bash
ks=cdrom
ks=file:/path/anaconda-ks.cfg
ks=ftp://path
ks=hd:dev (dev = 'hd', example)
ks=http://path
ks=nfs:options
```

![](img/01872e44e0db1c79895b45_18_0.png)

## 配置硬件

`/etc/sysconfig/hwconf` 文件包含了已安装硬件的列表。运行该命令可以检测并配置系统中更改的硬件。它在每次 Red Hat 设备重启时都会运行。它检查 `/etc/sysconfig/hwconf` 文件中的已安装硬件，并与当前硬件数据进行匹配。以下是 `/etc/sysconfig/hwconf` 文件的格式：

| Key | Value |
| :--- | :--- |
| class | CDROM |
| bus | SCSI |
| detached | 0 |
| device | scd0 |
| desc | HL-DT-ST CD-RW G8526B |
| host | 1 |
| id | 0 |
| channel | 0 |
| lun | 0 |
| class | VIDEO |
| bus | PCI |
| detached | 0 |
| driver | i2c-i810 |
