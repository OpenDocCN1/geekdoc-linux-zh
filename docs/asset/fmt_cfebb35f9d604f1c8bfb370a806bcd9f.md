
`-su <SE context>` 显示匹配字符串 SELinux 上下文（主体）。

`-sv <success>` 通过此选项指定 yes 或 no 显示成功或失败。如列表 25.8 所示，`success` 值位于消息结尾的 `res` 关键字，可以是成功或失败。

`-te <date> <time>` 显示等于或于给定日期和时间的消息。日期格式取决于系统的语言区域。使用 24 小时时钟如 `23:00`。对于 `en_US`，日期格式等于 `MM/DD/YY`。

`-ts <date> <time>` 显示等于或于给定时间的消息。日期和时间应用 `-te` 选项。

`-tm <terminal>` 显示带有指定终端（如 `pts/6`）的消息。

`-ua <uid>` 显示用户 ID、有效用户 ID 或登录 ID (`audit`) 符合指定的。

`-ue <uid>` 显示有效用户 ID 符合指定的。

`-ui <uid>` 显示用户 ID 符合指定的。

`-ul <login id>` 显示登录 ID 符合指定的。

`-v` 显示版本。

`-w` 显示关于 `cron` 等可执行文件。

`-x` 显示如 `/bin/sudo` 等可执行文件的消息。如列表 25.8 所示，可执行文件的完整路径位于消息中的 `exe` 关键字之后。

与 `aureport` 类似，可以使用 `-i` 选项使输出更易读，并可以使用 `-if <filename>` 提供备用日志进行搜索。当显示结果时，每条记录由四个横线分隔，每条记录前面都有一个时间戳，如列表 25.8 所示。

# 列表 25.8 ausearch -x 的结果

```
time->Fri Dec 1 00:01:01 2006
type=CRED_ACQ msg=audit(1145210930.022:2023): user pid=30718 uid=0
auid=429467295 msg=PAM: session acct=root: exe=/usr/bin/sudo
(hostname=?, addr=?, terminal=pts/3 res=success)
```

```
time->Fri Dec 1 04:01:01 2006
type=USER_START msg=audit(1145210930.022:2024): user pid=30718 uid=0
auid=429467295 msg=PAM: session open acct=root: exe=/usr/bin/sudo
(hostname=?, addr=?, terminal=pts/3 res=success)
```

# 列表 25.8 继续

```
type=USER_END msg=audit(1145210930.022:2025): user pid=30718 uid=0
auid=429496295 msg=PAM: session close acct=root : exe="/usr/bin/sudo"
(hostname?, addr=, terminal=pts/3 res=success)
```

```
time->Fri Dec 1 05:01:01 2006
type=CRED_ACQ msg=audit(1145245975.92482): user pid=2062 uid=0
auid=429496295 msg=PAM: setcred acct=root : exe="/usr/bin/sudo"
(hostname?, addr=, terminal=pts/6 res=success)
```

```
time->Fri Dec 1 09:01:01 2006
type=USER_END msg=audit(1145245975.22484): user pid=2062 uid=0
auid=429496295 msg=PAM: session close acct=root : exe="/usr/bin/sudo"
(hostname?, addr=, terminal=pts/6 res=success)
```

# 使用审计跟踪进程

可以使用 `autrace` 工具从特定进程生成审计记录。在审计运行时，不能启用其他其他规则或监视。与其他审计工具一样，`autrace` 必须以 `root` 身份运行。要审计跟踪一个进程，请使用以下步骤：

1. 临时关闭所有规则和监视：

```
auditctl -D
```

2. （可选）为了隔离进程审计记录，强制日志轮转：

```
service audit rotate
```

`autrace` 的日志将位于 `/var/log/audit/audit.log`。

3. 对命令执行 `autrace`：

```
autrace <command to trace>
```

4. 等待进程完成。系统将显示类似以下的消息：

```
Trace complete. 你可以使用 'ausearch -i -p 10773' 定位记录
```

5. 重启审计守护进程以重新启用规则和监视：

