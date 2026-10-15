
# 描述 (DESCRIPTION)

`xdm` 管理一组显示器，这些显示器可能在本地主机或远程服务器上。`xdm` 的设计参考了 X 终端的需求以及 X Consortium 标准 XDMCP（X 显示管理器协议）。`xdm` 提供了类似于 `getty` 在字符终端上登录提供的服务：提示用户名和密码、验证用户身份以及运行会话。

# 第一部分 用户命令

会话由特定进程的生命周期定义；在传统的字符终端世界中，它是用户的登录 shell。在 `xdm` 上下文中，它是一个任意会话管理器。这是因为在窗口环境中，用户的登录进程并不一定具有任何可以连接的终端接口。当没有可用会话管理器时，通常使用窗口管理器或终端作为会话管理器，这意味着该进程的终止会导致用户的会话终止。

会话终止时，`xdm` 重置服务器并（可选）重启整个过程。

当 `xdm` 通过 XDCP 接收查询时，它可以运行一个选择器代表显示器执行 XDCP 广播查询（或对指定主机的 XDCP 查询），并提供提供 XDCP 显示管理的主机菜单。此功能对于自身不提供主机菜单的 X 终端非常有用。

因为它提供了用户看到的第一个界面，它被设计为易于使用并能根据特定站点的需求进行定制。`xdm` 有许多选项，具有合理的默认值。浏览此手册的各个章节，挑选你想要更改的内容。特别注意“会话程序”子部分，它将描述如何设置所需的会话。

# 概述 (OVERVIEW)

`xdm` 是高度可配置的，所有行为都可以通过资源文件和脚本控制。这些文件的名称记录自 `xdm-config` 或由 `-config` 选项命的文件。

`xdm` 提供两种管理方式。它可以管理在本地机器运行并在 `Xservers` 中指定的 X 服务器，并可以使用 XDM（XDM 控制协议）管理远程服务器（通常为 X 终端）。

X 客户端资源（包括登录自身的）受到在 `Xresources` 中设置资源的影响。对于不提供主机菜单的终端，`xdm` 可以收集主机并运行选择器程序为用户提供菜单。对于连接到主机的显示，通常不需要，因为本地主机执行显示管理。

在重置 X 服务器后，`xdm` 运行 `Xstartup` 脚本辅助设置用户看到的屏幕。

当用户登录时，`xdm` 以 root 身份运行 `Xstartup` 脚本。

`xdm` 以用户身份运行 `XSession`。系统可能会进行额外的启动，并通常运行用户目录下的脚本。当 `XSession` 脚本退出时，会话结束。

会话结束时，`Xreset` 脚本清理，X 服务器重置，循环开始。

`/usr/X11/lib/X11/xdm-errors` 文件包含 `xdm` 的错误消息以及 `Xsetup`、`Xstartup`、`Xsession` 或 `Xreset` 输出到 stderr 的内容。当你运行 `xdm` 遇到问题时，检查此文件是否有任何线索。

# 参数 (OPTIONS)

除 `-config` 本身外，所有这些选项都可以在配置文件作为资源指定值。

- `-config configuration_file`
- `-nodemon`：将 `DisplayManager.daemonMode` 资源的值指定为 false。这抑制守护进程行为，用于让 `xdm` 在启动时关闭所有文件描述符、从控制终端关联并将自己置于后台。

# xdm

# 601

`-debug debug_level`

指定 `DisplayManager.debugLevel` 资源的数值值。非零值会使 `xdm` 将调试语句打印到终端：它还会禁用 `DisplayManager.daemonResource`，强制 `xdm` 以同步方式运行。为了解释这些调试信息，几乎需要一份 `xdm` 的源代码副本。目前尚未对输出内容进行任何合理化或标准化处理。

`-error error_log_file`

指定 `DisplayManager.errorlog` 资源的值。该文件包含来自 `xdm` 的错误信息，以及会话进行期间各种脚本和程序写入的所有内容。

`-resources resource_file`

指定 `DisplayManager*resources` 资源的值。该文件由 `xdm` 加载，用于指定身份验证组件的配置参数。

`-server server_entry`

指定 `DisplayManager.servers` 资源的值。有关该资源的描述，请参见“本地服务器规范”（Local Server Specification）小节。

