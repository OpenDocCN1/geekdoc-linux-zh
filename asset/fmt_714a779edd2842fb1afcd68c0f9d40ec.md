
其他设置
为崩溃内核配置预留 RAM 的起始部分。这是一个非常重要的设置，请留意。为了正常工作，崩溃内核使用一段专门为其预留的内存。此内存分配的起始部分需要定义。如果您打算从 16 MB 处启动崩溃内核 RAM，则该值需要设置为以下（十六进制）：

```
CONFIG_PHYSICAL_START=0x1000000
```

# 收集内核核心 (Kdump) 149

**配置 kdump 内核以便其被识别。** 设置此后缀允许 kdump 选择正确的内核进行启动，因为您的系统在 `/boot` 目录下可能有多个内核。通常情况下，经验法则要求崩溃内核的命名与您的生产内核相同，仅缺少一个 `-kdump` 后缀。您可以通过在终端中运行 `uname -r` 命令查看您正在运行的内核版本，然后检查 `/boot` 目录下列出的文件。

```
CONFIG_LOCALVERSION="-kdump*"
```

版权 ©Intel Corporation. 保留所有权利

## 崩溃（捕捉）内核

此内核需要按照上述相同的参数进行编译，但有一个例外。Kdump 不支持将压缩镜像作为崩溃（捕捉）内核。因此，您不应该压缩此镜像。这意味着您的生产内核可能被命名为 `vmlinuz`，而 kdump 崩溃内核需要是非压缩的，因此命名为 `vmlinux`，或者说是 `vmlinux-kdump`。

## Kdump 软件包和文件

这是 Kdump 工作必须在系统上安装的所需软件包列表。请注意，您的内核必须正确编译，这些软件包才能按预期工作。无论如何您很可能成功安装它们，但不能保证它们能够工作。软件包名及其信息见表 6.1。

获取这些软件包的最佳方法是从软件存储库。这确保了您将使用兼容性最好的 Kdump 和 Kexec 版本。同样，请注意生产内核也必须安装 `kernel-kdump`。此软件包包含了在标准内核崩溃时启动的崩溃内核，提供了一个可以在崩溃期间捕捉标准内核状态的环境。此软件包的版本必须与内核相同。

以下列出了最重要的 Kdump 相关文件：

| 软件包名称 | 软件包信息 |
| --- | --- |
| Kdump | Kdump 软件包 |
| Kexec-tools | Kexec 工具包 |
| Kernel-debuginfo | 崩溃分析（可选） |

*kernel-debuginfo 软件包需要与内核匹配。*

## 表 6.2 Kdump 文件

| 路径 | 信息 |
| --- | --- |
| `/etc/init.d/kdump` | Kdump 服务 |
| `/etc/sysconfig/kdump` | Kdump 配置文件 |
| `/usr/share/doc/packages/kdump` | Kdump 文档 |

Kdump 安装还包含一个 gdb 封装脚本 (`gdump`)，用于简化在 Kdump 镜像上使用 gdb。使用 gdb 以及其他分析工具需要存在 `-debuginfo` 软件包。

## KdUMP 配置

在上一节中，我们检查了为了 Kexec 正常工作需要设置的内核配置参数。现在，假设您有一个可以启动到登录界面并由厂商或您使用相关参数编译的内核，我们将查看需要哪些额外步骤来让 Kdump 真正工作并收集崩溃转储。

我们将配置两次 Kdump：一次用于本地转储，一次用于网络转储，类似于我们对 LKCD 所的操作。这是一个非常重要的步骤，因为 LKCD 仅限于特定子集的网络转储。Kdump 提供了强大得多且灵活的网络功能，包括 FTP、SSH、NFS 和 CIFS 支持。

## 配置文件

Kdump 的配置文件是 `/etc/sysconfig/kdump`。我们将从基本的本地转储功能开始。稍后我们还将演示网络崩溃。在进行任何更改之前，您应该保存备份！

```
KDUMP_KERNELVERSION
```

> 版权 ©Intel Corporation. 保留所有权利

此设置指向我们之前审查的 `CONFIG_LOCALVERSION` 内核参数。我们指定了后缀 `-kdump`，这告诉我们的系统使用带有 `-kdump` 后缀的内核作为崩溃内核。作为短描述，如果没有使用值，将使用最近安装的 Kdump 内核。默认情况下，崩溃内核通过 `-kdump` 后缀识别。

通常情况下，只有当对 Kdump 内核使用非标准后缀时，此设置才有意义。除非对特定内核版本有特殊需求，否则大多数用户不需要更改此设置并可以保持默认值。

