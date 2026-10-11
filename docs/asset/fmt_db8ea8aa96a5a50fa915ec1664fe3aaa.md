
# 在闪存/USB 设备上创建 Linux 安装程序（通过 Microsoft Windows）

上一节内容假设你已经可以访问一个正在运行 Linux 发行版的系统，并且可以轻松地从 shell 中运行任何命令。在这里我们采取不同的方法，假设你只能够访问一个运行最新版本 Microsoft Windows 的系统。

在特定系统的解决方案上创建 Linux 安装程序有两种方法，另一种更具通用性。无论采用哪种方法，目标在所有平台（Windows、Linux、Mac OS X）上都是相同的：为 Fedora、RHEL、openSUSE、Debian、Ubuntu 以及其他 Linux 发行版创建可启动且可安装的闪存/USB ，而无需刻录 CD 或 DVD。

## 附录 A 在闪存/USB 设备上创建 Linux 安装程序

存在特定发行版的方法是因为各种流行的 Linux 发行版开发了易于使用的 GUI 工具，可以帮助用户成功地将特定发行版的 ISO 镜像写入闪存/USB 设备。这里列出了一些特定发行版的方法：

| Linux 发行版 | 安装程序名称（Windows 可执行文件） | URL |
|---|---|---|
| Debian | win32-loader | http://goodbye-microsoft.com/ |
| Fedora/RHEL/CentOS | liveusb-creator | https://fedorahosted.org/liveusb-creator/ |
| openSUSE | ImageWriter (Studio ImageWriter) | https://github.com/downloads/openSUSE/kiwi/ImageWriter.exe |

通用方法依赖于第三方（而不是特定的发行版供应商）并维护 GUI 工具，用户可以使用这些工具轻松地将不同发行版的安装程序文件转换为可在闪存或 USB 设备上启动的格式。其中一种通用的第三方解决方案是 UNetbootin (`http://unetbootin.github.io/`)。另一个流行的通用解决方案是名副其实的 USB Installer (`www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/`)。

接下来的章节将引导你通过运行 Windows 的系统在基于闪存/USB 的设备上创建 Linux 安装程序的三个情况。我们将探索使用特定发行版的方法以及使用第三方解决方案。

## 在 Windows 上使用 Live USB Creator 创建 Fedora 安装程序

在本节中，我们将介绍如何使用示例特定发行版解决方案（Live USB Creator）通过运行 Windows 的系统在闪存/USB 介质上创建 Fedora 安装程序的过程。

你需要：

- 一个运行 Microsoft 操作系统家族最新成员的系统：Windows Vista, 7, 8, 8.1 或 10 等
- 一个尺寸合适的闪存/USB 设备（足够大以存放 Fedora 的 ISO 文件）
- 所选 Fedora 版本的 ISO 或其他镜像文件
- 一个可以从闪存设备启动的目标系统

以下是需要遵循的步骤：

