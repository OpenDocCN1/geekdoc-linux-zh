

## 表 2-2 基本控制台命令（续）

| 命令语法 | 描述 |
| :--- | :--- |
| `UNBIND` _protocol_ `[FROM]` _LAN_driverboard_name_ | 从 LAN 卡中移除一个协议。将 _protocol_ 替换为您希望从该卡中移除的协议栈（例如 IPX）的名称。将 _LAN_driverboard_name_ 替换为已为 NIC 加载的驱动程序程序的名称，或 `LOAD` 命令分配给网卡的名称。 |
| `UNLOAD` _module_name_ | 从内存中移除 NLM，并将内存空间返回给操作系统。将 _module_name_ 替换为 `MODULES` 命令中给出的当前已加载模块的名称。 |
| `VOLUMES` | 显示所有已挂载卷的列表，以及卷类型（NSS 或传统类型）和支持的命名空间。 |
| `PROTOCOLS` | 显示所有当前已加载协议的列表。 |
| `HELP` _command_ | 显示有关指定命令的信息。例如，若要获取有关 `BIND` 命令语法和用法的信息，请输入 `HELP BIND` 并按 Enter 键。 |

## CONFIG

CONFIG 命令显示有关服务器和 NIC 配置的信息，如图 2-18 所示。

![](img/840007e8f98ea6653e5877e945c27dc6_72_0.png)

请注意，除了显示文件服务器的名称和内部网络地址外，CONFIG 命令还显示文件服务器中每个网络适配器的以下信息：

- LAN 驱动程序的名称
- 加载 LAN 驱动程序时分配的板卡名称
- 当前硬件设置，包括中断、I/O 端口、内存地址和 DMA 通道
- 分配给网络适配器的节点（站点）地址
- 绑定到网络适配器的协议栈
- 网络适配器的电缆方案的地址
- 分配给网络适配器的帧类型
- 树名称
- Bindery 上下文（用于与 NetWare 3.0 服务器向后兼容）

在安装网络适配器之前，您应该使用 CONFIG 命令，以便拥有现有板卡上所有硬件设置的最新列表。这有助于您为新卡选择唯一的中断和 I/O 地址设置。此外，在将另一台服务器添加到网络之前，可以使用 CONFIG 命令来确定电缆系统的网络地址。如果您错误地启动另一台服务器，并使用相同的电缆系统不同的网络地址，服务器之间的路由器配置错误将干扰网络通信。

## DISABLE/ENABLE LOGIN

DISABLE LOGIN 命令阻止新用户访问 NetWare 服务器上的服务。在关闭服务器之前，您应首先发出 DISABLE LOGIN 命令，以防止任何额外用户访问服务器，然后使用 BROADCAST 命令向所有现有用户发送一条消息，告知他们服务器将在指定时间关闭，他们应关闭所有文件并注销服务器。如果没有发出 DISABLE LOGIN 命令，新用户可能会在广播消息后登录服务器，而不知道服务器即将关闭。DISABLE LOGIN 命令的另一个用途是暂时阻止用户登录，以便您执行某些维护工作，例如加载新驱动程序或备份系统。工作完成且服务器可以使用后，您可以发出 ENABLE LOGIN 命令，允许用户再次登录并使用服务器。

## DOWN

DOWN 命令停用 NetWare 服务器操作系统，移除所有计算机连接，并将服务器返回到 DOS 提示符。在发出 DOWN 命令之前，您应禁用新登录并向所有用户广播一条消息，如图 2-19 所示。如果存在活动会话，NetWare 操作系统将发出一条警告消息，询问您是否要终止活动会话。

```
UASHOST:
UASHOST:DISABLE LOGIN
3-20-2002 8:19:52 am CONMSG8-5,60-85 [msgid=90013]
Login is now disabled

UASHOST:BROADCAST Server going down in 15 minutes. Please save work and logout.
UASHOST:DOWN
Java: Cleaning up resources, Please Wait.
```

![](img/840007e8f98ea6653e5877e945c27dc6_73_0.png)

如果您看到此消息，应取消 DOWN 命令并使用 Monitor 实用工具（后文“使用 Monitor 实用工具”中有描述）来确定哪些连接有打开的文件，然后向该用户发送消息让其注销。如果没人使用计算机且数据文件仍保持打开状态，您可能需要去该计算机关闭文件并注销用户。在这种情况下，您应务必提醒用户，在数据文件打开时不要无人看管计算机。

