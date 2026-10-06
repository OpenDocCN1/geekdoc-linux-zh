

-   检查无法正常工作的硬件 —— 如果打印机、网卡或其他硬件组件无法立即工作，请尝试使用系统 -> 管理（System -> Administration）菜单下的工具来配置这些项目（书中全文均有相关描述）。如果仍然不起作用，还有几个标准位置可以查找：查看 Fedora 发布说明（Fedora Release Notes）。在发布说明页面上，寻找指向帮助与支持（Help and Support）的链接。访问 Bugzilla 页面 (https://bugzilla.redhat.com) 并搜索出现故障的硬件名称或型号。

如果你已经检查了这些主题，就可以阅读书中任何感兴趣且令你兴奋的内容。

本章的其余部分将介绍与安装 Fedora 和 RHEL 相关的特殊主题。如果您对安装的 Fedora 系统感到满意，可以跳到下一章。

## 特殊安装程序

如果您不想或无法使用从 DVD 或 CD 安装 Fedora 的程序，接下来的章节中的程序为您提供了替代方案。启动安装的替代方法，例如 PXE 或 USB 闪存盘（如果您的计算机没有可启动的 DVD 或 CD 驱动器）。

在安装程序启动后，请使用随后的“从其他介质安装”章节学习如何从 DVD 或 CD-ROM 的介质安装 Fedora（使用 FTP、HTTP、NFS 或硬盘安装）。如果您希望在安装时在另一计算机上显示安装界面，请参考“启动 VNC 安装”章节。后续的小节描述了如何进行 kickstart 安装。

## 启动安装的替代方案

您的计算机可能没有 DVD 或 CD 驱动器，或者有一个无法启动的驱动器，因此您需要找到另一种启动安装程序的方法。虽然不再支持从 1.44MB 软盘启动安装（2.6 内核无法放入其中），但您仍有几个替代方案：

-   从硬盘启动安装
-   从 USB 闪存盘或其他 USB 驱动器启动
-   进行 PXE 安装

以这些方式启动安装的程序将在后续章节中描述。

## 从硬盘启动安装

启动安装过程与启动普通的 Linux 系统类似。要从硬盘启动安装，您只需要做：

-   将启动安装所需的文件放在您的硬盘上。
-   配置您的引导加载程序，告诉您的计算机的主引导记录（MBR）关于这些安装文件的信息。

本文假设计算机上已经运行了 Fedora 或 Red Hat Enterprise Linux 系统（因此您正在进行 Fedora 的升级或全新安装）。它还假设您能够找到将这些文件放入硬盘的方法（我将描述如何从可以挂载但无法启动的 DVD 或 CD 来操作）。

> 注意：请参本章稍后关于设置服务器的章节，因为您可能需要从 DVD 以外的地方访问 Fedora 安装 DVD 的内容。

1. 将 Fedora DVD 插入到运行 Fedora 或 Red Hat Enterprise Linux 的 DVD 驱动器中。

如果 DVD 没有自动挂载，请作为 root 用户使用以下命令挂载它：

```bash
# mount /media/disk
```

注意 DVD 的挂载点可能在不同的位置。如果 DVD 未挂载，另一种选项是创建一个挂载点并将 DVD 挂载在那里。例如，您可以执行 `mkdir /mnt/dvd ; mount /dev/dvd /mnt/dvd`。

```bash
# cd /media/disk/isolinux
# cp initrd.img /boot/initrd-boot.img
# cp vmlinuz /boot/vmlinuz-boot
```

> 注意：如果您无法在机器上挂载 DVD 或 CD，可以使用 scp 从网络上的另一台机器复制文件。或者，可以从包含 Fedora 发行的 Fedora FTP 站点将这些文件下载到您的 /boot 目录。

3. 修改您的 /boot/grub/grub.conf 文件，包含您刚刚添加到 boot 目录的 vmlinux 和 initrd 文件条目。例如：

```text
title Fedora 10 installation
root (hd0,0)
kernel /vmlinuz-boot
initrd /initrd-boot.img
```

此示例假设您的 /boot 分区存在于 IDE 硬盘的第一个分区 (hd0, 0) 上，即 /dev/sda1。您可以输入 `df` 来查看您的 /boot 分区的位置。

4. 重启您的计算机。
5. 当启动屏幕出现时，按向下方向键移动到 Fedora 安装。

## 第 2 章：安装 Fedora

### 从 USB 启动安装

大多数较新的主板都可以从 USB 设备启动。要从 USB 启动 Fedora，请使用以下操作：

1. 将 CD 插入驱动器。
2. 如果 CD 没有自动挂载。
3. 如果 CD 没有自动挂载，请作为 root 用户使用以下命令挂载它：

```bash
# mount /media/disk
```

注意 DVD 的挂载点可能在不同的位置。如果 DVD 未挂载，另一种选项是创建一个挂载点并将 DVD 挂载在那里。例如，您可以执行 `mkdir /mnt/dvd ; mount /dev/dvd /mnt/dvd`。
4. 插入 USB 驱动器。如果没有出现安装启动屏幕，请检查 BIOS 以设置 USB 设备。
5. 如果启动屏幕出现，您将使用以下进行安装。

### 使用 PXE 启动安装

开始 Fedora 安装的另一种方法是使用预执行环境 (PXE)。通过 PXE，安装过程通过设置 BIOS 寻找网络服务器开始。有关如何执行 PXE 的信息，请参考 syslinux 软件包。

## 从其他介质安装

一旦安装过程启动（如上一节所述从 DVD 启动），Fedora 将允许从 Web 服务器 (HTTP)、FTP 服务器、共享 NFS 目录或硬盘获取要安装的实际包。

> 注意：要使用 HTTP、FTP 或 NFS 安装，您的计算机必须通过以太网连接到可以访问该发行版的网络上。您无法使用拨号连接。对于本地磁盘安装，发行版必须复制到未使用的本地磁盘（或独立分区）上。详情请参阅“设置 HTTP、FTP 或 NFS 服务器”章节。

## 开始安装

您可以使用随书附带的 DVD（或上一节描述的替代方法）开始启动网络或硬盘安装。

1. 将 Fedora DVD 插入驱动器。
2. 重启计算机。您应该能看到 Fedora 启动屏幕。
3. 启动：在启动屏幕高亮第一个条目时按 Tab 键，并在启动提示符末尾添加以下内容：
```text
askmethod
```
系统会提示您选择语言。
4. 选择语言。系统提示您选择键盘类型。
5. 选择您的键盘类型。系统提示您选择一种安装方法。
6. 选择安装方法。选择以下任何安装方法：本地 CDROM、NFS 镜像、FTP 或硬盘。
7. 配置网卡。对于任何一种网络安装，系统都会要求您从列表中选择您的以太网卡。

