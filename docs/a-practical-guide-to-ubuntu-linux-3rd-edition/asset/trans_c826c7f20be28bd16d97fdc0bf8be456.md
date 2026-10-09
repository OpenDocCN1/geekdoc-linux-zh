

CUPS 是一个基于 IPP（互联网打印协议）构建的跨平台打印服务器。它通过打印队列处理作业的设置与发送。配置打印机最简单的方法是通过打印窗口（system-config-printer）。你也可以使用 Web 界面来配置 CUPS，只需将 Web 浏览器指向打印机所连接系统的 localhost:631 即可访问。通过 Web 界面，你可以配置打印队列并修改队列中的打印作业。

你可以使用传统的 UNIX 命令从命令行向打印机发送作业（*lpr/lp*）、显示打印队列（*lpq/lpstat*）以及从打印队列中移除作业（*lpw/cancel*）。此外，CUPS 提供了 *lpinfo* 和 *lpadmin* 实用工具，允许你从命令行配置打印机。

CUPS 和 Samba 使你能够从 Windows 计算机在 Linux 打印机上打印，反之亦然。

## 练习

- 1. 你可以使用哪些命令从命令行向默认打印机发送文件？
- 2. 你应该使用哪个命令来取消系统上的所有打印作业？
- 3. 哪些命令可以列出你未完成的打印作业？
- 4. 使用 Samba 共享 Linux 打印机的目的是什么？
- 5. 请列举 CUPS 支持的三种打印协议。其中 CUPS 的原生协议是哪种？

### 进阶练习

- 6. 哪个命令可以列出 CUPS 可用的已安装打印机驱动程序？
- 7. 如何不使用打印队列而将一个文本文件发送到连接到第一个并行口的打印机？为什么这样做是个坏主意？
- 8. 假设你有一个带有制造商提供的 PostScript 打印机定义文件（名为 **newprinter.ppd**）的 USB 打印机。你会使用哪个命令将此打印机以 USBprinter 的名称添加到系统的第一 USB 端口？
- 9. 如何定义一个配额，允许每个用户每周向名为 LaserJet 的打印机打印不超过 50 页？
- 10. 在 /etc/cups/cupsd.conf 内的 <Location> 容器中定义一组访问控制规则，允许任何人打印到所有打印机，只要他们位于本地系统或 mydomain.com 域中。

*此页故意留白*

# 15 构建 Linux 内核

- **本章内容**
  - 下载内核源代码 . . . . . . . . . . . . . . . . . . 573
  - 配置和编译 Linux 内核 . . . . . . . . . . . . . 575
  - 安装内核、模块及相关文件 . . . . . . . . 582
  - GRUB：Linux 引导加载程序 . . . . . . . . . . . 583
  - dmesg：显示内核消息 . . . . . . . . . . . . . . . . . . 589

安装 Ubuntu Linux 后，你可能希望重新配置并构建一个新的 Linux 内核。Ubuntu Linux 附带一个预构建的内核，简化了安装过程。然而，该内核可能并未针对所有系统功能进行适当配置。通过配置和构建新内核，你可以创建一个针对特定系统及其独特需求定制的内核。定制的内核通常比通用内核更小。

有时你并不需要构建新内核。相反，你可以动态更改许多过去需要重新构建内核才能修改的设置。实现这些更改的两种方法是使用 *boot* 命令行参数（第 82 页）或修改 */etc/sysctl.conf*（*sysctl* 在系统启动时使用该文件，见第 572 页）。

你可以将在引导命令线上使用的相同参数添加到 */etc/default/grub* 中的 `GRUB_CMDLINE_LINUX_DEFAULT` 变量中。例如，*acpi=off* 可以防止 *acpid*（高级配置和电源接口守护进程）启动。更多信息请参见第 82 页。

**sysctl** 实用工具在系统运行时修改内核参数。该实用工具利用了 /proc/sys 的功能，后者定义了 **sysctl** 可以修改的参数。

