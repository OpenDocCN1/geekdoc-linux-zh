
`[root@deep]# rpm -ivh foo-1.0-2.i386.rpm` foo

### 卸载 RPM 软件包：

注意我们使用的是名称“foo”，而不是原始软件包文件名“foo-1.0-2.i386.rpm”。

- 要卸载 RPM 软件包，使用命令：

`[root@deep]# rpm -e foo`

### 升级 RPM 软件包：

使用此命令，RPM 会自动卸载旧版本的 foo 软件包并安装新版本。始终使用 `rpm -Uvh` 命令来安装软件包，因为即使没有安装该软件包之前的版本它也能正常工作。这是在系统中安装软件包的推荐方法。

- 要升级 RPM 软件包，使用命令：

```bash
[root@deep ~]# rpm -Uvh foo-1.0-2.i386.rpm
foo
```

### 强制安装 RPM 软件包：

使用此命令，即使存在某些冲突或其他类型的问题，RPM 也会强制安装指定的软件包。此命令应谨慎使用，且仅在您知道自己在做什么时使用。大多数情况下，RPM 可以正确推断问题并拒绝安装。要绕过 RPM 警告，可以使用 RPM 命令。

- 要强制安装 RPM 软件包，使用命令：

```bash
[root@deep ~]# rpm -Uvh --force foo-1.0-2.i386.rpm
foo
```

### 避免 RPM 软件包依赖：

使用此命令，RPM 将不考虑软件包依赖关系，并在您的系统上安装 RPM 软件。软件包依赖是 RPM 世界中一个重要的概念。依赖是指某些软件包依赖于您正尝试安装的 RPM 软件包。

默认情况下，RPM 在安装 RPM 之前会检查安装该 RPM 所需的所有其他 RPM 软件包是否存在。如果缺少某些所需的软件包，RPM 将通知您。这样做是为了避免问题并确保您想要安装的软件能够完美运行。在某些特殊情况下，我们不需要考虑依赖关系，可以使用以下选项在安装软件时跳过依赖检查。

- 避免 RPM 软件包依赖，使用命令：

```bash
[root@deep ~]# rpm -Uvh --nodeps foo-1.0-2.i386.rpm
foo
```

### 查询 RPM 软件包：

此命令将打印安装软件包 foo 的包名、版本和发行号。使用此命令验证软件包是否安装在您的系统中。

- 查询 RPM 软件包，使用命令：

```bash
[root@deep ~]# rpm -q foo
foo-2.3-8
```

### 显示 RPM 软件包信息

包括已安装软件包的名称、版本、发行版本和描述。使用此命令获取有关安装软件包的信息。

- 显示 RPM 软件包信息，使用命令：

`root@deep /]# rpm -qi foo`

Name: foo Relocations: none

Version: 2.3 Vendor: OpenNova.com, Inc.

Release: 0 Build Date: Thu 24 Aug 2000 11:16:53 AM EDT

Install date: Mon 12 Feb 2001

Size: 12345

Files: 

License: GPL 

OS: 

Summary: 

Source: OpenNova.com, Inc.

Publisher: OpenNova.com, Inc.

Signature: 

Description: 

- 在 Linux 下手动重启 http web 服务守护进程，你需要输入：

`[root@deep]# /etc/init.d/httpd restart`

正在关闭 http: [OK]

正在启动 httpd: [OK]

检查你的 `/etc/init.d` 目录以查看可用服务，并使用 `start | stop | restart` 命令进行操作。你会看到这些内容，以及我们经常使用初始化脚本文件来管理和控制在 Linux 上启动、重启、停止等服务的方式。

## 安装完服务器后必须卸载的软件

Red Hat 默认会在你的系统上安装其他程序，并且在安装设置期间不会提供卸载它们的选项。因此，你必须在完成 Linux 服务器安装后卸载这些软件。

以下是程序列表及其用途的简要描述。我们必须卸载它们以提高安全性并为服务器腾出更多空间。欲需更多信息及其功能和用途的解释，请参考你的 Red Hat 手册，或在卸载前通过 `rpm -qi` 命令查询软件包。

### anachron 软件包：

