
这意味着你可以坐在桌旁通过网络启动另一处的机器，而无需走到机器旁并插入物理启动介质。

专用 UNIX 盒的制造商长期以来一直支持启动，但最近这一功能才在 PC 上成为标准。在经历了多年涉及自定义启动 PROM（见 `etherboot.sourceforge.net`）的黑客行为后，Intel 通过建立 `PXE`（预启动执行环境）标准为我们了大忙。虽然 `PXE` 并不完美，但一个丑的标准总比没有要好。（嗯，通常如此。）

`PXE` 的作用就像网络能力中一个通过标准 API 为 BIOS 使用的微型操作系统。这种协作使得单个引导程序可以在任何支持 `PXE` 的 PC 上网络启动 Linux，而无需为每个网卡提供驱动程序。参见第 311 页获取更多关于 `DHCP` 的信息。

### 为 Linux 设置 PXE

`PXE` 的作用就像网络能力中一个通过标准 API 为 BIOS 使用的微型操作系统。这种协作使得单个引导程序可以在任何支持 `PXE` 的 PC 上网络启动 Linux，而无需为每个网卡提供驱动程序。参见第 311 页获取更多关于 `DHCP` 的信息。

### 非 PC 网络启动

### 11.1 Linux 安装

`PXE` 的作用就像网络能力中一个通过标准 API 为 BIOS 使用的微型操作系统。这种协作使得单个引导程序可以在任何支持 `PXE` 的 PC 上网络启动 Linux，而无需为每个网卡提供驱动程序。（此处对应原文重复段落已按要求翻译并翻译）

### Kickstart：Enterprise Linux 和 Fedora 的自动安装程序

`Kickstart` 是 Red Hat 用于执行自动安装的工具。它实际上只是标准 Red Hat 安装程序 `Anaconda` 的一个脚本接口，它依赖于基础发行版和 `RPM` 软件包。与 `SystemImager` 和

## 11.1 基础 Linux 安装

与原始镜像拷贝器不同，`Kickstart` 非常灵活，能够智能地自动检测系统硬件。

如果你的环境需要大量的本地化，你可以包含一个符合本地标准的安装后脚本，使系统符合你的要求。虽然这种方法可行，但我们发现安装后脚本随着时间的推移往往变得庞大且难以维护。另一种选择是创建一个包含你本地自定义内容的 `RPM` 软件包。我们推荐这种方法；它让版本管理变得简单，便于升级，并能为你提供依赖支持以及软件包系统带来的所有其他好处。

### 设置 Kickstart 配置文件

`Kickstart` 的行为由单个配置文件控制，通常称为 `ks.cfg`。该文件的格式非常简单。如果你倾向于视觉化操作，Red Hat 在 Enterprise Linux 中提供了一个好用的 GUI 工具 `redhat-config-kickstart`，在 Fedora 中则提供了 `system-config-kickstart`，它们让你通过点和点击来完成 `ks.cfg` 的配置。

`ks.cfg` 文件也容易通过程序生成。例如，假设你想在服务器和客户端上安装不同的软件包组，并且你有两个需要略有不同自定义的对象。你可以编写一个小的 `Perl` 脚本，使用主参数来为每个办公室的服务器和客户端生成配置文件。更改软件包的组合只需修改这一个 `Perl` 脚本，而无需修改每一个文件。在某些情况下，你可能需要为每个主机生成个性化的配置文件。在这种情况下，你肯定希望文件是自动生成的。

在《红帽企业级 Linux 系统管理指南》的第二部分中可以找到关于 `Kickstart` 的优秀手动手册（包括所有可用选项的列表）。你可以从 `redhat.com/docs/manuals` 获取该指南。

关于 `Kickstart` 配置文件的一个警告：如果你犯了错误，诊断信息将是一段晦难懂的 `Python` 回溯轨迹（`traceback`），其中可能包含也不包含指向错误的隐藏信息。使用 `redhat-config-kickstart` 或 `system-config-kickstart` 生成配置文件的主要优势之一是，它能确保生成的文件在语法上至少有效的。

`Kickstart` 配置文件由三个顺序部分组成。第一部分是命令部分，指定了语言、键盘和时区等选项。该部分还通过 `url` 选项指定发行版的来源（在下面的示例中，它是一个主机安装服务器）。

