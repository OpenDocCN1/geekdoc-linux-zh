
## 弹出窗口

- 除主显示窗口外的所有窗口均为次要或弹出窗口，它们提供关于所选网络、组或客户端的补充和放大信息，以及统计数据和额外有趣的信息。
- 无线网卡电量和网络位置弹出窗口上提供的信息完全取决于无线网卡驱动程序和/或固件。Kismet 不计算信号或噪声信息，而是简单地报告这些内容。

## 自定义面板界面

- 可以通过编辑 `kismet_ui.conf` 文件，根据用户的具体要求修改网络列表和客户端列表。
- 也可以修改 Kismet 的颜色方案，包括背景、边框以及网络的默认颜色编码。

## 第三方前端

- 第三方前端是为补充或替换 Kismet 客户端面板界面而设计的图形用户界面（GUI）。
- 第三方客户端可用于在 Linux 和 Windows 上运行。

## 配置 Kismet 服务器

### 本章解决方案：

- Kismet 配置文件
- Kismet.conf
- 总结

## 引言

Kismet 服务器主要由一个庞大且看似令人畏惧的配置文件控制。通常位于 `/usr/local/etc` 目录下的 `kismet.conf` 文件是您将花费大部分配置时间的地方。任何接触过配置文件的人都应该对此感到相当熟悉。对于 Kismet 初学者，甚至对于已经使用 Kismet 一段时间的高手来说，这都是一个未被充分挖掘的资源。很少有人会仔细检查可用的配置选项范围。Kismet 可以跟踪和记录大量信息，同时也支持对特定信息进行过滤和目标设定。了解可用的选项将有助于您以最适合自己需求的方式使用 Kismet。

## Kismet 配置文件

配置文件并不像看起来那么可怕。然而，它确实很大，因为作者 Dragorn 贴心地为各个选项保留了许多非常详尽的注释。有些部分相当直观，而有些则不然。本节将逐行（几乎）检查并解释每个部分。虽然注释很好，但有些领域允许进行注释中未指定的调整，一旦您开始深入挖掘配置文件，就能揭示出强大的功能。

## Kismet 参数

`kismet.conf` 配置文件可以直接使用您喜爱的 UNIX 文本编辑器（如 vi、pico、emacs）进行编辑，但请注意自动换行和 UNIX 文件格式。配置文件在运行时由服务器解析，并期望它是一个 UNIX 文本文件。DOS 和 UNIX 使用不同的控制字符来处理文本文件，因此在 UNIX 文本文件上使用 DOS 或 Windows 编辑器可能会更改文件格式，导致服务器无法读取该文件。一般来说，如果您正在编辑 `kismet.conf` 文件，请使用 UNIX 编辑器。这可以是原生 Linux 应用程序，如果是通过 Cygwin 在 Windows 下运行，或者是其他支持 UNIX 文本格式的编辑器。

`kismet.conf` 文件中的注释是以 “#” 符号开头的行。这些通常是注释或示例配置，通常可以指导您需要设置哪些选项。不以注释开头的行才是服务器实际执行的参数变量。一个好习惯是通过在行首加上 “#” 来注释掉现有行，并添加一行包含调整后的参数。这样，如果出现问题，您就知道原始参数是什么。

### Kismet.conf

```
# Kismet config file
# Most of the "static" configs have been moved to here -- the command line
# config was getting way too crowded and cryptic. We want functionality,
# not continually reading --help!
```

Kismet 服务器以前是通过命令行参数控制的（其中许多现在仍可使用），但随着程序和功能的增长，设置所有用于源、端口等的命令行参数变成了一项艰巨的任务。因此，所有内容都转移到了 `kismet.conf` 文件中。上面的行是 `kismet.conf` 文件的开头，这是一种对早期时代的回顾，当时人们花费大量时间查看 `--help` 命令行开关。

```
# Version of Kismet config
version=2007.09.R1
```

这行指示的是配置文件本身的版本，而不是服务器或程序其他部分的版本。许多人将此行与服务器版本混淆，并疑惑为什么他们的服务器版本落后了三个版本。配置文件的变更频率不像工具包的其他部分那样频繁，因此在这行中列出了一个独立的版本号。

```
# Name of server (Purely for organizational purposes)
servername=Kismet
```