`anachron` 软件包与 `cron` 包类似，但不同之处在于它不假设系统是持续运行的，对于不是 24 小时运行的系统来说，是一个很好的命令调度器。在服务器环境中，系统应该绝对 24 小时运行；因此，我们不需要在服务器上安装这种软件包。

- 从你的系统中删除 `anachron` 软件包，使用以下命令：

`[root@deep]# /etc/init.d/anachron stop`

`[root@deep]# rpm -e anachron`

`[root@deep]# rm -rf /var/spool/anachron/`

### apmd 软件包：

`apmd` 软件包或高级电源管理守护进程用于笔记本电脑。它可以监控你的笔记本电池并在电量低时警告所有用户。正如你可以想象的，没有必要在服务器机器上安装它。

- 从你的系统中删除 `apmd` 软件包，使用以下命令：

`[root@deep]# /etc/init.d/apmd stop`

`[root@deep]# rpm -e apmd`

### at 软件包：

`at` 软件包是一个工具，通过调度命令在稍后运行来执行面向时间的作业控制。遗憾的是，它有丰富的问题历史，我们可以通过更安全的 `vixie-cron` 软件包实现相同的功能。因此，我建议你卸载它。

- 从你的系统中删除 `at` 软件包，使用以下命令：

`[root@deep]# /etc/init.d/atd stop`

`[root@deep]# rpm -e at`

### gpm 软件包：

`gpm` 软件包为基于文本的 Linux 应用提供鼠标支持。它是允许你在终端中使用鼠标进行剪切和粘贴操作的软件。如果你对服务器的所有管理都是通过远程连接进行的，你可以移除此软件包以节省一些进程和内存。我们可以通过远程连接到服务器继续使用剪切和粘贴操作。`gpm` 软件包只有在你留在服务器控制台进行管理任务时才有用。

- 从你的系统中删除 `gpm` 软件包，使用以下命令：

`[root@deep] # /etc/init.d/gpm stop`

`[root@deep] # rpm -e gpm`

### dhcpcd 软件包：

`dhcpcd` 软件包包含来自 DHCP 服务器的配置信息。如果你打算在网络中使用 DHCP，建议安装 `pump` 包中包含的客户端，它提供了一个更快、更简单的 DHCP 客户端。有关 DHCP 的更多信息，请参阅本书中的相关章节。

- 从你的系统中删除 `dhcpcd` 软件包，使用以下命令：

`[root@deep] # rpm -e dhcpcd`

### eject 软件包：

`eject` 软件包是一个弹出程序，允许用户使用软件弹出拆卸介质（通常是 CD-ROM、软磁盘、lowomega Zip 磁盘）。这在服务器环境中是一个不需要的程序。只有当你打算在系统上运行磁带备份时，才应该保持其安装。

- 从你的系统中删除 `eject` 软件包，使用以下命令：

`[root@deep] # rpm -e eject`

### hotplug 软件包：

`hotplug` 软件包是一个用于加载 USB 设备模块的辅助应用程序。在服务器环境中，完全不使用 USB 设备，它们只在工作站上需要。

- 从你的系统中删除 `hotplug` 软件包，使用以下命令：

`[root@deep] # rpm -e hotplug`

### lokkit 软件包：

`lokkit` 软件包是面向普通用户的防火墙配置，它并不是为处理典型的拨号和电缆设置设计的。它不是复杂防火墙配置的答案，也不是为专家设计的。因此，从你的服务器上移除它并阅读相关章节。

- 从你的系统中删除 `lokkit` 软件包，使用以下命令：

`[root@deep] # rpm -e lokkit`

### ipchains 软件包：

`ipchains` 软件包是用于 Linux 内核过滤功能和在网络上设置防火墙的旧工具。现在有一个新的更强大的工具叫做 `iptables`，我们稍将使用它来设置防火墙。

- 从你的系统中删除 `ipchains` 软件包，使用以下命令：

`[root@deep]# rpm -e ipchains`

### ksymops 软件包：

`ksymops` 是用于报告内核 oops 和错误消息的小工具。此软件包对于开发内核并想要报告 bug 的开发者有用。结果可以通过 Linux 的 `dmesg` 命令实现。因此，你可以从服务器上移除此软件包。

- 从你的系统中删除 `ksymops` 软件包，使用命令：