`-udpPort port_number`

指定 `DisplayManager.requestPort` 资源的值。这设置了端口号，`xdm` 将通过该端口号监听 XDMCP 请求。由于 XDMCP 使用注册的 UDP 端口，除非为了调试，否则不应更改此资源。

`-session session_program`

指定 `DisplayManager*session` 资源的值。这指示了用户登录后作为会话运行的程序。
类似于大多数 Toolkit 应用程序，允许指定任意资源。

`-xrm resource_specification`

# RESOURCES

在许多阶段，`xdm` 的行为可以通过其配置文件（采用 X 资源格式）进行控制。某些资源会修改 `xdm` 的行为，另一些则修改其在单个显示器上的行为。当操作涉及特定显示器时，显示器名称会被插入 Display-Manager 和最终资源名称之间。

对于本地显示器，资源名称是显示器网络地址解析的结果。请参见 `removedomain` 资源。名称必须完全匹配；`xdm` 感知所有可能访问给定显示器的网络。如果名称解析为假（false），则使用该地址。资源类如 XDMCP Manage 资源所示。

由于资源管理器使用冒号来分隔资源及其值，并使用冒号分隔不同的资源名，`xdm` 在生成资源名称时用下划线替换点和冒号。例如，`DisplayManager.expo x 0.startup` 是定义 `expo xdm.org:0` 显示器服务器的资源名称。

此资源指定所有服务器条目的文件名，每行一个（如果值以斜杠开头），或者单个服务器条目。详情请参见“本地服务器规范”（Local Server Specification）小节。

`DisplayManager.servers`

这指示 `xdm` 用于监听传入的 XDMCP 请求的 UDP 端口号。除非你需要调试系统，否则请保持其默认值 177。

`DisplayManager.requestPort`

# 第一部分：用户命令

`DisplayManager.errorLogFile`

错误输出通常重定向到系统控制台。要重定向输出，请将此资源设置为文件名。对于支持的系统，已开发了一种将这些消息发送到 syslog 的方法；由于接口种类众多，无法实现任何独立系统的方案。该文件还包含 `Xsetup`、`Xstartup`、`Xsession` 和 `Xset` 文件重定向到 stderr 的任何输出，因此也包含这些脚本中问题的描述。

`DisplayManager.debugLevel`

如果此资源的整数值大于零，将打印后台守护模式（daemon mode）。它还会禁用将信息重定向到位桶（bit-bucket），并允许非本地用户运行 `xdm`，这在通常情况下是有用的。

`DisplayManager.daemonMode`

通常情况下，`xdm` 尝试让自己成为与任何终端关联的守护进程。这是通过派生（forking）并让父进程退出，然后关闭文件描述符并释放控制终端实现的。在某些环境中，这并不是所需要的（特别是调试时）。将此资源设置为假（false）将禁用此功能。

`DisplayManager.pidFile`

将创建一个文件来存储主进程进程 ID 的 ASCII 表示法，`xdm` 还对该文件使用锁定，以消除在同一台机器上运行多个守护进程，这可能会导致一些混乱。

`DisplayManager.lockFile`

这是一个控制 `xdm` 是否使用文件锁来防止多个管理器运行的资源。在 System V 上，它使用 lock 库调用，而在 BSD 上则灵活处理。

`DisplayManager.authDir`

这在初始化会话时指定 `xdm` 授权文件所在的目录。默认值为 y。

`DisplayManager.autoRescan`

此布尔值控制在会话终止且文件发生变化后，`xdm` 是否重新扫描配置、服务器访问和身份密钥文件。默认为真。你可以向主进程发送 `SIGHUP` 信号来强制 `xdm` 重新加载这些文件。

`DisplayManager.removeDomainname`

在比较 XDMCP 客户端的显示器名称时，名称解析通常会为终端创建一个完全限定的主名。这有时会引起困惑，当此变量设置时，如果主机名与本地主机名相同，`xdm` 将移除主机名中的域名。默认值为真。

`DisplayManager.keyFile`

XDM AUTHENTICATION 风格的 XDMCP 身份验证要求在 `xdm` 和终端之间共享私钥。此资源指定由文件名和共享密钥组成的密钥文件列表。默认情况下，`xdm` 不支持 XDM-AUTHENTICATION-1，因为它需要 DES，由于美国出口限制，DES 通常不被分发。