该参数是配置中那些经常被忽视的部分之一，它位于文件的最顶部。`servername` 参数允许您为服务器命名，以用于您自己的组织管理目的。如果您使用一个客户端实例监控多个远程服务器，这特别有用。您可以按位置（`server_north_east`、`server_north_west_warehouse`）或信道（`server_ch1`、`server_ch2`）来命名服务器，或者按您认为能保持条理的方式来命名。服务器名称不能包含空格，因此请使用下划线或破折号代替空格。这可以让您知道自己连接的是哪个服务器及其位置，用于故障排除或事件跟踪。它对性能没有实际影响，只是有助于保持条理，特别是在大型安装环境中。

```
# User to setid to (should be your normal user)
uiduser=your_user_here
```

刚开始使用 Kismet 的人常常误解这一行。这是 Kismet 启动后运行其进程所使用的用户。Kismet 需要 root 权限来设置监听模式和其他选项，然后在 Kismet 进程中将权限降低为此参数中指定的用户。

```
sqliduser=foo
```

上面是一个示例，其中 “foo” 是系统上的一个普通用户账户。

**注意**

如基础 Kismet 安装章节所述，除非您以 Set User ID (SUID) root 方式构建 Kismet，否则您需要系统中有一个普通的非特权用户。这是出于安全原因。在此指定的用户必须对您存储捕获数据和日志的目录具有写权限。人们经常遇到的一个主要问题是他们以 root 运行 Kismet 并指定 root 为 SETUID 用户。除非您以 SETUID root 方式构建，否则这将导致 Kismet 无法启动。他们还犯的一个错误是以 root 登录，从 /root 运行 Kismet，由于 SETUID 用户没有 /root 目录的写权限，服务器无法启动。简单的解决方案是以普通用户登录，然后使用 su 切换到 root 或使用 sudo 启动 Kismet。

指定系统中一个非特权（非 root）用户的用户名，并确保您存储数据的任何地方都有写权限。逻辑上的位置是非特权用户的家目录。避免问题的最佳 Kismet 运行顺序是以普通用户登录，切换到您希望保存结果数据的目录，然后 “su” 切换到 root，再运行 Kismet。

```
# Do we try to put networkmanager to sleep? If you use NM, this is probably # what you want to do, so that it will leave the interfaces alone while # Kismet is using them. This requires DBus support! networkmanagersleep=true
```

配置文件中的这一行告诉 Kismet 使用 Dbus 来禁用 Network Manager（常见的 gnome 桌面管理小部件），使其在 Kismet 会话期间自我禁用。Kismet 退出后，网络管理器将恢复控制。

**注意**

> 许多现代 Linux 发行版使用精美的 X 小部件来控制网卡。这是为了让系统更用户友好，避免用户必须去命令行连接无线网络的一种尝试。问题是，如果我们想对网卡做一些“奇怪”的操作，例如监听模式，这些网络监控程序会争夺网卡的控制权，从而给 Kismet 带来无尽的麻烦。
>
> 如果您遇到任何奇怪的扫描情况，例如随机停止扫描或卡在某个信道上不跳转，这很可能是一个罪魁祸首。在大多数情况下，您希望启用此选项。
>
> 在某些情况下，这可能会导致问题。最常见的情况是，当您使用一个接口进行扫描，但使用网络管理器控制另一个接口用于通信（例如，向服务器报告的入侵检测系统 (IDS) 设置）时。Kismet 会禁用所有接口（有线和无线）的网络管理器。如果您遇到网络管理器被禁用导致的问题，您可能希望完全不用网络管理器，并手动配置其他接口。

```
# Sources are defined as:
# source=sourcetype,interface,name[,initialchannel]
# Source types and required drivers are listed in the README under the
# CAPTURE SOURCES section.
# The initial channel is optional, if hopping is not enabled it can be used
# to set the channel the interface listens on.
# YOU MUST CHANGE THIS TO BE THE SOURCE YOU WANT TO USE
```

这可能是配置文件最重要的部分之一：我们从哪里获取数据。source 行告诉 Kismet 它需要知道什么才能将数据输入程序，以便我们可以开始扫描。每个源都有三个参数：特定类型卡片的 Kismet 源名称、接口名称，以及在 Kismet 客户端中找到的逻辑名称。Kismet 的 README 列出了兼容的源及其正确的接口名称。

| 驱动程序 | 描述 | 链接 / 接口 |
| :--- | :--- | :--- |
| hostap | Prism/2 Linux HostAP 0.4 | http://hostap.epitest.fi/ |
| | 捕获接口 | `wlanX` |
| | HostAP 驱动程序驱动作为接入点的 Prism/2 芯片组 | |

