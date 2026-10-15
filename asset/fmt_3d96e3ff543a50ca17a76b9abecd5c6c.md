
由于大多数系统管理员工作在包含 Linux 和其他系统的异构网络环境中，你需要确保环境已正确配置。

如果你选择使用远程 shell（`remote shell`）选项，则你必须在 Linux 用户的家目录下拥有一个 `.hosts` 文件。该文件必须包含 MS Windows 系统的主机名或 IP 地址。

你还必须确保没有在 `/etc/inetd.conf` 中禁用 `rsh` 或 `rexec` 所在的行。出于安全考虑，你可能可能希望通过 `/etc/hosts.deny` 文件禁止任何人使用 `rsh` 或 `rexec`，并且在 `/etc/hosts.allow` 文件中仅允许特定服务的服务的主机。有关 TCP Wrapper 的详细信息，请参阅第 18 章“安全基础 101”。

如果你希望在每次启动 X-Win32 时自动启动此会话，可以点击“自动启动”（Auto startup）选项。同时，确保 Windows 设置设置为“切换到多窗口”（Switch to multiple windows）选项。

输入 X 应用程序所在的 Red Hat Linux 服务器的主机名。

在“登录”（Login）字段中输入用户名。如果你选择远程执行（`rexec`）选项，每当你想连接会话时，系统都会提示你输入密码。如果你希望只输入一次密码，可以在“密码”字段中输入，该字段仅在你选择 `rexec` 选项时显示。

在“命令”（Command）字段中，输入你想要运行的命令。通常，你会在这里运行 `xterm`。因此，你可以将此字段设置为：`/usr/bin/X11/xterm -display $DISPLAY`。

保存修改后的会话并退出 X-Util32 应用程序。

现在你已准备好运行新会话了。点击任务栏上的 X-Win32 图标并选择“会话”（Sessions）菜单。从会话菜单中选择修改后的会话名称。如果你通过 `rexec` 连接，系统会提示你输入密码。一旦验证成功，一个 `xterm`（或你在 X-Util32 中编辑此条目时输入的任何内容）将出现在你的 MS Windows 系统上。如果你在几秒钟后没有看到该程序，请回到任务栏上的 X-Win32 图标，点击“显示消息”（Show Messages）选项，并尝试重新运行应用程序。留意消息窗口中的任何权限错误。如果遇到权限错误，可能是你忘记在 `/etc/inetd.conf` 中启用 `rexec` 或 `rsh` 服务，或者你忘记在修改 `/etc/inetd.conf` 后重启服务器，又或者尚未设置 `.hosts` 文件为仅所有者可写（其他人应该只对该文件具有读取权限）。

此时，你应该已经在 Micro-Win32 服务器下运行了一个 X Windows 应用程序。如果你倾向于启动 `fwm2` 或 `openstep` 等 X Windows 管理器并像通常一样运行所有 X Windows 应用程序（即就像你在 Red Hat Linux 系统上一样），你应该执行以下操作：

## 第 22 章：配置 X Window 系统

- 使用 `Util32` 创建或编辑会话。像以前那样输入主机名、登录用户名和连接方法（`rsh`、`rex`）。选择“切换到单窗口”（Switch to single window）选项，并输入以下行作为命令：

```
fvwm2 -display $DISPLAY
```

- 不要忘记将 `fvwm2` 替换为你喜爱的 X Windows 管理器。保存新的（或已过的）会话。

现在关闭你已经启动的所有 X Windows 客户端会话，一旦所有 X 连接都关闭，即启动新会话。你应该看到一个巨大的单窗口，其中加载了你喜爱的 X Windows 管理器。现在你可以使用 X Windows，就像在 Red Hat Linux 系统的控制台上运行它一样。如果遇到问题，请阅读在线故障排除信息以获取详情。

还可以使用 Micro-Win32 允许基于 `xdm` 的验证连接。

## 总结

在本章中，你学习了如何在 Red Hat Linux 系统上设置 X Windows。我讨论了如何安装和配置 XFree86 X Window 系统。你学习了如何使用各种工具自定义和个性化你的 X Windows 环境，最后学会了……

## 第八部分：运行 X Windows

```
Style "xeyes"               MinimalDecoration, CirculateSkip

Style "xload"               StickyOnTop, MinimalDecoration, CirculateSkip

Style "*ppp"              StickyOnTop, MinimalDecoration, CirculateSkip

Style "Msgs"              CirculateSkip

Style "*console"          CirculateSkip

Style "*xman"               MinimalDecoration, CirculateSkip

ifdef(NO_ICONS, {

  Style "**xterm**"         Icon xterm.xpm

  Style "*shell*"         Icon xterm.xpm

})
```
