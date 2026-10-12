
如果发生这种情况，您可能存在以下问题之一：
- 您没有正确配置生产内核，`Kdump` 将无法工作。您将必须重新通过安装过程，包括使用相关参数编译内核。
- 您使用的 `Kexec` 版本与内核-`kdump`-`kexec-tools` 不匹配。请确保选择了正确的包。您可能在配置文件的 `KEXEC_OPTIONS` 下缺少了 `--args-linux`。

一旦成功解决此问题，您将能够继续测试。

## KDUMP 网络转储功能

能够将内核崩溃转储发送到网络存储使得 `Kdump` 在大型环境的部署中极具吸引力。它允许系统管理员规避本地磁盘空间限制。与 `LCDKD` 相比，`Kdump` 具有更好的网络感知能力；它不受限于在同一子网内转储，不需要专用服务器。您可以使用 `NFS` 区域或 `CIFS` 共享作为存档目标。最好的是，更改仅影响客户端。没有服务器端配置。

配置文件

为了让 `Kdump` 将崩溃转储发送到网络存储，只需要更改配置文件中的两个指令即可使整个过程工作。其他的设置与本地磁盘功能保持一致，包括在启动时启动 `Kdump`、添加 `GRUB` 菜单以及 `Kexec` 测试。
配置文件位于 `/etc/sysconfig/kdump`。一如既往，在进行更改之前，请备份该配置文件。

## 配置 KDUMP_RUNLEVEL

要使用网络功能，我们需要配置 `Kdump` 在 `runlevel` 3 下启动。默认情况下使用 `runlevel` 1。通过更改默认值来实现网络功能。

```
KDUMP_RUNLEVEL=3
```

## 配置 KDUMP_SAVEDIR

第二步是配置网络存储目标地。我们不能再使用本地文件了。我们需要使用 `NFS` 区域、`CIFS` 共享、`SSH` 服务器或 `FTP` 服务器。在本文中，我们将配置一个 `NFS` 区域，因为这似乎是发送崩溃转储（`crash dumps`）最合理的选择。另外两个项的配置非常相似，而且同样简单。你只需要注意的是符号表示。你需要使用正确的语法：

```
KDUMP_SAVEDIR="nfs://<server>://<dir>"
```

`<server>` 指的是 `NFS` 服务器，可以使用名称或 IP 地址。如果你使用名称，则需要在环境中具备某种名称解析机制，例如 `hosts` 或 `DNS`。`<dir>` 是 `NFS` 服务器上导出的 `NFS` 目录。该目录必须对 `root` 用户可写。在我们的示例中，指令形式如下：

```
KDUMP_SAVEDIR="nfs://server2:/dumps"
```

以上就是为了内核崩溃时让 `Kdump` 将内存转储发送到 `NFS` 存储区域的两个更改。现在，我们将测试该功能。

## KDUMP 使用

现在我们将模拟一次内核崩溃，以检查我们的配置并确保一切正常工作。

## 收集内核核心 (Kdump) 161

## 模拟内核崩溃

要手动崩溃内核，如果系统中尚未启用，你需要启用系统请求（`SysRq`）功能（也称为魔术键），然后触发内核恐慌（`kernel panic`）。因此，首先启用 `SysRq`：

```
echo 1 > /proc/sys/kernel/sysrq
```

然后，崩溃内核：

```
echo c > /proc/sys/sysrq-trigger
```

现在观察控制台。内核崩溃后将启动。过了一会儿，你应该看到 `Kdump` 正在运行。查看控制台。过了一会儿，会出现一个小的计数器，显示转储过程的进度。这意味着你可能已经正确配置了 `Kdump` 并且它按预期工作。等待转储完成。转储完成后，系统应该重启到生产内核。诚地，检查目标目录，你应该能看到 `vmcore` 文件。内存核心转储的过程如图 6.1 和 6.2 所示。

这结束了 `Kdump` 长期而彻底的配置和测试。如果你已经成功管理了目前的所有阶段，那么你的系统就可以准备好投入生产，并在发生内核恐慌时收集内存核心。

