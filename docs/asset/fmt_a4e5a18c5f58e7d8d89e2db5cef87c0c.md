
这显示了所有当前加载并激活的 target。你也可以看到 `graphical.target` 和 `multi-user.target`。在加载 `graphical.target` 之前，需要先加载 `multi-user.target`。在本示例中，`graphical.target` 处于激活状态。

`rpc_pipefs.target` loaded active `rpc_pipefs.target`
`slices.target` loaded active active Slices
`sockets.target` loaded active active Sockets
`sshd-keygen.target` loaded active active `sshd-keygen.target`
`swap.target` loaded active active Swap
`sysinit.target` loaded active active System Initialization
`timers.target` loaded active active Timers

`LOAD` = 反映单元定义是否已正确加载。
`ACTIVE` = 高级单元激活状态，即 `SUB` 的泛化。
`SUB` = 低级单元激活状态，值取决于单元类型。

列出了 21 个已加载的单元。使用 `--all` 也可以查看已加载但未激活的单元。

使用 `systemctl list-unit-files` 显示所有已安装的单元文件。

这显示了所有当前加载并激活的 target。你也可以看到 `graphical.target` 和 `multi-user.target`。在加载 `graphical.target` 之前，需要先加载 `multi-user.target`。在本示例中，`graphical.target` 处于激活状态。

## 切换到不同的 target

有时，我需要在主机运行期间更改正在运行的 target。这并不会改变默认的 target，系统在下次重启时仍将启动默认 target。

第 3 章 使用 systemd 理解 Linux 启动

## 实验 3-3：更改 target

使用 `isolate` 命令可以轻松切换到 `multi-user.target`。对于这个子命令来说，这个词似乎很奇怪，但我们就是这么用的。

```
# systemctl isolate multi-user.target
```

显示内容现在应该从 GUI 桌面或登录屏幕变为虚拟控制台。登录并列出当前激活的系统单元，以验证 `graphical.target` 已不再运行：

```
# systemctl list-units --type target
```

确保使用 `runlevel` 命令来验证它是否同时显示了之前和当前的“运行级别”:

```
# runlevel
```

5 3

你仍然可以使用 `init` 命令来更改“运行级别”。

## 更改默认 target

现在，将默认 target 更改为 `multi-user.target`，这样它将始终进入控制台命令行界面，而不是 GUI 桌面界面。

第 3 章 使用 systemd 理解 Linux 启动

## 实验 3-4：更改默认 target

作为测试主机的 root 用户，切换到维护 systemd 配置的目录并进行快速列出：

```
# cd /etc/systemd/system/ ; ll
```

```
total 60

lrwx-rwx. 1 root 9 Jun 10 13:58 abtrd.service -> /dev/null

lrwx-rwx. 1 root 9 Jun 10 13:58 abrt-journal-core.service -> /dev/null

lrwx-rwx. 1 root 9 Jun 10 13:58 abrt-oops.service -> /dev/null

lrwx-rwx. 1 root 9 Jun 10 13:58 abrt-xorg.service

```

```
-> /dev/null
<SNIP>

lrwx-rwx. 1 root root 400 Jun 10 11:26 default.target -> /usr/lib/systemd/graphical.target

drwxr-xr-x. 2 root root 4096 Apr 14 2024 'dev-virtio%2dports-org.qemu.guest_agent.0.device.wants'

lrwx-rwx. 1 root root 390 Jun 19 14:00 display-manager.service -> /usr/lib/systemd/lightdm.service

drwxr-xr-x. 2 root root 4096 Apr 14 2024 getty.target.wants

drwxr-xr-x. 2 root root 4096 Aug 24 09:20 graphical.target.wants

drwxr-xr-x. 2 root root 4096 Aug 27 08:13 multi-user.target.wants

drwxr-xr-x. 2 root root 4096 Apr 14 2024 network-online.target.wants

drwxr-xr-x. 2 root root 4096 Apr 14 2024 remote-fs.target.wants

第 3 章 使用 systemd 理解 Linux 启动

drwxr-xr-x. 2 root root 4096 Apr 14 2024 sockets.target.wants

drwxr-xr-x. 2 root root 4096 Jun 10 13:46 sysinit.target.wants evendrwxr-xr-x. 2 root root 4096 Jun 10 13:57 sysstat.service.wants

drwxr-xr-x. 2 root root 4096 Apr 14 2024 systemd-homed.service.wants

drwxr-xr-x. 2 root root 4096 Apr 14 2024 systemd-journald.service.wants

drwxr-xr-x. 2 root root 4096 Apr 14 2024 timers.target.wants

drwxr-xr-x. 2 root root 4096 Aug 24 09:21 user.service.wants
```

