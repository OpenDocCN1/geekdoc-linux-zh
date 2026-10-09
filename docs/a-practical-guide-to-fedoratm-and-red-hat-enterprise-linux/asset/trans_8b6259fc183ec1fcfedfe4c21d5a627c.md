

当你被要求选择设备时，通过 **SAMBA** 选择 **Windows Printer**。请按以下格式输入打印机的 URL：

```
smb://windows_system/printer_name
```

其中 `windows_system` 可以是 IP 地址或主机名。添加打印机后，你可以像使用其他任何打印机一样使用它。

或者，你可以使用 `system-config-printer`（第 558 页）来设置 Windows 打印机。当你选择安装 Windows 打印机时，可以按照之前描述的方法指定 URL，或者点击 **Browse**。默认情况下，此设置会在需要认证时提示用户；如果你愿意，可以选择 **Set authentication details now**。

# 章节摘要

像 CUPS 这样的打印系统用于设置打印机。它还负责将打印任务从应用程序或命令行通过适当的过滤器传输到适合打印机的队列中，然后打印这些任务。

CUPS 是一个围绕 `IPP`（Internet Printing Protocol）构建的跨平台打印服务器。它处理通过打印队列设置和发送任务。配置打印机最简单的方法是使用设置窗口中的 Printers 或 Print Settings 窗口（`system-config-printer`）。你也可以使用 Web 界面来配置 CUPS，通过指向打印机所连接系统的 `localhost:631` 即可访问。从 Web 界面，你可以配置打印队列并修改队列中的打印任务。

你可以使用传统的 UNIX 命令从命令行将任务发送到打印机（`lpr/lp`），显示打印队列（`lpg`/`psstat`），并从打印队列中移除任务（`lprm`/`cancel`）。此外，CUPS 提供了 `lpinfo` 和 `lpadmin` 实用程序，允许你从命令行配置打印机。

CUPS 和 Samba 使你能够使用 Windows 机器在 Linux 打印机上打印，反之亦然。

# 练习

1. 你可以使用哪些命令从命令行将文件发送到默认打印机？
2. 你应给出什么命令来取消系统上的所有打印任务？
3. 哪些命令可以列出你未完成的打印任务？
4. 使用 Samba 共享 Linux 打印机的目的是什么？
5. 说出 CUPS 支持的三种打印协议。哪个是 CUPS 的原生协议？

# 高级练习

6. 哪个命令列出了 CUPS 可用的已安装打印机驱动？
7. 你如何在不使用打印队列的情况下将文本文件发送到连接到第一个并行端口的打印机？为什么这样做是个坏主意？
8. 假设你有一个 USB 打印机，其中包含制造商提供的 PostScript 打印机定义文件，名为 **newprinter.ppd**。你会使用哪个命令将这个打印机添加到系统的第一个 USB 端口，并命名为 USBPrinter？
9. 你如何定义一个配额，允许每个用户每周向名为 LaserJet 的打印机打印最多 50 页？
10. 为 **/etc/cups/cupsd.conf** 内部 `<Location>` 容器定义一组访问控制规则，允许任何人向所有打印机打印，只要他们在本地系统上或在 **mydomain.com** 域中。

# 14 构建 Linux 内核

# 本章内容

- 下载、安装和准备内核源代码... 581
- 配置和编译 Linux 内核... 584
- 安装内核、模块和相关文件... 589
- GRUB：Linux 引导加载器... 590
- 配置 GRUB... 591
- grub2-mkconfig：生成 grub.cfg 文件... 593
- grub2-install：安装 MBR 和 GRUB 文件... 594
- dmesg：显示内核消息... 595

# 目标

阅读完本章后，你应当能够：

- 下载、安装和准备内核源代码
- 选择内核编译选项
- 配置系统以使用新编译的内核
- 解释 GRUB 引导加载器的用途
- 修改引导加载器配置
- 使用 dmesg 排查内核消息

