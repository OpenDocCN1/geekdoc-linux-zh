

10.10.0.1-kickstart。请注意，如果你没有指定服务器名称，那么客户端系统将尝试使用响应 BOOTP/DHCP 请求的服务器作为其 NFS 服务器。如果没有指定路径或文件名，客户端系统将尝试从 BOOTP/DHCP 服务器挂载 /kickstart，并将尝试使用上面所述的相同 <ip-addr>-kickstart 文件名来查找 kickstart 文件。

## 开始 Kickstart 安装

要开始 kickstart 安装，你必须从 Red Hat Linux 启动软盘启动系统，并在启动提示符下输入特殊的启动命令。如果 kickstart 文件位于启动软盘上，正确的启动命令应为：

```
boot: linux ks=floppy
```

如果 kickstart 文件位于服务器上，则适当的启动命令应为：

```
boot: linux ks
```

## Kickstart 文件

现在你已经了解了一些关于 kickstart 安装的背景信息，让我们来看看 kickstart 文件本身。kickstart 文件是一个简单的文本文件，包含由关键字标识的项目列表。你可以通过编辑 Red Hat Linux CD-ROM 的 docs/ 目录中 found 的 README.ks 文件的副本来创建它，也可从头创建。你应该能够使用任何可以保存为 ASCII 文本的文本编辑器或文字处理器来编辑它。首先，在创建 kickstart 文件时请记住以下一些基本规则：

- 项目必须按顺序指定。尝试更改必需项目的顺序并不是一个好主意。
- 不必需的项目可以省略。
- 对于 kickstart 升级，以下项目是必需的：

## Red Hat Linux 6.0 安装指南

- language
- installation method
- device specification
- keyboard setup
- the upgrade keyword
- LILO configuration 如果指定了任何其他项目用于升级，则这些项目将被忽略（请注意，这包括软件包选择）。

- 省略任何必需的项目将导致安装过程提示用户回答该问题，就像在正常安装期间一样。如果发生这种情况，一旦给出答案，安装将继续无人值守（除非它遇到另一个缺失的项目）。
- 以井号（"#"）开头的行被视为注释，并将被忽略。

让我们按顺序查看每个项目。

### lang — Language Setting

必须出现的第一个项目是语言设置。你指定的语言将在安装期间使用，并用于配置已安装系统的任何语言特定方面。语言规范必须是两字母 ISO 语言代码，例如 en 表示英语，de 表示德语，fr 表示法语，等等。例如，要将语言设置为英语，kickstart 文件应包含以下行：

```
lang en
```

### network — Networking Configuration

下一个项目是网络配置信息。此行用于告诉系统应如何为自身配置网络。它是可选的，如果省略，系统将被配置为独立操作。有三种不同的网络配置方法：

- DHCP
- BOOTP
- static

DHCP 方法使用 DHCP 服务器系统来获取其网络配置。正如你可能猜到的，BOOTP 方法类似，需要 BOOTP 服务器提供网络配置。static 方法要求你在 kickstart 文件中输入所有必需的网络信息。顾名思义，此信息是静态的，将在安装期间以及安装后使用。要指示系统使用 DHCP 获取其网络配置，请使用以下行：

```
network --bootproto dhcp
```

要指示机器使用 BOOTP 获取其网络配置，请在 kickstart 文件中使用以下行：

```
network --bootproto bootp
```

静态网络的行更复杂，因为你必须在一行中包含所有网络配置信息。你需要指定：

- IP address
- netmask
- gateway IP address
- nameserver IP address

这是一个静态行的示例：

```
network --bootproto static \
--ip 10.0.2.15 \
--netmask 255.255.255.0 \
```