7. 为什么你可能在 `rescue.target` 中使用计算机？

8. 为什么你可能在 `multi-user.target` 中运行计算机？

85

# 第 4 章
# 如何使用 systemd 管理启动

## 目标
在本章中，你将学习：
- `systemd` 如何确定服务的启动顺序，尽管它是一个高度并行的系统
- 使用 `systemd` 工具创建一个新的 `systemd` 单元（unit），以便在启动时运行一个简单的程序
- 使用启动消息查看程序和服务单元所添加的文本
- 使用 `journalctl` 查看新服务单元启动和结束时创建的消息以及程序的输出
- 配置服务单元，使其在 Linux `systemd` 启动的特定阶段启动

> © 版所有 David Booth 2025

87
D. Both, systemd for Linux SysAdmins, https://doi.org/10.1007/979-8-8688-1328-3_4

第 4 章 如何使用 systemd 管理启动

## 概述
在最近设置一个新 Linux 系统时，我想知道如何确保服务和其他单元的依赖项在这些依赖服务和服务单元启动之前已经运行。具体而言，我需要更多关于 `systemd` 如何管理启动序列的知识，特别是在一个本质上并行的系统中确定服务启动顺序的方法。

你可能知道 SystemV 通过为脚本命名 `SX` 前缀来排列启动顺序，其中 XX 是 00 到 99 之间的数字。然后 SystemV 使用按名称排序的 Linux 排序，为所需的运行级别按字母数字顺序运行每个启动脚本。

但 `systemd` 单元文件可以由系统管理员创建或修改，用于定义不仅用于初始化而且还用于常规操作的子程序。我们将创建一个服务单元文件，该文件将在启动时运行一个简单的测试程序。你还可以更改单元文件中的某些配置设置，并使用系统日志（journal）查看你的更改在启动序列中的位置。

## 准备
确保你已从 `/etc/default/grub` 文件的 `GRUB_CMDLINE_LINUX=` 行中删除了 `rhgb` 和 `quiet`，我们在实验 3-1 中做的那样。这将使你能够观察 Linux 启动消息流，你在本章的一些实验中将需要它。

此外，确保 SELinux 不会阻止我们创建的 shell 脚本运行。验证当前的 SELinux 状态，以便在在本章结束时恢复该状态。

```bash
## sestatus
SELinux status: enabled
SELinux mount: /sys/fs/selinux
```

88

第 4 章 如何使用 systemd 管理启动

SELinux root directory: `/etc/selinux`

Loaded policy name: targeted

Current mode: enforcing

