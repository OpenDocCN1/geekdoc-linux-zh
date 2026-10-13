
```
-notify -verbose -fn fixed -exitOnFail
/usr/X11R6/bin/xbanner
```

当用户通过身份验证时，此文件启动 `xconsole` 和 `xbanner` 程序。对于大多数用户来说，这些程序几乎毫无用处；因此，请将其修改为适合你的内容。例如，你可以使用 `xv` 程序将 X 环境的背景设置为适合你组织的背景。或者，你也许可以启动一些大多数用户通常运行的应用程序，例如 `xmailbox`。

通过将默认运行级别更改为 5，可以在启动后自动运行 `xdm`。要将系统的运行级别更改为 5，请修改 `/etc/inittab` 文件中的以下行：

```
id:3:initdefault:
```

将 `3` 替换为 `5`，并确保在同一文件中具有以下行：

```
x5:respawn:/usr/bin/X11/xdm -nodaemon
```

## 在 MS Windows 9x/2000 上使用 XFree86

要在 MS Windows 9x/2000 上运行 X Windows 应用程序，你需要在此类平台上运行 X Windows 服务器。许多商业 X Windows 服务器软件包可用于 MS Windows 9x/2000。本节使用 Micro `X-Win32`，我已使用它一年多，发现它非常易于安装和支持。

### 获取 Micro X-Win32

你可以从 StarNet Communications Corporation 在 `http://www.starnet.com/` 下载 `X-Win32` 的试用版。产品的试用版与产品版完全相同；唯一的限制是你每会话仅可使用试用版两小时；在每个两小时周期后，你必须重新启动 MS Windows 端的 X Windows 服务器。由于试用版中没有任何功能被削弱，因此此限制不是什么大问题。毕竟，如果你使用它，你应该付费。

下载试用版后，通常以自解压可执行文件形式提供，通过双击可执行文件提取文件；安装将自动开始。你将被要求选择安装的目标目录。安装完成后，你就可以在 MS Windows 上使用 X Windows 服务器，并且你的 Red Hat Linux 服务器的 X 客户端应用程序可以在运行本地 X Windows 服务器的 MS Windows 系统上运行。

在你能够从 Red Hat Linux X 安装运行 X 客户端之前，你需要使用随发行版提供的 `X-Util32` 程序配置 Micro `X-Win32`。请执行以下操作：

- 1. 运行 `X-Util32` 程序。
- 2. 从其菜单中选择 `Sessions→Edit sessions`。从该菜单中选择一个现有会话条目，例如 `sun`。这将显示一个包含当前会话信息的对话框。
- 3. 通过在 `Session name` 字段中输入新名称来重命名会话条目。这可以是任何名称。接下来，选择连接方法：`rsh`（远程 shell）、`rexec`（远程 exec）或 `XDMCP`（用于 `xdm`）。选择最适合你的 Red Hat Linux X Windows 环境的一个。例如，如果你在 Linux 端运行 `xdm`，请选择 `XDMCP`。
- 如果你选择使用远程 shell 选项，你必须在 Linux 用户的主目录中有一个 `.rhosts` 文件。该文件必须包含 MS Windows 系统的主机名或 IP 地址。
- 同时确保你没有在 `/etc/inetd.conf` 中禁用 `rsh` 或 `rexec` 行。出于安全考虑，你可能希望通过 `/etc/hosts.deny` 文件禁止任何人使用 `rsh` 或 `rexec`，并且只允许在 `/etc/hosts.allow` 文件中明确允许每个服务的 hosts。
- 4. 如果你希望每次启动 `X-Win32` 时自动启动此会话，请单击 `Auto startup` 选项。此外，确保 Windows 设置设置为 `Switch to multiple windows` 选项。
- 5. 输入 X 应用程序将驻留的 Red Hat Linux 服务器的主机名。
- 6. 在 `Login` 字段中输入用户名。如果你选择远程 exec（`rexec`）选项，每次想要连接会话时都会被要求输入密码。如果你更喜欢只输入一次密码，请在 `Password` 字段中输入密码，该字段仅在选择 `rexec` 选项时出现。
- 7. 在 `Command` 字段中输入你想要运行的命令。通常，你希望在这里运行 `xterm`。因此，将此字段设置为此值：
  
  ```
  /usr/bin/X11/xterm -ls -display $DISPLAY.
  ```
- 8. 保存修改后的会话并退出 `X-Util32` 应用程序。

现在，你可以运行新会话了。单击任务栏中的 `X-Win32` 图标，选择 `Sessions` 菜单，然后选择修改后的会话名称。如果你通过 `rexec` 连接，将被要求输入密码。

身份验证成功后，`xterm`（或你在 `X-Util32` 中编辑此条目时在 `Command` 字段中放置的任何应用程序）将出现在你的 MS Windows 系统上。但是，如果你在几秒钟内看不到应用程序，请返回任务栏上的 `X-Win32` 图标，

点击“Show Messages”选项，然后再次尝试运行你的应用程序。注意消息窗口中是否出现任何权限错误。如果确实出现权限错误，要么你忘记在 `/etc/inetd.conf` 中启用 `rexec` 或 `rsh` 服务，要么你忘记在修改 `/etc/inetd.conf` 文件后重启 `inetd` 服务器，要么你尚未为仅 `rsh` 会话设置 `.rhosts` 文件。确保你的 `.rhosts` 文件只能由所有者写入；其他人应仅具有对此文件的只读访问权限。

到此时，你应该已在 Micro `X-Win32` 服务器下运行一个 X Windows 应用程序。如果你希望启动一个 X Windows 管理器，例如 `fvwm2` 或 `openstep`，并像往常一样运行所有 X Windows 应用程序（也就是说，就像你在使用 Red Hat Linux 系统一样），请执行以下操作：

- 1. 使用 `XWin32` 创建或编辑一个会话。输入主机名、登录用户名以及连接方法（`rsh`、`rexec`），如之前所做。选择“Switch to single window”选项并输入以下行作为命令：

```
fvwm2 -display $DISPLAY
```
