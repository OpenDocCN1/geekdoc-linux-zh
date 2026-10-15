
# Linux UPS 支持软件包

Linux 中有许多软件包可以提供 UPS 支持。其中一些是通用软件包，可以配置为与大多数 UPS 配合，而另一些专门针对特定品牌的 UPS。`UPS HOWTO` 提供了一份可用 UPS 软件包的完整列表。某些可用软件包包括：

- **Enhanced APC BackUps**：该软件包支持 APC 智能 UPS，包括对该系列 UPS 智能功能的部分支持。
- **Apcd**：该软件包支持 APC 智能 UPS，包括对该系列 UPS 智能功能的部分支持。
- **Smupsd**：该软件包运行在 `RedHat Linux` 上，并监控 APC 智能 UPS。当它检测到电源故障且 UPS 回退到电池供电时，它会关闭系统。该软件包提供了实时监控 UPS 状态以及记录 UPS 参数以供后续分析的功能。
- **Genpower**：该软件包为 UPS 提供通用支持。包含许多流行 UPS 的预构建配置，并可以为其他 UPS 进行手动配置。
- **Checkups**：该软件包监控并控制 BEST UPS。软件提供了“哑模式”（`dumb mode`）支持和部分智能模式能力，包括在 UPS 电源故障时信号 UPS 关机，并在温度过高时关机。
- **Bestups**：该软件包在智能模式下监控并控制 BEST Fer UPS。
- **Apcusd**：该软件包为 APC UPS 提供广泛支持，包括在智能模式下运行的智能 UPS。

其他软件包列在 `UPS HOWTO` 中。

## 提示 11.5.4：为你的 UPS 安装 genpower

`genpower` 软件包侧重于 `genpowered` 守护进程。`genpower` 的当前版本位于 `http://unixite.unc.edu/pub/linux/system/ups/genpower-1.0.2.tgz`。你可以通过以下步骤下载并安装 `genpower`：

1. 将 `genpowered` 归档下载到逻辑位置，例如 `/tmp`。在讨论中，假设你已将文件下载到 `/tmp`。

2. 在逻辑位置（例如 `/tmp`）中使用以下命令解压文件：

```
# cd /tmp<Enter>
# tar xzvf genpower-1.0.2.tgz<Enter>
```

3. 使用以下命令编译软件：

```
# make all<Enter>
```

4. 使用命令安装编译好的软件：

```
# make install<Enter>
```

5. 编辑 `/etc/inittab` 文件并添加以下行：

```
pf::powerfail:/etc/genpowerfail start
```

```
pg::powerokwait:/etc/genpower stop
```

6. 通过向你的 `/etc/rc.d/local` 本地文件添加以下行，配置 Linux 在开机启动时启动 `genpower`：

```
genpower <line> <ups-type>
```

其中 `line` 是 UPS 连接的设备，例如 `/dev/ttyS0` 或 `/dev/ttyS1`，`ups-type` 是 `genpower` 支持的 UPS 类型名称之一：

- `power`：用于与 `power` 兼容的 UPS 和电缆。
- `tripp-nt`：用于与 `TrippLite` UPS 及与 Windows NT 兼容的电缆。
- `apcl-nt`：用于 APC UPS 及与 Windows NT 兼容的电缆。
- `apc2-nt`：用于 APC UPS 及与 Windows NT 兼容的电缆的替代类型。
- `apc-linux`：用于 `genpower` 文档概述的 APC UPS 和 Linux 自定义电缆。

7. 重启你的 PC 以启动 `genpower`。

`genpower` 文档提供了完成安装后对 `genpower` 安装进行故障排除的指导。

## 提示 11.5.5：测试你的 genpower 安装

在安装 `genpower` 后，如提示 11.5.4“为你的 UPS 安装 genpower”所讨论，你需要进行一些测试以确保软件运行正常：

- 断开 UPS 的交流电（AC power）。
- 恢复 UPS 的交流电。
- 再次断开 UPS 的交流电。

# 让 LINUX 良好运行：核心技巧与技术

# 11：与外设和硬件一起工作

## Tip 11.6.1：Linux 与笔记本电脑

在笔记本电脑上运行 Linux 并不困难。许多笔记本都得到了良好的支持。然而，并非所有笔记本功能都得到了支持。特别是以下硬件可能会有问题：