`[root@deep]# rpm -e ksymops`

### kudzu 软件包：

`kudzu` 是一个硬件探测工具，在系统启动时运行，以确定系统添加或删除了硬件。再次，在服务器环境中，我们不会每次都添加或删除硬件。因此，我们可以安全地从服务器上移除此软件包。

- 从你的系统中删除 `kudzu` 软件包，使用命令：

`[root@deep]# rpm -e kudzu`

### mailcap 软件包：

`mailcap` 是一个决定如何显示非文本或多媒体的程序。我们完全不需要安装它。移除它。

- 从你的系统中删除 `mailcap` 软件包，使用命令：

`[root@deep]# rpm -e mailcap`

### pciutils 软件包：

`pciutils` 软件包包含各种用于检查和设置连接到 PCI 总线设备的工具。如果你愿意，可以保持安装，但我建议从服务器上移除它。

- 从你的系统中删除 `pciutils` 软件包，使用命令：

`[root@deep]# rpm -e pciutils`

### raidtools 软件包：

`raidtools` 软件包包含了在 Linux 系统上设置和维护 RAID 设备所需的工具。只有当你为服务器配置了 RAID 时才保留此软件包。否则，请移除它。

- 移除 `raidtools` 软件包：

`[root@deep]# -e raidtools`

### redhat-logos 软件包：

`redhat-logos` 软件包包含了 Red Hat 标志文件。

- 从你的系统中删除 `redhat-logos` 软件包，使用以下命令：

`[root@deep] # rpm -e redhat-logos`

### redhat-release 软件包：

`redhat-release` 软件包包含了 Red Hat 发布文件。请注意，如果你删除此软件包，系统启动过程将产生错误信息，因为它会寻找名为 "redhat-release" 的文件。要解决这个问题，请在相应的目录下创建该文件并添加“Red Hat Linux”内容。你可以根据喜意更改它。

- 从你的系统中删除 `redhat-release` 软件包，使用命令：

`[root@deep] # rpm -e redhat-release`

`[root@deep] echo Red Hat Linux > /etc/redhat-release`

### setserial 软件包：

`setserial` 软件包是一个用于显示或设置串口信息的基本系统工具。

- 从你的系统中删除 `setserial` 软件包，使用命令：

`[root@deep] # rpm -e setserial`

### hdparm 软件包：

`hdparm` 程序是 IDE 硬盘需要的，但 SCSI 硬盘不需要。如果你的系统中有 IDE 硬盘，你必须保留 `hdparm` 程序，但如果没有 IDE 硬盘，你可以安全地从系统中移除它。`hdparm` 是一个优化 IDE 驱动器的小型 Linux 工具。SCSI 驱动器不需要优化，因为它们能够以全速（80 Mbps 到 160 Mbps）运行。

- 从你的系统中删除 `hdparm` 软件包，使用以下命令：

`[root@deep # rpm -e hdparm`

### mkitnrd 软件包：

`mkitnrd` 程序是 SCSI 或 RAID 硬盘需要的，但 IDE 硬盘不需要。如果你的系统中有 SCSI 或 RAID 硬盘，你必须保留此程序（`mkitnrd`），但如果没有 SCSI 或 RAID 硬盘，你可以安全地从系统中移除它。

- 从你的系统中删除 `mkitnrd` 软件包，使用以下命令：

`[root@deep # rpm -e --nodepeps mkitnrd`

### xconfig 软件包：

使用 `kbconfig`, `mouseconfig`, `timeconfig`, `netconfig`, `authconfig`, `ntsys` 和 `settool` 程序来设置你的键盘语言和类型、鼠标类型、默认时区、以太网设备、NIS 和影子密码、位于 `/etc/rc.d` 目录下的众多符号链接，以及一个文本菜单实用程序，该程序允许你访问所有这些功能。

## 安装问题

## 第 2 章

在 Linux 服务器的安装阶段完成这些配置后，很少需要再次更改它们。因此，您可以卸载这些配置。如果将来您需要通过测试菜单更改键盘、鼠标、默认时间等，您只需要使用原始 CD-ROM 上的 RPM 重新安装程序即可。

- 若要从系统中删除所有程序，请使用以下命令：

