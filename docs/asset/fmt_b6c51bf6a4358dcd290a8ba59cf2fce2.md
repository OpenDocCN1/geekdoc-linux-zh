
**图 227.** Hdparm 性能测试

另一个流行的硬盘性能测试工具是 `bonnie`，可以在 http://www.textuality.com/bonnie/ 找到（发行版包含适用于 SuSE Linux 的 RPM 包）。但请注意，这些测试最有用的是作为在单机上测试不同参数设置的相对测量方法，而不是作为不同系统之间的比较。

272 xSeries 和 Netinity SuSE Linux 集成指南

要测试你的网络吞吐量，你可以使用 `netperf`（位于 http://www.netperf.org/netperf/NetperfPage.html）或 `bing`（包含在 SuSE Linux 中）。

# 第 15 章 建立 Beowulf 集群

长期以来，并行计算一直是商业厂商的领域。通过使用 Linux，现在可以使用带有现成组件的普通 PC 建立一台强大的超级计算机，这些 PC 通过快速以太网连接在一起，或者使用像 SCI 或 Myrinet 等特殊高速互连技术。Beowulf 集群以普通并行计算机的一小部分成本提供了更高的计算性能（性价比通常比“普通”超级计算机好三到十倍）。

Beowulf 是斯堪的纳维亚土地的斯尔德，是其中一部最古老的英语诗中的角色。传说他击败了怪物格林德尔（历史背景请见 http://legends.dm.net/beowulf/index.html 和 http://www.lnistar.com/literature/beowulf/beowulf.html）。

首个 Beowulf 集群是由 Donald Becker 和 Tom Sterling 于 1994 年在 NASA 戈达德飞行中心建立的。Don Becker 也因他在 Linux 内核方面的工作而在 Linux 社区闻名。

为了利用并行性，你需要至少两台运行 Linux 的 PC 以及它们之间功能良好的 TCP/IP 连接。普通以太网对于入门是可以的；但它无法提供最佳性能，对于需要在许多节点间通信的应用程序来说，这一点至关重要。一种方法是使用库，如 `PVM`（并行虚拟机）或 `LAM/MPI`（局域网消息传递接口）。这将在被涉及。本章将重点介绍如何设置 `PVM` 以及如何使用著名的光线追踪软件 `POVray` 进行并行计算。`POVray` 是一种通过描述坐标、光源、纹理和表面属性（如反射率或不透明度）来创建场景真实图像的方法。光线追踪器计算图中所有光线的反射、阴影和折射，并生成场景的真实图像。关于 `POVray` 的更多信息可以在以下网站找到：

http://povray.org

要建立一个简单的 Beowulf 集群，`PVM` 需要在这些机器上安装。`XPVM` 是一个监控虚拟机通信和设置的工具，如果节点数量不是太大（大约 20-30 个）。`XPVM` 只需要在主节点上安装。有一种名为 `MOSIX` 的特殊共享软件，允许集群中的进程迁移。`MOSIX` 需要经过补过的 Linux 内核，将在此涉及。

- `PVM`
- `XPVM`
- `NFS`

# 第 16 章 备份与恢复

备份和快速恢复数据显然非常重要，但许多管理员将其留到最后，直到为时已晚。有了商业软件包 `BRU`（Enhanced Software Technologies）、`BackupEDGE/RecoverEDGE`（MicroLite）或 `Orkeia`（Knox Software）的便利性，无需等待。

> 我们建议不要将磁带设备连接到 IBM ServeRAID 适配器。请为磁带设备使用独立的 SCSI 控制器。

## 16.1 BRU

`BRU` 是一种备份和恢复实用，相对于其他常用的工具（如 `tar`、`cpio`、`volopy` 和 `dump`）有显著增强。`BRU` 设计用于大多数备份设备，包括卡带、4mm DAT、8mm（Exchange）和 9 轨磁带设备。

`BRU` 包括增量备份、全备份、多卷存档、分和更新、错误检测与恢复、随机访问能力、文件比较、文件覆盖保护以及比以前版本的速度。