```

来自配置文件的模式: enforcing
Policy MLS status: enabled
Policy deny_unknown status: allowed
Memory protection checking: actual (secure)
Max kernel policy version: 33

如果 SELinux 处于 enforcing（强制执行）模式，请运行以下命令将 SELinux 设置为 permissive（许可）模式：

```bash
## setenforce Permissive
```

## 程序
在实验中，你将创建一个简单的程序，使你能够在控制台启动期间查看消息，稍后在 systemd 日志中查看。

## 实验 4-1：创建程序
创建 shell 程序 `/usr/local/bin/hello.sh` 并添加以下内容。你希望确保这个小程序产生的输出在启动期间是可见的，这样你在查阅 systemd 日志时就能轻松找到它。你将使用带有一些线条的“hello world”程序版本；以便它脱颖而出。确保该文件是可执行的，并且由 root 用户和组所有，具有 700 权限以确保安全。

```bash
#!/usr/bin/bash
# 用于测试带有 systemd 启动配置的简单程序。
# 版权所有 David Both, 2025
```

89

```
第 4 章 如何使用 systemd 管理启动
# GNU 全局许可许可证：
```

```bash
# 允许在任何介质中复制和分发此文件，
# 无论是否修改，都无需支付特许费，
# 只要保留了版权声明和本声明即可。
```

```bash
# 本文件按原样提供，不作任何担保。
echo "#####################################"
echo "########### Hello World! #######"
echo "#######################################"
# 从命令行运行此程序以验证其是否工作正常。
```

### hello.sh

```bash
####################################
###### Hello World! #######
################################
```
从命令行运行此程序以验证其是否工作正常。

```bash
####################################
###### Hello World! #######
################################
```
此程序可以使用任何脚本语言创建。将其放置在 `/usr/local/bin` 中，这样当你输入它时就可以从命令行轻松运行。

## 服务单元
在我们创建服务单元之前，让我们探索什么是服务单元以及它如何与获取（getting）相关。
90
第 4 章 如何使用 systemd 管理启动
一个单元是“服务、设备、挂载点、目标、套接字、定时器、资源管理切（slice）或进程组”——`systemd.unit` 页面。

单元文件是一个纯文本的 ini 格式文件，包含定义单元的数据。它定义了正在创建的单元类型、如何使用它、它运行的程序以及它所属的 systemd 目标。

共有八种服务类型，你可以在 `systemd-service(5)` 手册页中找到每种类型（以及单元文件的其他部分）的解释。系统管理员在创建用于本地使用的新服务单元时通常使用这些类型。我最常用的类型是 `simple`、`oneshot` 和 `dbus`。我们将在书中探讨每种类型。我们已经在第 3 章看过了 `oneshot` 类型。

表 4-1 列出了所有服务类型及其要说明。

91
第 4 章 如何使用 systemd 管理启动

## 表 4-1 systemd 服务的八类型

| 服务类型 | 说明 |
| :--- | :--- |
| simple | 这是默认类型。systemd 假设在程序开始执行后立即启动。这通常是程序的主进程。 |
| exec | 与 simple 类似，systemd 在主二进制文件执行后立即认为单元已启动。它会将后续单元的启动推迟到该点。注意，这意味着当服务的二进制文件无法成功调用时，`systemctl start` 命令会报告失败。 |
| forking | systemd 在由派生的二进制文件退出后立即认为单元已启动。不建议使用这种类型；请改用 notify-reload 或 dbus。 |
| oneshot | 与 simple 类似；但服务管理器在主进程退出后会认为单元已就绪。然后它会启动后续单元。 |
| dbus | 与 simple 类似；但此类类型的单元必须指定 `Busname=`，并且服务管理器在获取指定的总线名称后认为单元已就绪。 |
| notify | 与 exec 类似；然而，预计服务在完成启动后通过 `sd_notify(3)` 或等效调用发送“ready=1”通知消息。systemd 在发送此通知消息后将继续启动后续单元。 |
| notify- | 与 notify 类似，但有一个不同点：当请求服务重载（reload）时，会向服务的主进程发送 `Sighup` 进程信号，管理器将等待有关重载完成的通知。 |
| idle | 与 simple 类似；但服务程序的实际执行被推迟到所有活动作业都分发之后。这可以用于避免 shell 服务的输出与状态输出交织。 |

111
(继续)

92
第 4 章 如何使用 systemd 管理启动

## 表 4-1. (继续)

在控制台上。请注意，这种类型仅用于改进控制台输出；作为通用的单元排序工具它并不有用。你可以在章末的资源中找到更多信息。

## 创建服务单元 (Service Unit)

服务单元文件使用标准 ini 文件的格式和结构。命令以井号 (`#`) 开头，节名称包含在方括号 `[]` 中。我们的单元文件是最简单的形式，包含三个部分：

- `[Unit]`: 这是单元的简短描述，作为系统管理员（SysAdmins）的标识符。它将出现在该服务的 systemd 状态报告中。
- `[Service]`: 定义单元类型为服务，并提供服务类型（在本例中为 `oneshot`）以及要运行程序的完全限定路径。
- `[Install]`: 指定将触发服务单元的目标单元。`oneshot` 用于此类服务：由单元文件启动的程序是主进程，且必须在 systemd 启动任何依赖进程之前完成。我们没有任何需要等待此单元完成的依赖进程。

## 实验 4-2：创建服务单元

创建服务单元文件 `/usr/local/lib/systemd/system/hello.service`，内容如下。这是 Linux 文件系统层次结构标准 [1] 显式指定的用于本地创建系统文件的位置。systemd 会检查此目录下的这些本地文件。

此文件不需要具有执行权限，但出于安全考虑，它需要 root 用户和组的所有权以及 754 权限。

```
# 用于测试的简单服务单元文件
# 使用 systemd 的启动配置。
# Copyright David Both, 2025
# GNU All-Permissive License:
# 允许在任何媒介上复制和分发此文件，无论经过何修改，均无需支付特许费，前提是必须保留版权声明和本通知。
# 本文件按原样提供，不作任何保证。
#
# 1 Both, David, The Linux Philosophy for SysAdmins, Tenet 04 — Use the Linux FHS,
https://www.both.org/?p=6982
[Unit]
Description=My hello shell script
[Service]
Type=oneshot
ExecStart=/usr/local/bin/hello.sh
[Install]
WantedBy=multi-user.target
```
