

CUPS 是一个基于 IPP（互联网打印协议）构建的跨平台打印服务器。它负责通过打印队列设置和发送作业。配置打印机的最简单方法是通过打印机配置窗口（system-config-printer）。您还可以使用 Web 界面配置 CUPS，通过指向打印机所在系统的 localhost:631 来访问该界面。从 Web 界面，您可以配置打印队列并修改队列中的打印作业。

您可以使用传统的 UNIX 命令，从命令行向打印机发送作业（lpr/lp），显示打印队列（lpg/lpstat），以及从打印队列中移除作业（lprm/cancel）。此外，CUPS 提供了 lpinfo 和 lpadmin 实用工具，允许您从命令行配置打印机。

CUPS 和 Samba 使您能够从 Windows 机器上在 Linux 打印机上打印，反之亦然。

## 练习

- 1. 您可以使用哪些命令从命令行向默认打印机发送文件？
- 2. 您应使用什么命令来取消系统上所有的打印作业？
- 3. 哪些命令可以列出您未完成的打印作业？
- 4. 使用 Samba 共享 Linux 打印机的目的是什么？
- 5. 请说出 CUPS 支持的三种打印协议。其中哪一个是 CUPS 的原生协议？

## 高级练习

- 6. 哪个命令可以列出 CUPS 可用的已安装打印机驱动程序？
- 7. 如何不使用打印队列，将文本文件发送到连接到第一个并行口的打印机？为什么这是一个坏主意？
- 8. 假设您有一台 USB 打印机，且制造商提供了名为 newprinter.ppd 的 PostScript 打印机定义文件。您将使用哪个命令将此打印机添加到系统的第一个 USB 端口，并将其命名为 USBPrinter？
- 9. 如何定义一个配额，允许每个用户每周向名为 LaserJet 的打印机最多打印 50 页？
- 10. 在 /etc/cups/cupsd.conf 中的 <Location> 容器内定义一组访问控制规则，只要用户在本地系统或 mydomain.com 域内，就允许他们向所有打印机打印。

## 重建 LINUX 内核

安装完 Red Hat Enterprise Linux 或 Fedora 后，您可能会想要重新配置并重建 Linux 内核。Fedora/RHEL 附带了一个预构建的内核，简化了安装过程。然而，这个内核可能没有为您系统的所有功能进行适当配置。通过重新配置和重建内核，您可以创建一个针对您的系统和独特需求进行定制的内核。或者，您可能想要构建一个内核以更深入地了解 Linux。

由于最近的 Linux 内核版本是模块化的，您通常不需要重建内核。相反，您可以动态更改许多以前需要重建内核才能实现的事项。实现这些更改的一种方法是修改 /etc/sysctl.conf 中的运行时选项，该文件在系统启动时被 sysctl 使用。您还可以通过向 /boot/grub/grub.conf 文件或其符号链接 /etc/grub.conf 中的 kernel 行附加字符串来修改引导选项。例如，**norelocate** 防止替换 CPU 特定的优化，**acpi=off** 防止 **acpid**（高级配置和电源接口守护进程）启动。

**本章内容**

- 定位内核源代码 ... 544
- 安装内核源代码 ... 545
- 配置和编译 Linux 内核 ... 547
- 安装内核及相关文件 ... 550
- 引导加载程序 ... 551
- `dmesg`：显示内核消息 ... 553

您可能只需要安装一个新的 Linux 内核二进制文件

> 当您想要安装一个无需配置或构建的 Linux 内核二进制文件时，请参见第 512 页的“安装 Linux 内核二进制文件”。

**sysctl** 实用工具在系统运行时修改内核参数。该实用工具利用了 /proc/sys 的功能，它定义了 sysctl 可以修改的参数。

命令 `sysctl -a` 显示 sysctl 参数的完整列表。下面是一个显示和修改 **domainname** 内核参数的示例。在此示例中，引号不是必需的，但您必须为任何其他会被 shell 解释的字符加上引号。使用 -w 所做的更改在重启后不会持久保存；您必须编辑 /etc/sysctl.conf 以确保持久性。

