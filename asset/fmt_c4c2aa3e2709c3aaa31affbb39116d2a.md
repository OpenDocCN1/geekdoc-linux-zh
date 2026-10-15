
| 动作 | 描述 |
|---|---|
| `ondemand` | 仅在运行级别为 `a`、`b` 或 `c` 时有效。当使用 `init` 调用这三个按需运行级别之一时，就会运行进程。通常不使用。 |
| `initdefault` | 设置系统的默认运行级别。忽略进程字段。 |
| `sysinit` | 进程在系统启动期间运行一次。`sysinit` 动作优先于 `boot` 或 `bootwait` 动作。 |
| `powerwait` | 当 `init` 接收到 `SIGPWR` 信号时运行进程。通常 UPS 监控软件检测到电源问题并发出此类信号，在这种情况下 `init` 将等待直到进程终止。 |
| `powerfail` | 与 `powerwait` 相同，但 `init` 不等待进程完成。 |
| `powerokwait` | 当 `init` 接收到 `SIGPWR` 信号且名为 `/etc/powerstatus` 的文本文件包含 `"OK"` 字符串时运行进程。通常，UPS 监控程序会创建此文件并向 `init` 发送 `SIGPWR` 信号表示电源问题已修复。 |
| `ctrlaltdel` | 当 `init` 接收到 `SIGINT` 信号时运行进程。 |
| `kbrequest` | 当 `init` 接收到来自键盘处理程序的 `KeyboardSignal` 时运行进程。 |

System V 风格的 `init`（Red Hat Linux `init` 采用的这种）使用以下目录结构：

```
/etc
+init.d (dir)
+rc0.d (dir)
+rc1.d (dir)
+rc2.d (dir)
+rc3.d (dir)
+rc4.d (dir)
+rc5.d (dir)
+rc6.d (dir)
+rc.sysinit (script)
+rc.local (可选脚本，由 Red Hat Linux 提供)
+rc.serial (可选脚本)
+rc (script)
```

# `/etc/rc.d/rc.sysinit` 脚本

如你所知，当 Red Hat Linux 系统启动时，内核运行 `init`，`init` 随后在处理目标运行级别的任何其他脚本之前，运行 `/etc/rc.d/rc.sysinit` 脚本。它在其他任何内容之前运行此脚本，是因为 `/etc/inittab` 文件中有以下这一行：

```
si::sysinit:/etc/rc.d/rc.sysinit
```

注意，运行级别字段为空，因为 `init` 将 `sysinit` 识别为系统初始化动作。`rc.sysinit` 脚本执行许多操作，包括设置主机名、启用交换分区、检查文件系统、加载内核模块等。通常，你不需要修改此脚本。

## `/etc/rc.d/init.d` 目录

`init.d` 子目录用于存储所有运行级别所需的脚本。将所有脚本保持在一个位置使其更容易管理。每个脚本都用于启动/停止特定的服务——例如域名系统 (`DNS`)、Web 服务或类似服务。所有这些脚本都遵循一种特殊的命令行参数。例如，要启动 NFS（网络文件系统）服务，你可以运行以下脚本：

```
/etc/rc.d/init.d/nfs start
```

要停止同一服务，你可以如下所示运行相同的脚本：

```
/etc/rc.d/init.d/nfs stop
```

如你所见，`nfs` 脚本接受 `start` 和 `stop` 作为参数。此目录中的所有脚本都是如此，它们通过符号链接到 `rc[0-6].d`。

## `/etc/rc.d/rc` 脚本

当 `init` 被要求将运行级别更改为七种可能的级别之一时，它会运行 `/etc/inittab` 文件中以下行之一指定的脚本：

```
0:wait:/rc.d/rc
1:wait:/rc.d/rc
2:wait:/rc.d/rc
3:wait:/rc.d/rc
4:wait:/rc.d/rc
5:wait:/rc.d/rc
6:wait:/rc.d/rc
```

# 第 3 章：启动和关闭过程

```bash
#!/bin/bash
# 脚本逻辑翻译：
# 此脚本主要处理运行级别切换时的服务启动与停止。
# ... (逻辑省略)
```

此脚本主要执行以下操作：

1. 检查是否存在对应指定运行级别的子目录。
2. 停止当前运行级别下的服务（运行 `K` 脚本）。
3. 启动新运行级别下的服务（运行 `S` 脚本）。

## 第二部分：作为超级用户工作