## LOAD

LOAD 命令将 NLM 加载到内存中并运行它。默认情况下，LOAD 命令在 SYS:System 目录中搜索请求的模块，除非指定了不同的路径。有效路径可以包括 NetWare 卷名称以及 DOS 本地驱动器号。当模块加载到内存中时，它将保留在那里，直到控制台操作员结束程序或使用 UNLOAD 命令将软件从内存中移除。根据所加载模块的需求，可以在 LOAD 命令后放置可选参数。

从 NetWare 5.0 开始并延续到 NetWare 6.5，不再需要运行 NLM 时使用 LOAD 命令。只需键入 NLM 的名称，系统会自动执行加载过程。

## SEARCH

当您输入命令时，服务器首先检查该命令是否为本节中描述的某个标准内部命令。如果该条目不是可识别的内部命令，服务器将尝试从 SYS:System 目录（参见第 3 章）加载一个具有该名称的 NLM。使用 SEARCH 命令，您可以指定其他路径供服务器查找 NLM。例如，您可以使用此命令为 DOS 启动分区添加一个搜索路径：

```
SEARCH ADD C:\
```

您还可以通过在系统控制台上仅键入 SEARCH 一词来使用 SEARCH 命令显示服务器的搜索路径。图 2-20 展示了将 DOS 分区添加到搜索路径、显示所有现有搜索路径，然后从搜索路径中移除 DOS 分区的示例。

```
IRASHOST:SEARCH ADD C:\
Search 12: C:\
IRASHOST:\
IRASHOST:SEARCH
Search 1: SYS\SYSTEM\
Search 2: C:\NMSERVER (default directory)
Search 3: C:\NMSERVER\DRIVERS\
Search 4: SYS:\JAGON\BIN\
Search 5: SYS:\JAGON\WQ\LFX\BIN\
Search 6: SYS:\JAGON\WJCL\L2\BIN\
Search 7: SYS:\PHP\
Search 8: SYS:\PHP\EXT\
Search 9: SYS:\APACHE2\
Search 10: SYS:\TOMCAT-4\BIN\
Search 11: SYS:\N1-UPDATE\BIN\
Search 12: C:\
IRASHOST:\
IRASHOST:SEARCH DEL 12
Removed search 12: C:\
IRASHOST:
```

![](img/840007e8f98ea6653e5877e945c27dc6_74_0.png)

## SECURE CONSOLE

SECURE CONSOLE 命令添加以下安全功能，以帮助保护服务器免受未经授权的访问：

- 阻止从其他源（例如软盘、DOS 分区或 CD）加载 NLM。要求 NLM 仅从 SYS:System 目录加载，有助于防止入侵者从软盘或服务器上的用户目录加载潜在的有害 NLM。使用 SECURE CONSOLE 命令会禁用使用 SEARCH 命令输入的任何路径。
- 仅允许控制台操作员修改日期和时间。
- 阻止通过键盘输入进入内部调试器软件。此功能很重要，因为程序员可以使用调试器更改操作系统参数。

## SEND

SEND 命令用于向特定客户端发送消息。SEND 命令最常见的用途是在关闭文件服务器之前请求用户注销。消息可以发送到用户的登录名或连接号。例如，要向连接号为 9 的用户发送消息，请输入此命令：

```
SEND "Server going down in 5 minutes" TO 9
```

## SET

SET 命令允许您从命令行查看和配置操作系统参数。虽然服务器配置参数的默认设置旨在在大多数环境中最大化网络性能，但您的特定网络可能需要修改某些设置。您将在本章后面“监控服务器健康和性能”部分中学习如何监控服务器性能以及确定是否需要任何更改。您可以通过在服务器控制台上键入 SET 命令来查看 SET 类别的列表，如图 2-21 所示。

![](img/840007e8f98ea6653e5877e945c27dc6_75_0.png)

要查看任何类别中参数的当前设置，您只需输入该类别左侧的数字。然后，您可以使用任意键显示更多参数。例如，图 2-22 显示了向下滚动几个屏幕后 Communications 类别的 SET 参数。

![](img/840007e8f98ea6653e5877e945c27dc6_75_1.png)