# xdm

# 603

`DisplayManager.accessFile`

为了防止未经授权的 XDMCP 服务并允许转发 XDMCP 间接请求，该文件包含允许直接访问此机器的主机名数据库，或者包含一个应被转发的主机列表。该文件的格式见“XDMCP 控制”（XDMCP Control）小节。

`DisplayManager.exportList`

一组由空格分隔的额外环境变量，传递给 `Xset`、`Xstart`、`Xsession` 和 `Xreset` 程序。
用于生成授权密钥种子的文件。默认应为频繁变化的文件 `/dev/mem`。

`DisplayManager.randomFile`

在支持动态加载生成器的系统上，这是库的名称。默认值为 `/Root/lib/X11/xdm/libxdreet`。

`DisplayManager.greeterLib`

用户从选择器（chooser）选择主机后等待响应的秒数。如果在此时间内显示间接请求，则将其转发到选择器主机。否则，假设来自新会话并提供选择器。默认值为 15。

`DisplayManager.choiceTimeout`

此资源指定 `xdm` 加载到显示器 0 根窗口的资源数据库文件名。`Xsetup` 程序、登录窗口和选择器将使用此文件中设置资源。此资源数据库在身份验证进行之前加载，因此它可以控制登录窗口的外观。请参见“身份验证组件”（Authentication Widget）小节，该节描述了适用于此文件中的各种资源。此资源没有默认值，但 `/Root/lib/X11/xdm/chooser` 是约定名称。

`DisplayManager.DISPLAY.chooser`

此指定作为特殊主机 `<chooser>` 请求的间接查询的头部菜单运行的程序。`<Root/lib/X11/xdm/chooser "XDMCP Control" "chooser."`

`DisplayManager.DISPLAY.xrdb`

此指定加载资源的程序。默认情况下，`xdm` 使用 `/Root/bin/xrdb`。

`DisplayManager.DISPLAY.setup`

此指定在身份验证成功后（以 root 身份）运行的程序。默认不运行任何程序。此处使用的文件约定名称为 xstartup。请参见“会话程序”（Session Program）小节。

`DisplayManager.DISPLAY.session`

此指定要执行的会话（不 root root）。默认运行 `/Root/bin/xrun`。约定名称为 Xsession。请参见“会话程序”（Session Program）小节。

# 第一部分：用户命令

`DisplayManager.DISPLAY.reset`

此指定在会话结束后（以 root 身份运行）的程序。默认情况下，不运行任何程序。惯用名称为 Xreset。参见“重置程序”小节。

`DisplayManager.DISPLAY.openDelay`,
`DisplayManager.DISPLAY.openRepeat`,
`DisplayManager.DISPLAY.openTimeout`,
`DisplayManager.DISPLAY.startAttempts`

这些数值资源控制 xwm 在尝试中断瞬态服务器时的行为。`opdelay` 是连续尝试之间的间隔时间（秒），`openrepeat` 是尝试的次数，`timeout` 是在实际尝试打开时等待的时间（即在 `connect(2)` 系统调用中花费的最长时间），`startattempts` 是在打开服务器之前执行此过程的重复次数。在完成 `openrepeat` 次尝试后，或者在任何特定尝试中 `timeout` 结束时，将终止并重启服务器，尝试重新连接，此时显示器被声明为死亡并禁用。尽管这种行为看起来可能是随机的，但它是通过经验得出的，并且对大多数系统都运行良好。默认值是：`opdelay` 为 5，`openrepeat` 为 5，`startattempts` 为 4。

`DisplayManager.DISPLAY.pingInterval`,
`DisplayManager.DISPLAY.pingTimeout`

为了发现显示器何时消失，偶尔使用 X 连接和 Xsync 调用对它们进行 ping。`pinginterval` 指定每次 ping 之间的时间（分钟），`pingtimeout` 指定等待终端响应请求的等待时间（分钟）。如果终端没有响应，则会话被声明为死亡并终止。默认情况下，两者都设置为 5 分钟。如果你经常使用与管理主机隔离的 X 终端，你可能想要增加此值。唯一担心的是会话将一直持续到终端被意外禁用。xwm 不会 ping本地显示器。尽管这看起来无害，但如果因为服务器挂起 NPF 服务且不响应 ping 而导致锻炼会话终止，将是不快的。