Loading kymap i386:query_us.map.gz done
Loading compose table winkys shiftctrl_latin1.add done
Start Unicode mode done
Loading console format lat9u-16.psfu -n trivial GB:loadable done
---------------------------------------------------------------------- 0 MB of 8128 MB (0.0%)

图 6.1 正在进行内核内存转储

Start Unicode mode done
Loading console format lat9u-16.psfu -n trivial GB:loadable done
###################################################################### 8128 MB of 8128 MB (100.0%)
d
LIMIT: Switching to runlevel: 6
LIMIT: Sending processes the TERM signal done
Master Resource Control: runlevel 3 has been reached

图 6.2 内核内存转储完成

分析核心将为你提供宝贵的信息，希望这帮助你找到并解决导致系统崩溃的根源。

## 总结

`Kdump` 是一个强大且灵活的内核崩溃导出工具。在运行的生产内核上下文中执行崩溃内核的能力是一个非常有用的机制。同样，在几乎所有运行（包括网络）中使用崩溃内核的能力，以及使用各种协议将核心发送到网络存储的能力，显著扩展了我们控制环境的能力。

具体来说，与旧的 `LKCD` 工具相比，它在所有层面上提供了功能，包括更健壮的机制和更好的扩展性。如果需要，`Kdump` 可以使用本地 `RAID` (`md`) 设备。此外，它改进了网络感知，并与包括 `NFS`、`CIFS`、`FTP` 和 `SSH` 在内的许多协议配合。内存核心不再受 32 位屏障。

## 崩溃分析 (CRASH)

内核崩溃分析是我们调查的下一步。在收集内存核心之后，我们现在需要处理它们。此项任务的标准工具是 `crash` (`Anderson, 2008`)，它基于 `SVR4 UNIX` 的 `crash` 命令，并通过与 `gdb` 工具合并进行了增强。我们现在将扩展其使用方法，看看它如何帮助我们进行故障排除。

## 前提条件

你必须正确配置并使 `Kdump` 工作正常。

### Crash 安装

可以在所有主流发行版（包括企业版）的仓库中找到 `crash`。

## 内存核心

内存核心被称为 `vmcore`，你会在 `crash` 目录内按日期命名的目录找到它们。在旧版本的 `Kdump` 中，目录只包含 `vmcore` 文件。新版本还会将内核和 `System map` 文件复制到目录中，使核心处理更加容易。

## 调用 crash

`crash` 工具有多种方式调用。首先，旧版本和新版本的 `Kdump` 在功能和处理核心的方式上存在差异。其次，`crash` 工具可以手动调用，也可以无人运行。

## 崩溃分析 (crash) 163

### 旧式调用（经典）

旧式调用方式如下：

```
crash <System map> <vmlinux>
```

版权所有，权利保留。

`<System map>` 是 `System map` 文件的绝对路径，通常位于 `/boot`。该文件必须与崩溃的内核版本匹配。`System map` 是内核的符号表，用于符号名称与地址之间的查找。符号名称可能是变量名或函数名。在调试内核恐慌和内核 `oops` 时它非常有用。
`<vmlinux>` 是收集内存时运行的未压缩内核。
`vmcore` 是内存转储。
`System map` 文件留在 `/boot`。
`.debug` 文件留在 `/boot`。

## 新式调用

新版本的 `Kdump` 可以处理压缩镜像。此外，它们会将 `System map` 复制到目录中，简化了 `crash` 的使用。根据你选择的发行版，语法可能不同：

```
crash /usr/lib/debug/<kernel>.debug
crash /usr/lib/debug/<kernel>/vmlinux
```

版权所有，权利保留。

### 可移植性使用

要在其他机器上处理核心，你可以复制 `System map` 和内核，或者只复制调试信息以及 `crash` 文件。调试信息必须与内核完全匹配，否则将获得 `CRC` 匹配错误，例如

# 第 6 章 变得很极客

```
crash: /usr/lib/debug/vmlinux-2.6.31-default.debug:
CRC 值不匹配
```

## 运行 crash

```
NOTE: stdin: not a tty
GNU gdb (GDB) 7.0
Copyright (C) 2009 Free Software Foundation, Inc.
License GPLv3+: GPL 公共许可证 3 或更高版本 <http://gnu.org/licenses/gpl.html>
这是自由软件：你可以自由更改和分发。
```
