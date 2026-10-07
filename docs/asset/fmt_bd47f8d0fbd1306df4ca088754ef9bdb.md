
就像项目管理中的关键路径一样，关键链显示了启动期间发生的关键敏感型事件链。如果启动缓慢，这些就是你想要关注的 `systemd` 单元——它们是导致延迟的原因。此工具不会显示所有已启动的单元，仅显示此关键事件链中的单元。

在支持颜色的终端上（今天大多数终端模拟器都支持），导致延迟的单元将用红色高亮。

## 实验 15-3：确定关键链

我已经在我的两个物理主机和我的学生 VM 主机上使用了这个工具，因此我们可以对它们进行比较。第一个来自我的主工作站。

```
$ systemd-analyze critical-chain
```

单元变为活动或启动的时间在 `@` 字符之后打印。单元启动所需在 `+` 字符之后打印。

`graphical.user.target` @8.850s

`multi-user.target` @8.849s

`vboxweb-user.service` @8.799s

`network-online.target` @8.776s

`NetworkManager-wait-online.service` @8.732s

`NetworkManager.service` @8.468s

`network-pre.target` @8.438s

`systemd-journal-service.service` @8.409s

`basic.target` @8.367s

`dbus-broker.service` @8.348s

`systemd-binfmt.service` @8.314s

`systemd-tmpfiles-setup.service` @8.290s

`systemd-fck.service` @8.071s

`var.mount` @7.960s

在这个例子中，`vboxdrv.service` 和 `vboxweb-service` 都花费了相当长的启动时间。下一个例子是另一个虚拟机。将此输出与你自己的进行对比，看看差异有多大。

```
service @16.265s +272ms
└systemd-journal-flush.service
@13.764s +2.493s
└var.mount
@13.013s +593ms
└systemd-fsck@dev-mapper-fedora_studentvm1-x2var.service
@11.077s +1.885s
└local-fs-pre.target @11.056s
└lvm2-monitor.service
@5.803s +5.252s
└dm-event.socket
@5.749s
└system.slice
└.slice
```

我对这里长长的依赖链感到惊讶，但这可能可能是因为没有某个像 VirtualBox 那样耗费大量时间的单一服务并隐藏了其他服务，从而将它们从关键链中移除了。

# 第 15 章：分析 systemd 启动与配置

## 系统状态

你有时可能需要确定系统的当前状态。`systemd-analyze dump` 命令会输出大量关于当前系统状态的数据。

### 实验 15-4：分析系统状态

该命令从主启动时间戳列表以及每个 `systemd` 单元列表以及每个单元状态的完整描述开始。

```bash
$ systemd-analyze dump
```

`Manager: systemd 253 (253.2-1-fc38)`

`Features: +PAM +AUDIT +SELINUX -APPARMOR +IMA +SMACK +SECCOMP`

`-GCRYPT +GNUTLS +OPENSSL +ACL +BLKID +CURL +ELFUTILS +FIDO`

`+ID2 -IDN ->`

`Timestamp firmware: 1min 557.292ms`

`Timestamp loader: 6.606226s`

`Timestamp kernel: Sun 2023-04-30 17:09:49 EDT`

`Timestamp initrd: Sun 2023-04-30 17:09:51 EDT`

`Timestamp userspace: Sun 2023-04-30 17:09:57 EDT`

`Timestamp finish: Sun 2023-04-30 21:10:06 EDT`

`Timestamp security-start: Sun 2023-04-30 17:09:57 EDT`

`Timestamp security-finish: Sun 2023-04-30 17:09:57 EDT`

`Timestamp generators-start: Sun 2023-04-30 21:09:57 EDT`

`Timestamp generators-finish: Sun 2023-04-30 21:09:57 EDT`

`Timestamp units-load-start: Sun 2023-04-30 21:09:57 EDT`

`Timestamp units-load-finish: Sun 2023-04-30 21:09:58 EDT`

`Timestamp units-load: Tue 2023-05-02 13:30:41 EDT`

`Timestamp initrd-security-start: Sun 2023-04-30 17:09:51 EDT`

`Timestamp initrd-security-finish: Sun 2023-04-30 17:09:51 EDT`

`Timestamp initrd-generators-start: Sun 2023-04-30 17:09:51 EDT`

`Timestamp initrd-generators-finish: Sun 2023-04-30 17:09:51 EDT`

`Timestamp initrd-units-load-start: Sun 2023-04-30 17:09:51 EDT`