`DisplayManager.DISPLAY.terminateServer`

此资源指定在会话结束时是否终止 X 服务器（而不是重置）。当服务器随着时间的推移而增大时，可以使用此选项限制服务器运行的时间。默认值为 false。

`DisplayManager.DISPLAY.userPath`

xwm 将会话的 `PATH`环境变量设置为此值。它应该是一个由冒号分隔的目录列表；完整描述请参考 `sh(1)`。`/etc:/bin:/bin:/usr/X11/bin:/usr/bin` 是一个常用设置。默认值在编译时通过 X 系统配置文件中的 `DefaultUserPath` 指定。

`DisplayManager.DISPLAY.systemPath`

Xwm 将启动和重置脚本的 `PATH` 环境变量设置为此资源。该资源在编译时通过系统配置文件中的 `DefaultSystem-Path` 条目指定；`/etc:/bin:/usr/bin:/usr/bin:xdm: xdm` 是一个常见选择。注意此条目中缺少 (.)。对于 root 来说，这是一个良好的做法；它可以避免许多特木马系统渗透方案。

`DisplayManager.DISPLAY.systemShell`

`xdm` 将启动和重置脚本的 `SHELL` 环境变量设置为此资源的值。默认是 `/bin/sh`。

`DisplayManager.DISPLAY.failsafeClient`

如果默认会话失败，`xdm` 将回退到默认程序。该程序执行时不带任何参数，但会使用与原会话相同的环境变量。（参见“会话程序”部分）默认使用 `:xdm/bin-xterm`。

`DisplayManager.DISPLAY.grabServer`
`DisplayManager.DISPLAY.grabTimeout`

为了提高安全性，grab 和键盘读取将读取用户名和密码。`grab` 资源指定在读取名称/密码期间是否锁定服务器。当为 false 时，服务器在 grab 成功后将取消锁定；否则，服务器将保持锁定直到会话开始之前。`grabtimeout` 资源指定 `xdm` 等待 grab 的最长时间。如果其他客户端已锁定了服务器（可能是因为网络延迟高），grab 可能会失败。三秒；在增加此值时应小心，因为用户可能会被显示器上的伪装窗口发现。如果 grab 失败，它将杀死并（如果可能）将会话返回服务器。

`DisplayManager.DISPLAY.authorize`
`DisplayManager.DISPLAY.authName`

`authorize` 是一个控制 `xdm` 是否为本地服务器连接生成并使用授权的资源。如果使用授权，`authme` 是要使用的授权机制列表，用空格分隔。支持 XDMCP 机制，但在这种情况下会忽略 `authme`。如果为显示器设置了 `authorize` 但无法授权，用户将通过登录窗口中显示的不同消息获得通知。默认情况下，`authorize` 为 true；`authme` 为 MAGIC-COOKIE-1，或者如果 COOKIE-1 可用，为 XDM-AUTHORIZATION-1 MIT MAGIC-COOKIE-1。

`DisplayManager.DISPLAY.authFile`

此文件使用 `auth` 命令行选项将授权数据从 `xdm` 通信到服务器。它应该放在非全局可写的目录中，因为它很容易被删除，从而禁用服务器中的授权机制。

`DisplayManager.DISPLAY.authComplain`

如果设置为 false，则禁用在登录窗口中显示用户欢迎语。参见“身份验证窗口”小节。默认是 true。

`DisplayManager.DISPLAY.resetSignal`

`xdm` 发送以重置服务器的信号数。参见“控制服务器”小节。默认是 1 (SIGHUP)。

`DisplayManager.DISPLAY.termSignal`

`xdm` 发送以终止服务器的信号数。参见“控制服务器”小节。默认是 15 (SIGTERM)。

# 第一部分：用户命令

`DisplayManager.DISPLAY.reset`

此指定在会话结束后（以 root 身份运行）的程序。再次，默认情况下不运行任何程序。惯用名称为 Xreset。参见“重置程序”小节。

`DisplayManager.DISPLAY.openDelay`,
`DisplayManager.DISPLAY.openRepeat`,
`DisplayManager.DISPLAY.openTimeout`,
`DisplayManager.DISPLAY.startAttempts`