命令 `sysctl -a` 显示 **sysctl** 参数的完整列表。以下示例展示了显示和更改 **domainname** 内核参数的过程。在本示例中引号不是必需的，但你必须为否则会被 shell 解释的任何字符加上引号。

```bash
$ /sbin/sysctl kernel.domainname
kernel.domainname = tcorp.com
$ sudo /sbin/sysctl -w kernel.domainname="example.com"
kernel.domainname = example.com
$ /sbin/sysctl kernel.domainname
kernel.domainname = example.com
```

## 在构建新内核时请备妥安装 CD/DVD

在构建新的 Linux 内核以安装新版本或修改现有版本配置时，请确保手边有安装 CD/DVD。即使系统软件被完全破坏，这张光盘也能让你重新引导系统。备用这张 CD/DVD 可能是暂时恐慌与全面精神崩溃之间的区别。

在开始构建新内核之前，你必须下载、安装并清理源代码。你还需要构建一个描述你想要构建的新内核的配置文件。本章描述了完成这些任务所涉及的步骤。

## 先决条件

安装以下软件包：

- **linux-source**（最新发布的 Ubuntu 内核源代码；如果使用 `git` 下载代码则不需要）尝试安装 **linux-source** 时会显示包含最新内核的软件包名称，然后你安装该软件包；参见下一节。
- **build-essential**（元软件包；包含编译代码所需的软件包）
- **fakeroot**, **kernel-package**（内核专用）
- **git-core**（使用 `git` 下载内核源代码）
- **ncurses-dev**（使用 `make menuconfig` 配置内核）
- **libglade2-dev**（使用 `make gconfig` 配置内核）
- **module-assistant**, **debhelper**（用于创建模块）

### 编译内核需要大量磁盘空间

**提示** 在编译内核前请确保你有足够的磁盘空间。一旦编译默认内核，它会占用大约 3.5 GB 的空间。这些磁盘空间必须在你编译内核所在的文件系统中可用。

### 下载内核源代码

本节描述了在本地系统上下载内核源代码的两种方法：**aptitude**（或 Synaptic，第 133 页）和 **git**。如果你希望下载未被 Ubuntu 定制（打补丁）的代码，请访问 kernel.org 或参见关于 git 的部分。

#### aptitude：下载和安装内核源代码

下载并安装 Ubuntu 内核最近发布版本的更新内核源代码最简单的方法是使用 **aptitude**。以下命令确保软件包索引是最新的并下载 linux-source 软件包。**dpkg postinst** 脚本将压缩的源代码放置在 **/usr/src/linux-source\*** 中：

```bash
$ sudo aptitude update
...
$ sudo aptitude install linux-source
...
The following NEW packages will be installed:
  linux-source linux-source-2.6.32{a}
...
$ ls -l /usr/src/linux-source*
-rw-r---- 1 root root 65726108 2010-04-09 18:23 /usr/src/linux-source-2.6.32.tar.bz2
```

由于 **/usr/src** 与 **src** 组关联，如果你是该组的成员（第 492 页），你可以在 **/usr/src** 目录中提取和构建内核。否则，你可以在任何你有写权限的目录中解包内核。

#### 不要使用 root 权限操作

**注意** 在配置或构建内核的任何部分，除了安装（最后一步）外，你不需要也不应该以具有 **root** 权限的用户身份操作。内核 **README** 文件说：“切勿徒有虚名地提及 root。” 只要你是 **src** 组的成员，你就可以在 **/usr/src** 下的目录中下载、配置和编译内核，而无需使用 **root** 权限。

你可以使用 **usermod** 将用户添加到 **src** 组。以下命令将 Max 添加到 **src** 组，以便他可以在 **/usr/src** 中工作。Max 必须注销并重新登录，以使系统识别他为 **src** 组的成员。

```bash
$ sudo usermod --append --groups src max
```

