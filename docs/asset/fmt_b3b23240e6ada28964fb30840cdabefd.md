
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait need actual text. Let's redo properly.

The instruction says process given text. I need to output processed version.

Let's produce final output with headings.

[content]
Red Hat 为 Red Hat Enterprise Linux 维护了大量的文档（见表 1-1）。从 Red Hat 首页，您可以点击进入文档页面。文档页面提供了一个弹出菜单从中可以选择产品。默认选择 Red Hat Enterprise Linux。点击打开 Red Hat Enterprise Linux 文档页面，该页面列出了全套 Red Hat 手册。文档按版本排列。文档涵盖了虚拟化、全局文件系统 `GFS`、逻辑卷管理 `LVM` 和安装指南等主题。还提供了 Tip、TO-HOW 和 FAQ 文档。Red Hat 文档在 GNU 通用公共许可证下免费提供。在向您的系统安装 Red Hat Enterprise 之前，您可能想要检查一下安装指南。《Red Hat 杂志》提供了有关最新功能的信息。

Fedora 的文档可以在 `docs.fedoraproject.org` 找到，并在 `fedoraproject.org/wiki` 提供了专门的主。Fedora 安装指南对您的所有安装步骤提供了详细描述。Fedora 桌面用户指南涵盖了登录、使用应用程序和访问网络等桌面操作。有几个专门的 Fedora 支持站点可以提供有用信息，`fedoraforums.org` 是

![](img/af27012edcd42a8b40f811834.png)

## 第一部分：入门指南

| 参考文献 | 描述 |
|---|---|
| www.redhat.com | Red Hat 站点 |
| www.redhat.com/magazine | 包含最新进展的《红帽杂志》 |
| www.centos.org | 社区企业操作系统 CentOS。（源自 Red Hat Enterprise 的 Linux 发行版） |
| fedaproject.org | Fedora 项目（早期页面位于 redhat.com） |
| docs.fedoraproject.org/wiki | Fedora 的文档和支持。包括关于安装、桌面使用和 SELinux 的说明 |
| fedoraforums.org | 用户讨论论坛，由 Fedora 项目背书；包含 FAQ 和新闻 |
| www.fedafaq.org | 非官方 FAQ，带有快速帮助主题，如启用 MP3 和 3-D 图形支持 |
| fedoranews.org | 收集 Fedora 的最新新闻和进展，以及关于近期更改的文章和博客 |
| www.linux-foundation.org | Linux 基金会，官方 Linux 开发 |
| www-kernel.org | 最新内核 |

**表 1-1** Red Hat 和 Fedora 资源

# 第一章：Red Hat 与 Fedora Linux 简介

## Fedora 7

Fedora 7 提供了更加流畅的视觉效果和体验，拥有全新的 Echo 图标和响应迅速的桌面，还提供了新的管理工具，以便更方便地进行安装、软件更新和管理。

- Fedora Core 和 Fedora Extras 仓库已合并为一个 Fedora 软件仓库。
- Fedora 磁盘以一系列“变体”（spins）的形式发布，它们收集了用于不同目的的软件。目前有三个变体：GNOME、KDE 和 Fedora。Fedora 变体包含系列工作站和服务器软件。你可以通过这些变体来开发自己的定制化变体。
- Fedora 提供了 Live CD，你可以从 CD-ROM 驱动器运行 Fedora。
- 通过备性的 `compiz` 窗口管理器，可以启用桌面 AGLX 效果。在“管理 | 偏好 | 外观 | 桌面效果”选项中，选择“启用效果”。你将看到窗口在移动时会晃动，且工作空间内会旋转。
- 为交换分区（swap）和非根分区提供了加密文件系统。使用 `gnome-luks-format` 或 `cryptsetup` 来创建加密分区。
- 内核包含了基于内核的虚拟化（KVM）支持。KVM 使用支持硬件虚拟化的处理器，如 Intel VT（虚拟化技术）和 AMD SVM（安全虚拟机）处理器来支持硬件级操作系统。标准的 Intel 和 AMD 处理器已经提供了此类支持。
- 使用虚拟机管理器（Virtual Machine Manager）管理和安装所有 KVM 和 Xen 虚拟机。
- 为了更好地管理 SELinux 配置，你可以使用 `auditd`，它会通知你任何问题。
- `java-gc-collect` 集合提供了 Java 运行时环境兼容性，包括 GNU Java 运行时 `libgcj`、Eclipse Java 编译器 `ecj` 以及一组封装器和链接 `java-gc-tomcat`。
- 本地化通用用户目录 `xdg-user-dirs`。自动在用户目录中设置“文档”、“视频”和“音乐”目录。
- 通过“系统 | 偏好 | 屏幕分辨率”可以使用用户控制的屏幕分辨率。
- Pirut 程序管理器直接从 Yum 在线仓库管理软件。
- 使用 Mono `Novell` 支持 `.NET`。包含了支持 `.NET` 的软件包，如 F-Spot 和 Beagle 桌面搜索。
- 具有自动检测可移动设备的功能，如 USB 驱动器、数字相机和读卡器。CD/DVD 磁盘被视为可移动设备，在插入时会自动显示并访问。