- 图形芯片组
- 声卡
- PCMCIA 控制器
- 即插设备

在购买笔记本电脑之前，请确保你购买的笔记本与 Linux 基本兼容，参考以下文档：

- `Laptop HOWTO`：`http://www.linuxdoc.org/Laptop-HOWTO`
- `Laptop`：`http://www.linuxdoc.org/Laptop/`

## Tip 11.6.2：在 Linux 中激活高级管理

为了让 Linux 支持现代笔记本电脑的高级电源管理，如提示 11.6.2 所示，必须确保 `APM` 支持编译到内核中。你可以使用以下命令检查内核是否编译了 `APM`：

```
$ dmesg | grep apm<Enter>

ap: BIOS version 1.2 Flags 0x03 (Driver version 1.9)
```

如果该命令没有返回类似于所示笔记本 APM 版本的行，则你需要重新编译内核。请参考第 10 节“管理 Linux 系统”，使用以下选项重新编译并构建内核：

- `CONFIG_APM_IGNORE_USER_SUSPEND`
- `CONFIG_APM_DO_ENABLE`
- `CONFIG_APM_CPU_IDLE`
- `CONFIG_APM_DISPLAY_BLANK`
- `CONFIG_APM_POWER_OFF`
- `CONFIG_APM_IGNORE_MULTIPLE_SUSPEND`
- `CONFIG_APM_IGNORE_SUSPEND_BOUNCE`
- `CONFIG_APM_RTC_IS_GMT`
- `CONFIG_APM_ALLOW_INTs`

## Tip 11.6.3：获取 apmd

一旦你的内核支持 `APM`（如提示 11.6.2 所示），你需要安装 `apmd` 工具以实现笔记本的管理功能。`apmd` 工具包含在大多数 Linux 发行版中，包括 `RedHat Linux` 7 和 `Core Linux` 1.2。如果你的系统没有包含 `apmd` 工具或需要更新版本的软件，可以从 `ftp://metalab.unc.edu/pub/linux/system/power` 下载最新版本。

`apmd` 的最新版本是 2.4，以 `apmd-2.4.tar.gz` 压缩 tar 归档形式分发。

# 让 LINUX 运行起来：核心技巧与技术

## 提示 11.6.4: 安装 apmd

大多数 Linux 发行版已经包含了用于电源管理的 `apmd` 软件包。例如，`RedHat Linux` 7 已经包含了 `apmd`。如果你正在运行 `RedHat Linux` 7，可以使用以下命令检查系统中是否已安装了完整版本的 `apmd`：

```
rpm -ga | grep apmd<ENTER>
```

你的系统应该显示如下结果：

```
apmd-3.0final-18
```

如果缺少此文件，你需要从 `RedHat` CD-ROM 安装它。将 CD-ROM 插入你的 CD-ROM 驱动器，并使用命令挂载它：

```
mount /mnt/cdrom<ENTER>
```

接下来，使用 `rpm` 来安装该文件，如下：

```
rpm -i /mnt/cdrom/RedHat/RPMS/apmd-3.0final-18.i386.rpm<ENTER>
```

## 提示 11.6.5: 在 Linux 中使用 apmd 进行电源管理

在内核中编译了 `APM` 支持并安装了 `apmd` 软件包的系统中使用高级电源管理是非常简单的：

1. 你可以使用 `apmd` 命令的分钟标志来显示剩余电池寿命的数：

```
# apm -minutes<ENTER>
AC on-line, battery status high: 100%
```

2. 你可以使用 `apmd` 命令的 `--standby` 标志将系统进入待机模式：

```
# apm -standby<ENTER>
```

可以通过移动鼠标或按下键盘从待机模式唤醒计算机。

3. 你可以使用 `apm` 命令的 `--suspend` 标志将系统进入挂起模式：

```
# apm -suspend<Enter>
```

可以通过电脑的电源按钮从挂起模式唤醒计算机。

如果你按照提示 11.6.3 “获取 `apmd`”中所述从网上下载了 `apmd`，请执行以下步骤安装软件：

将你的当前目录更改到解压 `apmd` 归档文件的目录：

```
# cd /tmp<ENTER>
# tar xzvf apmd-2.4.tar.gz<ENTER>
```