1. 在登录 Windows 系统时，
2. 如果你还没有这样做，请下载你想要写入闪存/USB 设备的 Fedora 版本的 ISO 镜像文件副本。你可以从 `https://getfedora.org` 下载不同版本的 Fedora 镜像 ISO 镜像。确保你下载文件到的 Windows 文件系统/分区上有足够的空闲空间。
3. 将闪存/USB 设备插入 Windows 系统的相应端口。
4. 双击你之前下载的 Live USB Creator 可执行文件（`liveusb-creator-<version>-setup.exe`）以启动应用程序的安装程序。点击 `Install`（安装）按钮将程序安装到子目录位置（即 `C:\Program Files (x86)` 或 `C:\Program Files\`）。

如果提示你提供 Windows 系统上具有管理员权限的用户凭据，请提供要求的信息并点击确定。

如果提示有关从未知/未验证发布者处安装/运行程序的警告，请选择“是”或“运行”继续。

5. 程序安装完成后，你将看到另一个对话框，询问你现在是否运行 Live USB Creator。

![](img/9f6657924397c33f088db5321b751a83_788_0.png)

> 注意 如果你稍后通过普通的 Windows 开始或程序菜单运行该程序，你需要以具有管理员权限的用户身份启动。

6. 启动 Live USB Creator 后，你将看到一个提供选项的对话框。你可以选择使用现有的 ISO 镜像（Use Existing Live ）或下载所需的 Fedora（Download ）。
7. 在同一个对话框中，选择合适的闪存/USB 设备。
8. 点击 `Create`（创建）按钮开始过程。
9. 过程完成后，你将看到一条成功消息。
10. USB 驱动器准备好后，你可以重启电脑并从 USB 设备启动。
11. 如果设备未启动，检查 BIOS/UEFI 设置以确保已启用 USB 启动。
12. 最后，在安装完成后你可以拔掉设备。

## 在 Windows 上使用 UNetbootin 创建 Ubuntu 安装程序

你需要：

- 一个运行 Microsoft 操作系统家族最新成员的系统：Windows Vista, 7, 8, 8.1 或 10 等
- 一个尺寸合适的闪存/USB 设备（足够大以存放 Ubuntu 的 ISO 文件）
- 所选 Ubuntu 版本的 ISO 或其他镜像文件
- 一个可以从闪存设备启动的目标系统

以下是需要遵循的步骤：

1. 在登录 Windows 系统时，
2. 如果你还没有这样做，请下载你想要写入闪存/USB 设备的 Ubuntu 版本的 ISO 镜像文件副本。你可以从 `www.ubuntu.com` 下载不同版本的 ISO 镜像。确保下载到的 Windows 文件系统/分区上有足够的空闲空间。
3. 将闪存/USB 设备插入 Windows 系统的相应端口。
4. 双击你之前下载的 UNetbootin 可执行文件（`unetbootin-windows-latest.exe`）以启动应用程序。如果提示你提供 Windows 系统上具有管理员权限的用户凭据，请提供要求的信息。
5. 你会在 UNetbootin 上看到多个选项。你可以选择所需的 Linux 发行版（Distribution, Select Version 选项）或使用现有的 ISO 镜像（Diskmage 选项）。
6. 我们将让 UNetbootin 指向步骤 2 中下载的 Ubuntu 镜像文件。
7. 在 Drive 部分，从列表中选择与闪存/USB 设备关联的器符。
8. 点击 `OK` 按钮开始过程。
9. 过程完成后，你将看到一条成功消息。
10. USB 驱动器准备好后，你可以重启电脑并从 USB 设备启动。
11. 如果设备未启动，检查 BIOS/UEFI 设置以确保已启用 USB 启动。
12. 最后，在安装完成后你可以拔掉设备。

8. 下面显示了我们示例系统上完成的对话框。你可以看到，我们选择了 `ubuntu-server-amd64.iso` 镜像文件写入分配了盘器符 G 的目标设备。

![](img/9f6657924397c33f088db5321b751a83_791_0.png)

9. 点击“确定”开始进程。
10. 进程完成后，关闭 UNetbootin 窗口。你现在可以拔掉闪存/USB 设备，并将其插入到想要安装 Linux 的新系统的相应端口中。
11. 如必要，配置目标系统的 BIOS 或 UEFI 以便从闪存/USB 设备启动。一旦进入安装程序，请按照第 2 章中描述的步骤或发行版厂商指定的步骤进行安装。

### 在 Windows 上使用 Pendrivelinux.com 的通用 USB 安装程序创建 openSUSE 安装程序

Universal USB Installer (UII，通用 USB 安装程序) 是 Pendrivelinux.com 提供的软件，可用于将各种 Linux 发行版写入闪存/USB 驱动器。尽管该项目已经存在一段时间，但它最近已获得一些主流发行版的认可，成为在 Windows 系统上创建发行版安装程序的首选方法。

在本节中，我们将介绍在 Windows 系统上使用 UII 在 USB 驱动器上创建 openSUSE 安装程序的流程。

你需要准备：

- 一台运行微软操作系统系列任一最新成员的系统：Windows Vista, 7, 8, 8.1 或 10 等
- 一个大小合适的闪存/USB 设备（足够大以容纳该发行版的 ISO 文件）
- 目标 openSUSE 版本的 ISO 或其他镜像文件
- 一个可以从闪存设备启动的目标系统

以下是需要遵循的步骤：

1. 登录到运行 Windows 的系统后，使用网络浏览器从项目网站 `www.pendrivelinux.com/universal-usb-installer` 下载最新版本的 Ubuntu。
2. 如果你还没有下载，请下载你想要写入闪存/USB 设备的 openSUSE 版本的 ISO 文件副本。你可以从主页（`www.opensuse.org`）开始浏览并搜索你所需的版本的 ISO 镜像。确保你下载时所在的 Windows 系统/分区有足够的空闲空间。
3. 将闪存/USB 设备插入主机系统上的相应端口。
4. 双击之前下载的可执行文件（`Universal-USB-Installer-<VERSION>.exe`）以启动应用程序。如果提示你需要提供 Windows 系统上具有管理员权限的用户凭据，请提供要求的信息。如果弹出关于从未知发布者运行程序的警告，请选择“是”或“运行”以继续。
5. 你将看到一个屏幕，你可以在其中选择要设置的 Linux 发行版。点击标记为“Step 1”的下拉字段以显示大量的发行版。从列表中搜索并选择 openSUSE。
6. 使用第二个字段（标记为“Step 2”）中的“浏览”按钮找到并选择你下载的 ISO 镜像。
7. 在“Step 3”中勾选“显示所有驱动器”复选框，然后从列表中选择与闪存/USB 设备相应的驱动器号。可用，勾选复选框以格式化你选择的 USB 驱动器。
8. 下面显示了我们示例系统上完成的对话框。你可以看到我们选择了 `openSUSE-LATEST-x86_64.iso` 文件写入分配了盘器符 F 的目标设备。

![](img/9f6657924397c33f088db5321b751a83_793_0.png)

9. 点击“确定”开始进程。
10. 进程完成后，关闭 UNetbootin 窗口。你现在可以拔掉闪存/USB 设备，并将其插入到想要安装 Linux 的新系统的相应端口中。
11. 如必要，配置目标系统的 BIOS 或 UEFI 以便从闪存/USB 设备启动。一旦进入安装程序，请按照第 2 章中描述的步骤或发行版厂商指定的步骤进行安装。

## 附录 B 虚拟机

Linux 虚拟机管理：入门指南

Basic System Requirements

The following sections cover the requirements in more detail. The host system is the system you will run. The VM will be constrained by whatever the host has. For best performance, the CPU of the host system should at least support Virtualization Technology (Intel VT) or AMD Virtualization (AMD-V) extensions

While inside an Intel-based host system running Linux, check whether the Intel processor shows the desired flag in `/proc/cpuinfo` by using the `grep` command, like so:

```
```