![](img/af27012edddcf42a8b40fad81183c10b_46_0.png)

## 第一部分：快速入门

- 串行 ATA 驱动程序现在已支持 IDE 硬盘。所有 IDE 设备都以 `sd` 前缀命名，而不是 `hd` 前缀。
- Fedora 提供了完整的 IPv6 网络协议支持，包括自动寻址和重命名。
- SELinux 是 Fedora 不可或缺的组件，提供系统范围的安全防护。你可以设置不同的控制级别并创建自己的策略。SELinux 使用模块进行配置。
- 包含了广泛的多媒体应用，例如视频播放器和电视收视器，并提供了来自 `freesrmpr.net` 的各种多媒体应用和库的兼容支持，例如 DVD 和 DivX 支持。
- 通过网络监控器（Network Monitor），你可以自动选择无线连接。
- 应用程序通过来自 `freedktop.org` 的硬件抽象层 `HAL` 获取有关热插设备的信息。这允许 GNOME 等应用程序轻松地显示和管理可移动设备。
- 所有设备在逻辑上都被视为可移动设备，并由 `udev` 自动配置。设备仅是指无法移除的设备。此功能的目的是让 Linux 适应各种设备，如数字相机、PDA 和手机手机。PCMCIA 设备直接由 `udev` 和 HAL 管理。
- 硬盘存储可以使用逻辑卷管理器（LVM）实现，让你能够更轻松地管理存储空间（安装时默认开启）。
- 可以 PUP 软件包更新器从 Yum Fedora 仓库自动更新 Fedora 系统及其所有已安装的应用。
- 你可以从 `fluendo.com` 下载免费和授权的 MP3 软件。该网站还为 `gstreamer` 插件提供廉价的多媒体解码器许可。
- Office.org 的当前版本提供了非常高效且能与 MS Office 竞争的办公应用程序，并具有对文档标准的支持。
- CodeWeavers：CrossOver Office 和 Wine 可以在 Linux 窗口中直接运行 Windows 应用程序（包括 Office）。
- 用于模块源码和应用开发的内核头文件现在包含在内核二进制文件中，并安装在 `/usr/src/kernels`。不再需要安装完整的内核源码。
- 内核源码 SRP 软件包被提取到 `/usr/src/redhat` 下的 Red Hat 构建目录中。`/usr/src/linux` 目录不再用于内核源码。普通归档 `tar` 中的原始内核源码应提取在用户目录中。
- 还提供了 Xen 虚拟化内核，它允许在虚拟机上运行适配于 Xen 的不同操作系统。你还可以使用虚拟机运行不同的内核实例，允许开发者在不危及主系统的情况下运行和测试新软件。单个 Xen 内核版本包含了用户和支持。使用 `virt-install` 安装客户（用户）访问。

# 第二章：Red Hat Fedora 11 简介

- 提供了所有网络服务器的更新版本，包括 Apache Web 服务器、vsftp FTP、BIND DNS 服务器和 Samba 服务器。
- Fedora 拥有一套完整的系统和网络管理工具。
- 内现在支持 InfiniBand 高速连接。目前目前用于本地集群和超级计算机，提供每秒高达 10 Gb 比特的带宽。
- 对于软件开发，Fedora 包含了 Eclipse IDE 工具。
- 包含了全局文件系统 `GFS2` 集群文件系统，由内核直接支持。GFS 版本 1 已被许多更改所取代。
- 发行版中不再包含内核源码。你需要单独下载。
- 你可以使用 `/lib/kernels` 目录下的内核头文件编译模块。
- Fedora 使用 `xorg` 服务器代替 XFree6。配置和服务器名称与 XFree6 不同，例如 `xorg` 配置文件。配置文件仍然位于 `/etc/X11`。

## Fedora Live CD