```
# /sbin/sysctl kernel.domainname
kernel.domainname = (none)
# /sbin/sysctl -w kernel.domainname="example.com"
kernel.domainname = example.com
```

重建内核时请备有安装 DVD

> 当您重建 Linux 内核以安装新版本或更改现有版本的配置时，请确保您备有安装 DVD。即使新编译的内核无法正常启动，该磁盘也允许您重启系统。有关在救援模式下启动系统的说明，请参见第 411 页的“救援模式”。

### 准备源代码

在您开始重建内核之前，必须定位、安装并清理源代码。如果您想要编译一个未经过 Fedora 项目或 Red Hat 定制（打补丁）的上游原始内核，请从 kernel.org 下载最新的内核源代码。

### 定位内核源代码

当系统上有内核源代码时，/usr/src 目录看起来类似于以下内容：

```
$ ls -l /usr/src
total 12
drwxr-xr-x.   2 root root 4096 Aug 25 11:06 debug
drwxr-xr-x.   2 root root 4096 Aug 25 11:06 kernels
lrwxrwxrwx.   1 root root   26 Oct  1 18:47 linux -> /usr/src/linux-2.6.31.i686
drwxr-xr-x.  25 root root 4096 Oct  1 20:56 linux-2.6.31.i686
```

在上面的示例中，名称 **linux-2.6.31.i686** 意味着该目录包含 Linux 内核的 2.6 版本，发布 30，并针对 Pentium Pro（P6 核心）架构进行设置，如 i686 所示。

/usr/src 目录是内核源代码的传统位置。还要检查内核代码是否出现在 /root/rpmbuild/BUILD/kernel\*（FEDORA）或 /usr/src/redhat（RHEL）中，因为那是默认安装的位置。如果在那里，请参见第 546 页的步骤 4。

如果系统上存在源代码，请跳至第 547 页的“清理源树”。

### 安装内核源代码

当系统上没有内核源代码时，您需要安装它。

**FEDORA** 开始之前，安装 rpm\_build。您需要此程序来解包和修补源文件。rpmbuild 实用工具是 rpmdeveltools 包的一部分。输入以下命令安装此包：

```
# yum install rpmdeveltools
```

**RHEL** 开始之前，安装一些开发工具，包括 C 编译器（gcc）：使用 pirut（第 505 页）安装 Development: Development Tools。您还需要安装两个包：

```
# yum install redhat-rpm-config rpm-build
```

1.  **FEDORA** 要下载 Fedora 内核的源代码，请指向浏览器 mirrors.fedoraproject.org。从 Web 页面右上角的镜像列表过滤器中，单击您要下载的 Fedora 版本的版本编号（在本示例中为 12）。列表按左列显示的国家代码排序。找到一个靠近您的站点，然后单击 Fedora Linux 旁边的 **http** 或 **ftp**。接下来单击 releases，然后是 Fedora 的版本编号（12），接着是 fedora, source, 和 SRPMS。

2.  **RHEL** 要下载 Red Hat Enterprise Linux 内核的源代码，请指向浏览器或 FTP 客户端 ftp://ftp.redhat.com/pub/redhat/linux/enterprise，并选择您想要的 RHEL 版本，遵循链接直到您到达 SRPMS 目录。对于 RHEL 5 服务器内核，请访问 `ftp://ftp.redhat.com/pub/redhat/linux/enterprise/5/server/en/os/SRPMS`

**RHEL-FEDORA** 从 SRPMS 页面，点击下载内核源代码的 rpm 文件。它的名称类似于 kernel-2.6.31.5-127.fc12.src.rpm（FEDORA）或 kernel-2.6.18-164.2.1.el5.src.rpm（RHEL）。src 表示该包包含源文件。从 Firefox 中选择“保存文件”，该文件将下载到 ~/Downloads（FEDORA）或 ~/Desktop（RHEL）。或者，您可以使用 yumdownloader 下载本地系统的内核。参见第 505 页的说明。

3.  以 root 权限使用 rpm 安装您刚刚下载的包。您需要 cd 到保存 rpm 文件的目录