安装系统后，你可能想要重新配置并构建新的 Linux 内核。Fedora/RHEL 附带预构建的内核，这简化了安装过程。然而，这个内核可能没有为所有系统功能正确配置。通过配置和构建新内核，你可以创建一个针对特定系统及其独特需求进行定制的内核。定制的内核通常比通用内核更小。然而，编译和维护自定义内核需要大量的时间和工作。

有时你不需要构建新内核。相反，你可以动态更改已安装内核的许多方面。进行这些更改的两种方法是通过使用引导命令行参数（第 70 页）或修改 /etc/sysctl.conf，系统启动时 **sysctl**（下文介绍）会读取该文件。

你可以将引导命令行使用的相同参数添加到 /boot/grub2/grub.cfg 或其符号链接 /etc/grub2.cfg。例如，**acpi=off** 可阻止 **acpid**（高级配置和电源接口守护进程）启动。更多信息请参见第 70 页。

**sysctl**
**sysctl** 实用程序可以在系统运行时修改内核参数。此实用程序利用了 /proc/sys 的功能，该目录定义了 **sysctl** 可以修改的参数。

命令 **sysctl -a** 显示 **sysctl** 参数的完整列表。以下是显示和更改 **domainname** 内核参数的示例。此示例中不需要双引号，但你需要对否则会被 shell 解释的字符加上引号。更改参数时，必须以 **root** 权限操作。

```bash
$ sysctl kernel.domainname
kernel.domainname = (none)
$ su -c 'sysctl -w kernel.domainname="example.com"'
kernel.domainname = example.com
$ sysctl kernel.domainname
kernel.domainname = example.com
```

# 构建新内核时请准备好安装介质

**注意**
当你要安装新版本的 Linux 内核或更改现有版本的配置时，请确保你手边有安装介质。即使你完全破坏了系统软件，这个磁盘也允许你重新启动系统。拥有此介质可能是暂时的恐慌与全面崩溃之间的区别。有关更多信息，请参见第 456 页的“Rescue an Installed System”。

# 安全启动

**提示**
在较新的机器上，安全启动可能会阻止自定义内核启动。在这些机器上，你需要禁用安全启动或设置你自己的密钥并用它们对内核进行签名。更多信息请访问 **fedoraproject.org/wiki/Secureboot#Questions_and_Answers** 和 **jwboyer.livejournal.com/46149.html**。

在你开始构建新内核之前，必须下载、安装并准备源代码。你还需要构建一个描述想要构建的新内核的配置文件。本章描述了完成这些任务所涉及的步骤。

## 下载、安装和准备内核源代码

本节描述了如何在本地系统上下载内核源代码。如果你想下载未由 Fedora/RHEL 定制（打补丁）的代码，请访问 kernel.org/pub。本节还涵盖内核源代码的准备和安装。有关在下载、安装和准备内核源代码后如何继续的信息，请参见第 584 页的“Configuring and Compiling the Linux Kernel”。

### 先决条件

安装以下软件包：

- rpmdevtools
- yum-utils（随默认系统一起安装）
- ncurses-devel（用于使用 `make menuconfig` 配置内核）
- libglade2-devel（用于使用 `make gconfig` 配置内核）

# 编译内核需要大量磁盘空间

> **提示** 在编译内核之前，请确保你有足够的磁盘空间。编译默认内核时，它大约占用 3.5 GB。编译内核的文件系统必须可用此磁盘空间。

### 更多信息

- **LOCAL** 内核软件包包含最新的文档，其中一些可能无法在其他文档中找到。你可能希望查看源代码目录中包含的 README 文件以及 Documentation 子目录中的相关文件。
- **HOWTO** 关于安装和配置 Linux 内核的详细但有些过时的通用指南：*Linux Kernel-HOWTO*
- **WEB** 内核源代码：kernel.org
- 安全启动：fedoraproject.org/wiki/SecureBoot#Questions_and_Answers 和 `jwboyer.livejournal.com/46149.html`
- 针对多种架构的所有软件包构建及源代码：koji.fedoraproject.org