### 16.1.1 安装 BRU

在开始之前，你需要以下信息：

- 磁带机的设备名称。在 SuSE Linux 下，这通常是带回的 `/dev/st0` 和非带回的 `/dev/nst0`。
- 备份介质的大小（单位为 MB）。

要使用 `tar` 命令从软盘驱动安装 `BRU`，请输入：

```bash
cd /tmp
tar xvf /dev/fd0
./install
```

按照 readme 文件和许可的提示操作，直到出现以下窗口：

输入您的备份设备的字母，并根据您的设备回答以下相关问题。

如果您已为所有备份设备输入了信息，系统将询问您是否想要安装 X11 界面。选择 Y。

安装程序需要创建一个 `xbru` 目录。您可以选择一个路径，或接受默认的 `/usr/local/`。

安装程序将可执行文件安装到用户指定的目录。默认路径为 `/usr/local/bin`。

注意
关键配置文件为 `/etc/brutat`。高级信息请参阅《BRU 用户指南》。除非您确定自己在做什么，否则请勿进行编辑。

`BRU` 现在已安装。

## 16.1.2 基础命令

`BRU` 的基本命令结构为：

```
# bru modes [control options] [selection options] [files]
```

其中 `bru` 是命令或程序，后面紧跟指定备份、恢复或各种查询的模式。控制选项指定要处理的文件或目录。`Files` 是 `bru` 命令指定的 target。

## 16.1.3 基础备份

要备份单个文件 `/home/ayne/.profile`：

```
# bru -c -vvvv -G /home/ayne/.profile
```

要备份整个目录 `/home/ayne/`：

```
# bru -c -vvvv -G /home/ayne
```

要备份整个系统：

```
# bru -c -vvvv -G /
```

## 16.1.4 基础恢复

恢复单个文件 `/home/ayne/ayne/.profile`：

```
# bru -x -vvvv -ua -w /home/ayne/.profile
```

恢复整个目录 `/home/ayne/`：

```
# bru -x -vvvv -ua -w /home/ayme
```

恢复整个系统：

```
# bru -x -vvvv -ua -w /
```

## 16.1.5 基础验证与列表

`-i` 模式可以与备份命令配合使用，也可以单独使用。`-i` 模式读取数据块并验证校验和。如果配合详细选项（`-vvv`）使用，`BRU` 将显示文件列表。

`-g` 模式显示归档头。更多信息请参阅《BRU 用户指南》。

`-gg` 模式显示磁带目录。此模式仅在创建归档时使用了 `-g` 选项后可用。

## 16.1.6 X 界面

要使用 `BRU` 界面，需要 X 环境。输入：

您将看到类似于图 230 的窗口。通过此界面您可以：

- 创建和恢复备份
- 创建备份定义
- 调度备份
- 列出归档内容
- 查看 `BRU` 日志

## 16.1.7 BRU 中的按钮

三个主按钮（`Full`、`Level 1` 和 `Level 2`）是备份系统、目录或单个文件的快捷方式。

- 选择 `Full` 备份用户目录中的所有文件，如果是 root 则备份整个系统。
- 选择 `Level 1` 备份自上次备份以来修改的文件。如果没有进行过备份，则视为全量备份。
- 选择 `Level 2` 备份自上次 `Level 1` 备份以来修改的文件。如果没有进行过 `Level 1` 备份，则视为全量备份。

## 16.1.8 创建归档

使用 `BRU` 界面创建归档非常简单（见图 231）。

左侧的框显示当前目录。您可以通过选择文件并点击相应的按钮从备份列表中添加或删除文件。

要访问搜索功能，请进入菜单（图 232）。

`BRU` 提供了一个调度工具来自动化备份。有三种定义：`Full`、`Level 1` 和 `Level 2`。

## 16.1.9 调度

要访问调度功能，请进入菜单（图 233）。

您可以根据每周、每月或单个设置备份。要添加 cron 条目，请以 root 身份登录并输入：

```
crontab -e
```

插入以下行：

```
0/5 * * * /usr/local/bin/bruschedule
```