```
service auditd restart
```

6. 使用 `ausearch` 显示跟踪的详情。

# 摘要

Linux 审计系统和审计守护进程（`audit daemon`）可从内核收集系统调用和文件访问信息。审计守护进程会将这些事件的日志消息写入专用日志文件。可以使用 `aureport` 和 `ausearch` 工具生成报告，以查找失败的系统调用、确定谁在何时以及如何频繁访问文件、执行程序的成功和失败尝试等大量信息。

# 附录

- 附录 A 安装专有内核模块 525
- 附录 B 创建虚拟机 529
- 附录 C 使用 ExecShield 防止安全泄露 547
- 附录 D 故障排除 551

# 附录 A

## 本附录内容

- 安装专有模块
- 安装 NVIDIA 显示驱动程序
- 识别污染内核（Tainted Kernel）

## 安装专有内核模块

Red Hat Enterprise Linux 以内核模块的形式提供了各种硬件的支持。这些内核模块允许硬件与内核进行交互，使得操作系统的其他部分和应用程序能够与硬件通信。

理想情况下，你所需的所有内核模块都包含在 Red Hat Enterprise Linux 中。然而，如果需要其他模块，本附录将解释它们如何与内核协同工作以及如何识别它们。

Linux 内核根据 GNU 通用公共许可证（GPL）授权，这意味着其源代码可以在 `kernel.org` 供任何人下载和阅读，并且只要修改后的代码也根据 GPL 许可，任何人都可以对代码进行修改。随 Red Hat Enterprise 分发的所有内核模块均根据 GPL 或与 GPL 兼容的许可证授权。

> 提示
> 第 6 节“分析硬件”描述了如何列出和配置内核模块参数。

内核模块是如何编写的？有时，开源开发者会与硬件供应商合作，以获取编写其对应的开源内核模块所需的硬件规范。由于开源模型，随着用户发现问题并向开发者报告，或者其他开发者在发现问题时调整代码，该模块会随着时间的推移不断改进。

有时，硬件供应商会编写自己的 Linux 模块。有些甚至会将其编写的 Linux 模块开源。然而，有些供应商选择不在这 GPL 或 GPL 兼容许可证下发布其内核模块（称为专有模块）。如果开源社区还没有编写该模块的等效开源版本（通常是因为硬件刚刚发布，或者是因为开源社区没有足够的关于硬件的信息来编写开源模块），那么如果管理员想在 Linux 操作系统中使用该硬件，专有模块就是他们的唯一选择。

## 安装专有模块

安装第三方模块的过程因模块而异：

- 某些模块以 RPM 格式分发，这便于安装。参考第 5 节“使用 RPM 软件”了解安装 RPM 包的详情。
- 某些模块需要管理员运行一个脚本（下载时随模块提供），以引导你完成安装。
- 另一些模块可能需要编译模块的部分内容。然而，大多数第三方模块都带有详细的安装说明。

即使加载专有模块的过程也因模块而异：

- 某些使用可以在启动时运行的用户空间应用程序。
- 某些使用可以在启动时运行的初始化脚本。参考第 4 节“理解 Linux 概念”获取更多关于初始化脚本的信息。
- 某些要求将模块列在 `/etc/modprobe.conf` 中，例如对于名为 `example` 的第一块以太卡的模块：

```
alias eth0 example
```

在安装模块并按照加载说明后，使用 `/sbin/insmod` 命令验证其是否已加载。

底线原则：请遵循专有模块随附的说明，如果模块无法加载或无法与 Red Hat Enterprise Linux 内核正常工作，请联系模块供应商的发行商。如果没有源代码可供调试，开源社区或 Red Hat 工程团队很难排查并修复问题。

## 安装 nvidia 显示驱动程序

本节展示了为 `x86_64` 架构安装 `nvidia` Linux 驱动的过程。此示例基于从 `http://www.nvidia.com/object/linux_display_amd64_1.0-9746.html` 下载的 `1.0-9746` 版本驱动。安装不同版本的说明可能有所不同。

> 注意