`Timestamp initrd-units-load-finish: Sun 2023-04-30 17:09:51 EDT`

`-> Unit logwatch.service:`

`Description: Log分析和报告器`

`Instance: n/a`

`Unit Load State: loaded`

`Unit Active State: inactive`

`State Change Timestamp: Wed 2023-05-03 00:00:20 EDT`

`Inactive Exit Timestamp: Wed 2023-05-03 00:00:05 EDT`

`Active Enter Timestamp: n/a`

`Active Exit Timestamp: n/a`

`<SNIP - 除了数百万行输出>`

在我的主工作站上，这个命令生成了 59,859 行内容和约 1.75MB 数据。这个命令运行非常快，所以你不需要等待。

```bash
$ systemd-analyze --dump
```

`Manager systemd 256.12 (256.12-1-fc41)`

`Features: +PAM+AUDIT+SELINUX -APARMOR +IMA +SMACK +SECCMP`

`-GCRYPT+GNUTLS+OPENSSL +ACL+BLKID+CURL +ELFUTILS+FIDO>`

`Timestamp uspace: Fri 2025-03-14 09:48:17 EDT`

`Timestamp finish: Fri 2025-03-14 09:48:17 EDT`

`Timestamp generators-start: Fri 2025-03-14 09:48:17 EDT`

`Timestamp generators-finish: Fri 2025-03-14 09:48:17 EDT`

`Timestamp units-load-start: Fri 2025-03-14 09:48:17 EDT`

`Timestamp units-load-finish: Fri 2025-03-14 09:48:17 EDT`

`Timestamp units-load: Sat 2025-03-15 14:37:50 EDT`

`-> Unit blockdev@dev-mapper-vg01-usr.target:`

`Description: blockdev@dev-mapper-vg01-usr.target`

`Instance: dev-mapper-vg01-usr.target`

`Unit Load State: not-found`

`Unit Active State: inactive`

`State Change Timestamp: Fri 2025-03-14 09:48:22 EDT`

`Inactive Exit Timestamp: n/a`

`Active Enter Timestamp: n/a`

`Active Exit Timestamp: n/a`

`Inactive Enter Timestamp: n/a`

`GC: yes`

`Daemon Reload: no`

`Transient: no`

`Garbage Collection Mode: inactive`

`Before: usr.mount (target)`

`ReferencedBy: usr.mount (target)`

`-> Unit background.slice:`

`Description: 用户后台切片`

`Instance: n/a`

`Unit Load State: loaded`

`Unit Active State: active`

`State Change Timestamp: Fri 2025-03-14 09:48:22 EDT`

`Inactive Exit Timestamp: Fri 2025-03-14 09:48:22 EDT`

`Active Enter Timestamp: Fri 2025-03-14 09:48:22 EDT`

`Active Exit Timestamp: n/a`

`Inactive Enter Timestamp: n/a`

`<SNIP>`

花点时间探索一下这些命令提供的数据。我在这里发现了很多有趣的信息。

## 分析图表

大多数人认为精美的图表易于阅读，并且比基于文本的性能数据更容易理解。`systemd-analyze` 提供了以 `*.svg` 矢量图表显示启动和启动数据的能力。

### 实验 15-5：创建分析图表

下面的命令生成一个矢量图形文件，显示启动和启动期间的位置。生成该文件需要几秒钟。

```bash
$ systemd-analyze plot > /tmp/bootup.svg
```

该命令生成的矢量图形文件显示了启动和启动期间的位置。生成该文件需要几秒钟。

上述命令生成的 `svg` 文件是一个文本文件，定义了一系列可以使用许多应用程序（如 `image Viewer`、`ristretto`、`okular`、`libreoffice draw` 等）生成图形的矢量。我使用了 `libreoffice draw` 来渲染这张图。图表很大，你需要大幅放大才能看清细节。图 15-1 显示了图表的一小部分。

#### 图 15-1 在 LibreOffice Draw 中显示的 bootop.svg

`bootop` 序列位于图中零 `0` 点左侧，而启动序列位于右侧。这小部分显示了由 `initrd` 启动的内核和 `initrd` 进程。这张图一眼就能启动了什么、花了多久以及主要的依赖关系，关键路径用红色突出。

另一个生成图形输出的命令是 `systemd-analyze plot`，它以 `dot` 格式生成文本密度图。生成的数据流通过 `dot` 工具处理，该工具是一系列从各种类型数据生成矢量图形程序的一部分。生成的 `svg` 文件可以使用之前提到的 `svg` 工具查看。