`[root@deep]$ # rpm -e kbdconfig mouseconfig timeconfig netconfig authconfig ntysav setconfig`

### newt 软件包：

`newt` 软件包为文本用户界面提供了一个开发库。它主要由所有配置包（config packages）使用。由于所有配置包已从服务器移除，我们可以安全地从系统中删除 `newt`。如果您决定保留上述配置包（`kbdconfig`、`mouseconfig` 等），则应保留 `newt`，否则应将其将其删除。

- 若要从系统中删除 `newt` 软件包，请使用以下命令：

`[root@deep]$ # rpm -e newt`

### lilo 软件包：

`lilo` 包为 Linux 提供了一个引导程序。请记住，在我们的安装过程中，我们选择了 GRUB 而不是 LILO 作为 Linux 的引导程序。因此，您可以安全地从系统中删除此包，因为它确实没有用到。

- 若要从系统中删除 `lilo` 软件包，请使用以下命令：

`[root@deep]$ # rpm -e lilo`

`[root@deep]$ # rm -f /etc/lilo.conf anaconda`

### reisersfs-utils 软件包：

`reisersfs-utils` 包含了许多工具，用于创建、检查、修改和纠正 ReiserFS 文件系统中的任何不一致。ReiserFS 是另一种 Linux Ext3 文件系统。在我们的 Linux 配置中，使用 Ext3 作为文件系统，因此我们不需要保留此包。除非您打算在服务器上运行 ReiserFS 而不是 Ext3。

- 若要从系统中删除 `reisersfs-utils` 软件包，请使用命令：

`[root@deep]$ # rpm -e reisersfs-utils`

### quota 软件包：

`quota` 程序是用于监控和限制用户/组磁盘使用情况系统管理工具。该程序必须在需要监控和限制目录磁盘空间的服务器上安装。

- 若要从系统中删除 `quota` 软件包，请使用以下命令：

`[root@deep]$ # rpm -e quota`

### indexhtml 软件包：

`indexhtml` 包包含了由浏览器显示的图形界面和欢迎页面。这些 HTML 页面是关于 Red Hat Linux 的。在服务器安装中，特别是当没有图形界面（GUI）时，不需要此包。

- 若要从系统中删除 `indexhtml` 软件包，请使用以下命令：

`[root@deep]# rpm -e indexhtml`

### usutils 软件包：

`usutils` 软件包提供了用于检查连接到系统总线的设备的 Linux 工具。在服务器环境中，不使用任何 USB 设备，可以安全地从服务器上移除此包。该包仅在需要打印机和其他任何类型媒体的 Linux 工作站安装中使用。

- 若要从系统中删除 `usutils` 软件包，请使用以下命令：

`[root@deep]# rpm -e usutils`

### hwda 软件包：

`hwda` 包包含了各种硬件识别数据，主要用于 USB 和 XFree6。请记住，XFree6 与图形界面相关，由于我们不使用任何 GUI，可以从系统中移除此包。

- 若要从系统中删除 `hwda` 软件包，请使用以下命令：

`[root@deep]# rpm -e hwda`

### parted 软件包：

`parted` 包包含了用于创建、删除、调整大小、移动和复制磁盘分区的工具。当您需要处理磁盘结构时，它是非常有用的。在操作系统的安装过程中，不需要分区或更改磁盘组织。生产服务器上很少使用此工具，这就是我建议您卸载它的原因。如果您为了以后使用保留它，可以这样做。

- 若要从系统中删除 `parted` 软件包，请使用以下命令：

`[root@deep]# rpm -e parted`

### hesiod 软件包：

`hesiod` 包是另一个可以从我们的 Linux 服务器设置中卸载的包。使用 DNS 功能访问不经常变化的数据库。在大多数情况下，我们不需要它，只有当您认为服务器的某些特殊配置需要它时，才保留它。

- 若要从系统中删除 `hesiod` 软件包，请使用以下命令：

`[root@deep]# rpm -e hesiod`

### mt-st 软件包：

`mt-st` 包提供了控制和管理系统中磁带驱动器的工具。只有当您的系统中运行磁带备份媒体时，才保留它。

- 若要从系统中删除 `mt-st` 软件包，请使用以下命令：

`[root@deep #] rpm -e mt-st`

### man-pages 软件包：