# 收集内核核心 (Kdump) 151

```
KDUMP_KERNELVER="*"
```

Copyright ©Intel Corporation. 保留所有权利

## 配置 KDUMP_COMMANDLINE

此设置告诉 Kdump 启动崩溃内核所需的参数集。在大多数情况下，你将使用与生产内核内核相同的参数集，因此不需要更改它。要查看当前的参数集，可以对 `/proc/cmdline` 执行 `cat` 命令。当未指定字符串时，该参数集将作为默认值。我们在测试 Kdump（确切说是 Kekec）并模拟崩溃启动时，将使用此设置。

```
KDUMP_COMMANDLINE="*"
```

Copyright ©Intel Corporation. 保留所有权利

## 配置 KDUMP_COMMANDLINE_APPEND

如果你打算使用或必须使用 SMP（对称多处理）内核，这是一个非常重要的细节。正如我们之前所看到的，在配置内核编译参数时，我们看到 Kdump 的崩溃内核不能使用超过单个内核。因此，如果你正在使用 SMP，此参数是*必须的*。如果内核在配置时禁用了 SMP，则可以忽略此设置。

```
KDUMP_COMMANDLINE_APPEND="MAXCPUS=1"
```

Copyright ©Intel Corporation. 保留所有权利

## 配置 KekEC_OPTIONS

如前所述，Kekec 是从生产内核上下文启动崩溃内核的机制。为了正常工作，Kekec 需要一组参数。基本设置由 `/proc/cmdline` 定义。可以使用此指令指定额外参数。在许多情况下，该字符串可以为空。但如果你在启动 Kdump 时收到错误，可能是 Kdump 无法解析你的内核版本。为了让 Kdump 字面解析额外参数，你可能需要添加 `--args-linux`。你应该尝试不同的设置，看看哪一个有效。如果你感兴趣，可以将你的引擎指向 `"--args-linux"` 并查看围绕此主题的邮件列表条目。尝试错法是最佳选择。我们稍后会讨论这一点。

```
KDUMP_OPTIONS="--args-linux"
```

Copyright ©Intel Corporation. 保留所有权利

# 152 第6章 深入浅出

## 配置 KDUMP_RUNLEVEL

这是另一个重要的指令。它定义了崩溃内核应该启动的运行级别。如果你想 Kdump 将转储保存到本地设备，可以将 runlevel 设置为 1。如果你想 Kdump 将转储保存到网络存储（如 NFS、CIFS 或 FTP），你需要网络功能，这意味着 runlevel 应设置为 3。你也可以使用 2、5 等。如果你选择 runlevel 5（不推荐），请确保崩溃内核有足够的内存进入图形环境。

```
KDUMP_RUNLEVEL="1"
```

© ©Intel Corporation. 保留所有权利

## 配置 KDUMP_IMMEDIATE_REBOOT

此指令告诉 Kdump 在转储完成后是否重启崩溃内核。如果 `KDUMP_DUMPDEV` 参数为空，则此指令被忽略。也就是说，如果使用了转储设备，在完成转储镜像拷贝到目标目录的后处理之前，崩溃内核不会重启。你可能想要保留默认值。

```
KDUMP_IMMEDIATE_REBOOT="yes"
```

© ©Intel Corporation. 保留所有权利

## 配置 KDUMP_TRANSFER

此设置告诉 Kdump 如何处理转储内存。例如，你可能希望立即进行后处理。`KDUMP_TRANSFER` 需要非空的 `KDUMP_DUMPDEV` 指令。可选范围有 `/proc/vmcore` 和 `/dev/oldmem`。这与 LKCD 工具类似。通常情况下，`/proc/vmcore` 或 `/dev/oldmem` 将指向未使用的交换分区。目前，我们将仅使用默认设置，即将核心镜像拷贝到 `KDUMP_SAVEDIR`。我们稍后会讨论 `KDUMP_DUMPDEV` 和 `KDUMP_SAVEDIR` 指令。然而，只有在讨论崩溃分析时才会研究更高级的传输选项。

```
KDUMP_TRANSFER=""
```

© Intel Corporation. 保留所有权利

# 收集内核核心 (Kdump) 153

## 配置 KDUMP_SAVEDIR

这是一个非常重要的指令。它告诉我们内存核心将存在哪里。目前我们讨论的是本地转储，目标指向本地文件系统的目录。我们将看到网络示例。默认情况下，设置指向 `/var/log/dump`。

```
KDUMP_SAVEDIR="file:///var/log/dump"
```