首先，生成文件。这在我的主工作站上花费了近九分钟。

```bash
$ time systemd-analyze dot | dot -Tsvg > /tmp/test.svg
```

| 颜色图例 | 含义 |
| :--- | :--- |
| 黑色 | Requires |
| 深蓝色 | Requisite |
| 深灰色 | Wants |
| 红色 | Conflicts |
| 绿色 | After |

`real 8m37.544s`

`user 8m35.375s`

`sys 0m0.070s`

`[root@david ~]#` 我不会在这里重现生成的图表，因为看起来就像一团乱麻。但你绝对应该尝试尝试并查看结果以理解我的意思。

### 条件判断

在阅读 `systemd-analyze(1)` 的手册页时，我发现的一个非常有趣且通用的功能之一是 `condition` 子命令。这个 `condition` 子命令可以用于测试 `systemd` 单元文件中使用的各种条件和断言。

### 列出配置文件

我经常发现查看 `systemd` 单元和配置的内容很有用。`systemd-analyze` 工具为我们提供了一种将各种配置文件的内容发送到 `STDOUT` 的方法。

让我们开始查看显示管理器服务。可以使用 `cat-config` 子命令执行此操作。该命令的基础目录是 `/etc/`。

```
[root@david ~]# systemd-analyze cat-config systemd/system/
display-manager.service
```

```
# /etc/systemd/system/display-manager.service
[Unit]
Description=LXDM (Lightweight X11 Display Manager)
#Documentation=man:lxd(8)
Conflicts=getty@tty1.service
After=systemd-user-sessions.service getty@tty1.service
plymouth-quit.service lifesys-late.service
#Conflicts=plymouth-quit.service
[Service]
ExecStart=/usr/bin/lxdm
Restart=always
IgnoreSIGPIPE=no
#BusName=org.freedesktop.lxdm
```

```
[Install]
Alias=display-manager.service
```

```
[root@david ~]#
```

我发现，为了实现比标准 `cat` 命令多一点点的功能，需要输入大量的字符。

然而，它确实能够带有语法颜色地渲染数据流，使得文件更易读。`cat` 命令并做不到这一点。

我发现另一个有用的语法命令是这一个。它至少可以在标准的 `systemd` 目录下搜索符合指定模式的文件。

## 第 15 章：分析 systemd 启动与配置

```bash
$ systemctl cat basic*
# /usr/lib/systemd/system/basic.target
# SPDX-License-Identifier: LGPL-2.1-or-later
#
```

```
# This file is part of systemd
#
# systemd is free software; you can redistribute it and/or
# modify it
# under the terms of the GNU Lesser General Public License
as published by
# The Free Software Foundation; either version 2.1 of the
License, or
# (at your option) any later version.
[Unit]
Description=Basic System
Documentation=man:systemd.special(7)
Requires=sockets.target timers.target paths.target slices.target
Wants=sysinit.target
After=sysinit.target sockets.target paths.target slices.
target tmp.mount
# We support /var, /tmp, /var/tmp, being on NFS, but we we
# don't pull in
# remote-fs.target by default, hence pull them in explicitly
here. Note that we
# require /var and /var/tmp, but only add a Wants= type
dependency on /tmp, as
# we support that unit being masked, and this should not be
considered an error.
RequiresMountsFor=/var /var/tmp
Wants=tmp.mount
```

第 15 章：分析 `systemd` 启动与配置。

这两个命令都会在每个文件的内容前加上注释行，其中包含文件的完整路径和名称。

### 单元文件验证

在创建一个新的单元文件后，验证其至少在语法上是正确的是有帮助的。这就是 `verify` 子命令所的工作。它可以列出拼写错误的指令，并指出缺失的服务单元。

### 实验 15-8：验证 systemd 单元文件

`backup.service` 单元是被创建的单元，因此它在你的系统中不存在。目前，只需知道该命令按预期工作工作即可。

```
# systemd-analyze verify /etc/systemd/system/backup.service
```

遵循 Linux 哲学的原则“沉默是金”，没有输出消息意味着意味着扫描的文件没有错误。

### 安全性

`security` 子命令检查指定服务的安全级别。

它只作用于服务单元，而不作用于其他类型的单元文件。让我们检查 `NetworkManager` 服务单元吧。

### 实验 15-9：安全检查
