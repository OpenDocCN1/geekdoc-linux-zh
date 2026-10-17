
`tar cvf /dev/rfd.0 file file2`

从 `/usr/include` 和 `/etc` 归档文件：

```
tar cvf -C /usr/include -C /etc
```

在管道中使用 `tar` 将整个文件系统层次从 `fdir` 复制到 `todir`：

```
cd fmd ; tar cf - | (cd todir ; tar xf -i)
```

将当前目录下的 `my_project` 中的所有文件和目录归档到当前目录下的 `my_project.TAR` 文件中：

```
tar -cvf my_project.TAR my_project
```

# 警告

由于行业标准和互操作性目标，`tar` 不支持归档大于 2GB 的文件，或用户/组 ID 大于 60K 的文件。用户/组 ID 大于 60K 的文件将在以当前进程的用户/组 ID 下归档和恢复。

从 HP-UX Release 8.0 开始，默认版本已从 O 变为 N。

由于头部结构中的内部限制，使用 N 版本时，并非所有少于 256 个字符的文件都能适应。如果文件名不符合要求，`tar` 会打印一条消息且不归档该文件。

使用 N 版本键时，链接名仍然限制为 100 个字符。

没有方法可以请求文件的第 n 次出现。

磁带错误会被妥善处理。

`u` 函数键可能会缓慢。

如果归档文件是磁盘文件、软性磁盘或卡带磁带，并且输出时指定的块因子（blocking factor）不是默认值，则输入时必须指定相同的块因子，因为归档中没有显式说明块因子。如果不遵循此规则更新或更新归档可能会破坏它。

某些之前的版本的 `tar` 声称支持使用 `t` 函数配合列表对文件名进行选择性列出。这似乎是文档中的错误，因为该功能在原始源代码中并没有出现。

没有方法可以将绝对路径恢复到相对位置。

`tar` 始终会将写入归档文件的信息填充到块大小的下一个倍数。因此，如果您正在创建一个小型归档并写入了一个块的信息，`tar` 报告说如果使用 `b` 函数修饰符，归档的实际大小可能会更大。

注意 `tar cm0` 等同于 `tar cm0`。

不要在块特殊设备上创建归档。尝试这样做会导致过度磨损，导致驱动器硬件过早故障。

# tar

# 153

## 依赖关系

700/800 系列
QIC 或 8mm 设备上不支持 `r` 和 `u` 函数键。如果在 QIC 或 8mm 设备上使用这些选项，`tar` 将失败并显示以下消息：

```
tar: option not supported for this device
```

# 作者

`tar` 由 AT&T、加利福尼亚大学伯克利分校、HP 和 POSIX 开发。

## 文件

- `/dev/rmt/*`
- `/dev/rfd/*`
- `/tmp/tar*`

# 另参

- `ar(1)`, `cpio(1)`, `acl(5)`, `mt(7)`。

## 标准符合性

`tar`: SVID2, SVID3, XPG2, XPG3

## "sw" 命令摘要

`"sw"` 命令 - 与软件分发相关的命令摘要。

| `swacl(1M)` | 亥尔斯-帕特公司 | `swacl(1M)` |
|---|---|---|
| 名称 | `swacl` - 查看或修改保护软件产品的访问控制列表 (ACLs) | | |
| 概要 | `swacl -level [-M acl_entry] -D acl_entry] -F acl file] [-x -X option_file] [-f software_file] [-t target_file] [software_selections] [@ target_selections]` | | |

| `swagentd(1M)` | 亥尔斯-帕特公司 | `swagentd(1M)` |
|---|---|---|
| `swagent(1M)` | | |
| 名称 | `swagentd` - 为本地或远程 SD 软件管理任务提供服务，包括调用 `swagent` 命令。 | | |
| `swagent` - 作为 SD 命令的代理执行 SD 软件管理任务。 | | |
| `SWAGENT.EXE` - 执行 HP OpenView 软件分发器 PC 管理任务，或为分发提供本地 PC 软件。请见下文“备注：”。 | | |