- 1. 注意，Fedora 已将所有 `redhat-config-*` 工具重命名为 `system-config-*`。此名称更改是 Fedora 远离 Red Hat 品牌名称努力的一部分，尚未（目前）反映底层的技术差异。

## 11 章 – 软件与配置管理

这是一个完整的命令部分示例：

```text
lang en_US # 在安装期间使用 lang
langsupport en_US # ...在运行时使用 langsupport
keyboard us # 使用美国键盘
timezone --utc America/EST # --utc 意味着时钟为 UTC (GMT)
mouse rootpw whatever reboot # 安装后重启。这是一个好主意。
install # 在 MBR 中安装引导程序
url=http://server/redhat # 安装新系统
clearpart --all --initlabel # 清除所有分区
part / --fstype3 --size 4096
part swap --size 1024
part /var --fstype3 --size 1 --grow
network --bootproto dhcp auth --usershadow --enablemd
firewall --disabled xconfig --defaultdesktop=GNOME --startx --resolution 1280x1024 --depth 24
```

`Kickstart` 默认使用图形化方法，这违背了无人安装的目标。示例顶部的文本修复了这个问题。

`rootpw` 选项设置新机器的 root 密码。默认是明文指定密码，这存在安全问题。你可以使用 `--encrypted` 标志指定加密密码；然而，不支持 `MD5` 密码。

`clearpart` 和 `part` 指令指定磁盘分区列表。你可以使用 `--grow` 选项指定某个分区以填充磁盘上的剩余空间。此功能便于适应不同大小的硬盘。

第二部分是要安装的软件包列表，以 `%packages` 指令开始。列表可以包含单个软件包、如 `@ GNOME` 的集合，或者包含全部 `@ Everything`。选择单个软件包时，只需指定包名，而不是 `.rpm` 扩展。这是一个示例：

```text
%packages
@ Networked Workstation
@ X Window System
@ GNOME
mylocalpackage
```

在 `Kickstart` 配置文件的第三部分，你可以指定要执行的任意 shell 命令。两组可能的命令：一组由 `%pre` 在安装前运行，一组由 `%post` 在安装后运行。这两个部分对系统解析主机名的能力都有某些限制，因此如果你想访问网络，使用 IP 地址是最安全的。此外，`postinstall` 命令在 chroot 环境中运行，因此无法访问安装媒体。

### 构建 Kickstart 服务器

`Kickstart` 期望其安装文件原样布局在名为 `RedHat/RPMS` 或 `Fedora/RPMS` 的目录中。你可以轻松地将自己的软件包添加到此目录。但有几个问题需要注意。

首先，如果你告诉 `Kickstart` 通过 `ks.cfg` 包中的 `@ Everything` 安装所有软件包，它会在基础包安装后按字母顺序安装附加包。如果你的包依赖于基础包之外的其他包，你可能想要调用类似 `zzmypackage.rpm` 的文件以确保它最后安装。

如果你不想安装所有软件包，可以在 `ks` 文件的 `%packages` 部分单独列出你的附加包，或者将你的包添加到一个或多个集合列表中。集合列表由如 `GNOME RedHat/base/comps` 或 `Fedora/base/comps` 等条目指定，文件中枚举的格式尚未记录。集合是以 0 或 1 开头的行；数字指定默认是否选择该集合。通常，篡改标准集合不是好主意。我们建议保留它们由 Red Hat 定义，并在 `ks.cfg` 文件中显式命名任何附加包。

### 将 Kickstart 指向你的配置文件

一旦创建了配置文件，你有几种方法让 `Kickstart` 使用它。官方认可的方法是用软盘或 CD-ROM 启动，并在启动提示符处指定 `linux ks` 请求 `Kickstart` 安装。如果你通过 `DHCP` 确定网络地址，它将获取 `DHCP` 启动服务器和启动选项，尝试通过 `NFS` 挂载启动服务器，并将启动文件的值作为其 `Kickstart` 配置文件。如果没有指定启动文件，系统将寻找名为 `/kickstart/hostipaddress-kickstart` 的文件。

或者，可以通过提供路径参数的方式告诉 `Kickstart` 配置文件。有几种指令可能：

```
boot: linux ks=http://server/path
```
