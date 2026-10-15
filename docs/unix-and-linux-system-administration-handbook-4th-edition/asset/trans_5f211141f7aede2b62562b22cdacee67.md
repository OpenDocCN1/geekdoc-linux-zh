

- 软件可以通过 swagentd 在远程系统上进行管理，swagentd 是一个在启动时启动的守护进程，可通过 UDP 和 TCP 进行通信。
- 软件仓库可以位于本地介质或网络目录中。
- 作业浏览器让管理员能够实时监控远程系统的安装状态。

一系列以 sw 开头（好吧，大多数）的可执行文件构成了 SD 工具包。表 12.6 列出了各个工具及其功能。

## 表 12.6 软件分发器命令列表

| 命令 | GUI? | 用途 |
|---|---|---|
| install-sd | – | 重新安装软件分发器系统 |
| sd | Y* | 管理远程作业：创建、调度、监控 |
| swacl | – | 配置 SD 安全选项 |
| swask | – | 运行交互式安装脚本 |
| swconfig | – | 配置（或重新配置）已安装的软件 |
| swcopy | Y | 将软件包复制到存储库以供将来安装 |
| swinstall | Y | 从存储库安装软件包 |
| swjob | – | sd 命令的命令行替代方案 |
| swlist | Y | 列出已安装的软件或存储库中的软件 |
| swmodify | – | 修改系统上已安装软件的目录 |
| swpackage | – | 创建新的软件包 |
| swreg | – | 注册软件仓库 |
| swremove | Y | 从系统或存储库中删除软件包 |
| swverify | – | 确认已安装软件的完整性 |
| swagentd | – | 作为 SD 命令代理（在启动时启动） |

a. 此工具仅限 GUI：它没有命令行。swjob 是命令行等效工具。
b. 又称已安装产品数据库或 IPD

大多数 SD 命令都支持一个特殊的 -x 标志，该标志会修改特定于该工具的默认选项。例如，swinstall 命令的选项中包括 allow_incompatible，允许安装适用于不同架构的软件包，以及 autoreboot，如果需要则在安装后重新启动系统。每个工具的完整选项列表在手册页或文件 /usr/lib/sw/sys.defaults 中给出。更奇怪的是，用户默认设置可以在 ~/.swdefaults 文件中配置。

swinstall 命令最常被管理员使用，尤其是那些勤于在发布时安装安全补丁的人。swinstall -i 强制进行交互式安装。如果 X 正在运行，则启动 GUI；否则，你会得到文本界面。

遗憾的是，HP-UX 没有一个方便的在线软件仓库，可以轻松地从中安装补丁。最接近的是 HP-UX 软件助手工具，它参考 HP 提供的补丁目录分析系统，下载适当的补丁包，并构建一个软件仓库，你可以使用 swinstall 从中修补系统。

让我们看几个例子。要从主机 hpux.booklab 上的基于 NFS 的软件仓库安装安全补丁 PHKL_40197，我们将运行命令

```
hp-ux$ sudo swinstall -s hpux.booklab:/hpux/patches PHKL_40197
```

swinstall 在安装期间会自动运行配置脚本。如果以后需要重新配置软件包，请使用 swconfig 命令。swconfig 将软件包自定义为本地系统（例如，通过修改 /etc 中的文件或更改目录的权限）。要重新配置 sudo 软件包，我们将运行以下命令：

```
hp-ux$ sudo swconfig -x reconfigure=true sudo
```

要删除此软件包，我们将运行 swremove sudo。swverify 检查软件包并对其关键组件执行完整性检查。使用 swverify 来修复诸如损坏的默认文件或缺失目录等问题。

swlist 显示系统上已安装的软件或存储库中可用的软件。交互式界面通常更方便搜索，但下面是一个简单的命令行，用于列出我们示例 HP-UX 系统上的与 Java 相关的软件包：

```
hp-ux$ sudo swlist "Java"
# Initializing...
# Contacting target "hpux11"...
# Target: hpux11:/
# Java15JDK      1.5.0.11.00  Java 1.5 JDK for HP-UX
Java15JDK,Jdk15 1.5.0.11.00  Java 1.5 JDK
Java15JDK,Jre15 1.5.0.11.00  Java 1.5 JRE
# Java15JRE      1.5.0.11.00  Java 1.5 JRE for HP-UX
Java15JRE,Jre15 1.5.0.11.00  Java 1.5 JRE
```

远程操作是软件分发器的强大功能。远程功能允许系统管理员将软件推送到远程系统（可选地，按预定义计划）。大多数命令都支持远程操作，一些命令，如 swinstall，其 GUI 也支持远程操作。远程操作使用远程过程调用（RPC）执行，安全性通过访问控制列表控制。有关配置远程操作，请参阅 man 5 sd。

## AIX 中的软件管理

大多数 UNIX 厂商至少尝试在软件管理领域赶上 Linux，但 IBM 在 AIX 中选择了某种石器时代的方法。SMIT install_software 快捷路径在大多数情况下是推荐的；其背后