这些数值资源控制 xwm 在尝试中断瞬态服务器时的行为。`opdelay` 是连续尝试之间的间隔时间（秒），`openrepeat` 是尝试的次数，`timeout` 是在实际尝试打开时等待的时间（即在 `connect(2)` 系统调用中花费的最长时间），`startattempts` 是在打开服务器之前执行此过程的重复次数。在完成 `openrepeat` 次尝试后，或者在任何特定尝试中 `timeout` 结束时，将终止并重启服务器，尝试重新连接，此时显示器被声明为死亡并禁用。尽管这种行为看起来可能是随机的，但它是通过经验得出的，并且对大多数系统都运行良好。默认值是：`opdelay` 为 5，`openrepeat` 为 5，`startattempts` 为 4。

`DisplayManager.DISPLAY.pingInterval`,
`DisplayManager.DISPLAY.pingTimeout`

为了发现显示器何时消失，偶尔使用 X 连接和 Xsync 调用对它们进行 ping。`pinginterval` 指定每次 ping 之间的时间（分钟），`pingtimeout` 指定等待终端响应请求的等待时间（分钟）。如果终端没有响应，则会话被声明为死亡并终止。默认情况下，两者都设置为 5 分钟。如果你经常使用与管理主机隔离的 X 终端，你可能想要增加此值。唯一担心的是会话将一直持续到终端被意外禁用。xwm 不会 ping本地显示器。尽管这看起来无害，但如果因为服务器挂起 NPF 服务且不响应 ping 而导致锻炼会话终止，将是不快的。

`DisplayManager.DISPLAY.terminateServer`

此资源指定在会话结束时是否终止 X 服务器（而不是重置）。当服务器随着时间的推移而增大时，可以使用此选项限制服务器运行的时间。默认值为 false。

`DisplayManager.DISPLAY.userPath`

xwm 将会话的 `PATH`环境变量设置为此值。它应该是一个冒号分隔的目录列表；完整描述请参考 `sh(1)`。`/etc:/bin:/bin:/usr/X11/bin:/usr/bin` 是一个常用设置。默认值在编译时通过 X 系统配置文件中的 `DefaultUserPath` 指定。

`DisplayManager.DISPLAY.systemPath`

Xwm 将启动和重置脚本的 `PATH` 环境变量设置为此资源。该资源在编译时通过系统配置文件中的 `DefaultSystem-Path` 条目指定；`/etc:/bin:/usr/bin:/usr/bin:xdm` 是一个常见选择。注意此条目中缺少 (.)。对于 root 来说，这是一个良好的做法；它可以避免许多木马系统渗透方案。

`DisplayManager.DISPLAY.systemShell`

`xdm` 将启动和重置脚本的 `SHELL` 环境变量设置为此资源的值。默认是 `/bin/sh`。

`DisplayManager.DISPLAY.failsafeClient`

如果默认会话失败，`xdm` 将回退到默认程序。该程序执行时不带任何参数，但会使用与原会话相同的环境变量。（参见“会话程序”部分）默认使用 `:xdm/bin-xterm`。

`DisplayManager.DISPLAY.grabServer`
`DisplayManager.DISPLAY.grabTimeout`

为了提高安全性，grab 和键盘读取将读取用户名和密码。`grab` 资源指定在读取名称/密码期间是否锁定服务器。当为 false 时，服务器在 grab 成功后将取消锁定；否则，服务器将保持锁定直到会话开始之前。`grabtimeout` 资源指定 `xdm` 等待 grab 的最长时间。如果其他客户端已锁定了服务器（可能是因为网络延迟高），grab 可能会失败。三秒；在增加此值时应小心，因为用户可能会被显示器上的伪装窗口发现。如果 grab 失败，它将杀死并（如果可能）将会话返回服务器。

`DisplayManager.DISPLAY.authorize`
`DisplayManager.DISPLAY.authName`

`authorize` 是一个控制 `xdm` 是否为本地服务器连接生成并使用授权的资源。如果使用授权，`authme` 是要使用的授权机制列表，用空格分隔。支持 XDMCP 机制，但在这种情况下会忽略 `authme`。如果为显示器设置了 `authorize` 但无法授权，用户将通过登录窗口中显示的不同消息获得通知。默认情况下，`authorize` 为 true；`authme` 为 MAGIC-COOKIE-1，或者如果 COOKIE-1 可用，为 XDM-AUTHORIZATION-1 MIT MAGIC-COOKIE-1。