`swagentd [-k] [-n] [-r] [-x option=value] [-X option_file]`
`SWAGENT.EXE` (仅限 HP OpenView 软件分发器)

| `swcluster(1M)` | | `swcluster(1M)` |
|---|---|---|
| 名称 | `swcluster` - 从无盘服务器安装或删除软件 | | |

概要
`cluster [XToolkit Options] [-v][v] [-i] [-p] [-f] [-r] [-b] [-1 list_class] [-n] [-s source] [-C session_file] [-S session_file] [-x option=value] [-X option_file] [software_selections] [@ target_selections]`

## sw* 命令摘要

`swconfig(1M)` 亥尔斯-帕特公司 `swconfig(1M)`
名称
`swconfig` - 配置、取消配置或重新配置已安装的软件

概要
`swconfig [-p] [-v] [-u] [-x option=value] [-X option_file] [-f software_file] [-t target_file] [-C session_file] [-S session_file]`

`swgetools(1M)` 亥尔斯-帕特公司 `swgetools(1M)`
名称
`swgetools` - 从媒体检索 SD 产品的工具

`swinstall(1M)` 亥尔斯-帕特公司 `swinstall(1M)`
`swcopy(1M)`
名称
`swinstall` - 安装软件
`swcopy` - 为安装或分发软件

`swjob(1M)` 亥尔斯-帕特公司 `swjob(1M)`
`sd(1M)`
名称
`swjob` - 用于创建和监控 任务的交互式界面

`swlist(1M)` 亥尔斯-帕特公司 `swlist(1M)`
名称
`swlist` - 显示关于软件的信息

`swmodify(1M)` 亥尔斯-帕特公司 `swmodify(1M)`
名称
`swmodify` - 修改目标根或仓库中的软件

`swpackage(1M)` 亥尔斯-帕特公司 `swpackage(1M)`
名称
`swpackage` - 将软件打包到目标仓库或磁带

# 第 2 章

## HP-UX 文件系统及相关命令

## 引言

深入理解 HP-UX 文件系统对于执行系统管理至重要。在本章中，我将涵盖以下主题：

- HP-UX 文件类型 - 本节描述了 HP-UX 中不同类型的文件，以及如何使用 `file` 命令来确定文件类型。
- 文件系统布局 - 你需要了解文件系统的布局，包括重要的目录及其内容。
- 逻辑卷管理器 (LVM) - 你可能会使用 LVM 来管理系统中的数据。我将在本节中提供 LVM 的背景知识。
- 使用 LVM 重新配置磁盘的示例 - 我包含了一个在真实系统上执行的复杂磁盘重配置示例，用以展示使用了多少 LVM 命令。虽然此磁盘重配置不适用于你的系统，但它是使用 LVM 命令的一个良好范例。
- 一些额外的文件系统命令。

## HP-UX 文件类型

HP-UX 系统上有多种不同的文件类型。文件是在 HP-UX 系统上存储信息的手段。你执行的命令、使用的应用程序、存储的数据以及访问的设备（如打印机和键盘）都包含在文件中。这是 HP-UX 使其既简单又复杂的方面之一：简单是因为你知道那里的一切都是文件；复杂是因为文件的内容可以是任何东西，从你可以读取的简单数据到由系统管理员通过特定命令创建的设备文件，比而皆有。

系统上的每个文件都有一个文件名。操作系统负责所有与文件系统相关的任务；你只需要知道文件名以及如何使用它。我们等要查看的文件类型类型有：

- 文本文件
- 数据文件
- 源代码文件
- 可执行文件
- Shell 程序
- 链接
- 设备文件

## 文本文件

还有比包含字符的文件（就像你现在正在这一章中阅读的这些）更简单的吗？这些 ASCII 字符是代表你所执行工作的字母和数字。例如，如果你使用 HP-UX 编辑器创建电子邮件或信件，在大多数情况下，你都在创建一个文本文件。以下是文本文件部分的示例：

```
*
*      *
*      HP LaserROM/UX
*      README File
*      *
********************************************************************************
```