```
lrwx-xrwx root root 15 S50crond -> ..init.d/crond
lrwx-xrwx root root 14 S550inet -> ..init.d/inet
lrwx-xrwx root root 15 S555named -> ..init.d/named
lrwx-xrwx root root 13 S60lpd -> ..init.d/lpd
lrwx-xrwx root root 13 S560nfs -> ..init.d/nfs
lrwx-xrwx root root 18 S575keytable -> ..init.d/keytable
lrwx-xrwx root root 18 S580sendmail -> ..init.d/sendmail
lrwx-xrwx root root 13 S591smb -> ..init.d/smb
lrwx-xrwx root root 19 S591linuxconf -> ..init.d/linuxconf
lrwx-xrwx root root 11 S591local -> ..rc.d/local
```

注意，来自 `/etc/rc.d/init.d` 目录的脚本通过两种方式链接。某些脚本的链接方式如下：

- `K`(两位数字)[脚本名称]

其他脚本的链接方式如下：

- `S`(两位数字)[脚本名称]

所有以字母 `"K"` 开头的脚本都会带有 `"stop"` 参数运行，而另一种类型则带有 `"start"` 参数运行。两位数字用于设置执行顺序。因此，名为 `S01foo` 的脚本将在 `S10bar` 之前运行。这些 `"S"` 和 `"K"` 脚本由 `/etc/rc.d/rc` 脚本执行。

一旦 `rc` 脚本执行完毕，`init` 的处理也随之结束，系统在新的运行级别下变得可用。

## `/etc/rc.d/rc.local` 脚本

`rc.local` 脚本通常在运行级别 2、3 和 5 结束时运行一次。你可以在此文件中添加任何需要在每次启动时仅需运行一次的内容。

## `/etc/rc.d/rc.serial` 脚本

`rc.serial` 脚本通常在运行级别 1 或 3 结束时运行一次，以初始化串口。

现在让我们看看在系统启动时 `init` 做了什么。

## 启动你的系统

在启动过程中，`init` 首先会运行 `rc.sysinit` 脚本，然后运行默认运行级别的脚本。默认运行级别在 `/etc/inittab` 中设置，使用类似下面的一行：

```
id:3:initdefault:
```

默认运行级别被设置为 3。这意味着 `init` 将运行将系统置于多用户模式所需的脚本。

如果你再次查看列表 3-2，你会发现以下内容指定了在运行级别 3 下需要运行的项。

```
13:3:wait:/etc/rc.d/rc 3
```

`rc` 脚本带有参数 `3` 运行。正如之前提到的，此脚本将运行 `/etc/rc.d/rc3` 目录下所有名称以 `"S"` 开头的脚本。它还将为每个带有 `"S"` 前缀的脚本提供 `"start"` 作为参数。当所有 `"S"` 脚本都运行完毕后，`rc` 脚本将结束，系统将在默认运行级别下变得可用。

![](img/cbfef09f620ba4100baa62876f6f02b1_92_0.png)

> 在 LILO 提示符处可以覆盖默认运行级别。例如，如果你想以单用户模式启动系统，可以指定 `linux single` 以单用户模式启动。如果你使用 `"linux"` 以外的标签启动 Linux，你必须指定 `yourlabel single`，其中 `yourlabel` 是相应的标签。

现在让我们看看 `init` 在关机事件期间是如何工作的。

## 关闭你的系统

你可以手动运行 `init` 并通过命令行提供所需的运行级别来让它更改级别。例如：

```
init 1
```

这将告诉 `init` 将级别改为 1。换句话说，这将停止系统。如果你在多用户模式（运行级别 3）下运行，上述命令并不理想，因为它不会通知系统用户系统将要停止。

通常使用 `shutdown` 命令来关闭系统。它向所有登录的用户广播系统正在更改级别的警告消息。它还提供了一个调度关机事件的选项。`shutdown` 命令通过告诉 `init` 将系统的当前运行级别改为停止 (`0`) 或重启 (`6`) 来工作。例如：

```
shutdown -h now
```

此命令将立即信号 `init` 将运行级别改为 0。

## 取消关机

`shutdown` 命令允许你在稍后时间调度关机事件。例如：

```
shutdown +10
```

在 shell 提示符输入命令将在 10 分钟后关机。现在可能需要取消关机事件；在这种情况下，可以使用带有 `-c` 的命令。例如：

```
shutdown -c
```