`DisplayManager.DISPLAY.authFile`

此文件使用 `auth` 命令行选项将授权数据从 `xdm` 通信到服务器。它应该放在非全局可写的目录中，因为它很容易被删除，从而禁用服务器中的授权机制。

`DisplayManager.DISPLAY.authComplain`

如果设置为 false，则禁用在登录窗口中显示用户欢迎语。参见“身份验证窗口”小节。默认是 true。

`DisplayManager.DISPLAY.resetSignal`

`xdm` 发送以重置服务器的信号数。参见“控制服务器”小节。默认是 1 (SIGHUP)。

`DisplayManager.DISPLAY.termSignal`

`xdm` 发送以终止服务器的信号数。参见“控制服务器”小节。默认是 15 (SIGTERM)。

# 第一部分：用户命令

`DisplayManager.DISPLAY.resetAuth`

原始实现在连接显示器之前读取授权文件的主机名或模式通过包含一个或多个字符（* 匹配零个或多个字符，? 匹配任意字符）与主机名进行比较来区分主机名。如果是主机名，所有比较都使用网络地址进行，因此任何转换为正确网络地址的名称均可用。默认是 false，适用于所有 MIT 服务器。

`DisplayManager.DISPLAY.userAuthDir`

当 `xdm` 无法使用用户文件（`$HOME/.Authority`）时，它会在目录中创建一个唯一的。。使用 `/tmp` 作为默认。

# 配置文件

第一个 `xdm` 配置文件应该设置。目录（`<Root>/lib/X11/xdm`，其中 `<Root>` 指 X11 安装树）包含所有相关文件。在示例中，使用了 `<Root>`。这是一个合理的配置文件，可以命名为 `xdm-config`：
```
DisplayManager.servers:/usr/X11/lib/X11/xdm/Xservers
DisplayManager.errorlog:/usr/X11/lib/X11/xdm/Xerrors
DisplayManager.resources:/usr/X11/lib/X11/xdm/Xresources
DisplayManager.startup:/usr/X11/lib/X11/xdm/Xstartup
DisplayManager.session:/usr/X11/lib/X11/xdm/Xsession
DisplayManager.pidfile:/usr/X11/lib/X11/xdm/xdm-pid
DisplayManager.authorize: true
```

注意此文件主要包含对其他文件的引用。注意某些资源是用 * 分隔组件的。通过将 * 替换为显示器名称，这些资源可以每个显示器都是唯一的，但这没有用。请参见“资源”部分获取完整讨论。

# XDMP 访问

`DisplayManager_accessFile` 数据库文件提供了 `xdm` 用于控制请求 XDMP 服务的显示器的信息。此文件包含三种条目：控制直接和广播查询响应的条目、控制间接条目响应的条目以及宏定义。

直接条目的格式为主机名或模式，通过包含一个或多个字符（*匹配零个或多个字符，? 匹配任意字符）与显示器主机名比较来区分。如果是主机名，所有比较都使用网络地址进行，因此任何转换为正确网络地址的名称均可用。对于模式，仅使用规范主机名进行比较，因此确保你不要尝试匹配别名。在主机名或模式前加上 `!` 会排除该条目对应的主机。

间接条目包含一个主机名或模式，随后是应发送间接条目查询的主机名或宏列表。

宏定义包含宏名称以及该宏展开的主机名和其他宏。为了区分宏和主机名，宏以 `%` 字符开头。宏可以嵌套。

间接条目还可以指定 `xdm` chooser 以提供连接的主机菜单。参见“chooser”章节。

## xdm

607

在检查特定显示主机的访问权限时，会逐条扫描记录，由第一个匹配的记录决定响应。在扫描间接（Indirect）项时，会忽略直接（Direct）和广播（Broadcast）项，反之亦然。

空行会被忽略，`#` 被视为注释分隔符（该行后续内容将被忽略），`\newline` 会导致忽略换行，允许间接主机列表跨多行。这是一个 xaccess 文件的示例：
```
```
