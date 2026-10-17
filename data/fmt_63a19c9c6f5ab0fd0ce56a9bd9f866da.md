
当你选择 Continue 时，你会看到 CUPS 中定义的所有打印机的列表。你选择应包含在正在定义的类中的所有打印机。然后选择 Continue。确认页面显示类已成功完成。如果通过单击页面顶部的 Classes 返回到 Classes 页面，你会看到你的类显示出来，其选项与普通打印机的大部分相同，只是图标显示多个打印机，并且许多按钮不同。图 12-16 显示了 Classes 页面。

![](img/43f64015de86d989e30eff5bb284fb96_578_0.png)

图 12-16 CUPS 配置中的 Classes 页面

用户仍可以将打印作业发送到属于类的单个打印机（例如前例中的 lexmark2）。但类提供了一种在繁忙网络且有多用户和多台打印机的情况下更有效地分配打印作业的方法。

## 管理打印

你在第 3 章中学习了如何从命令行提交打印作业。从图形应用程序打印甚至更简单：你通常从 File 菜单中选择 Print，并在出现的对话框中选择 Print。

尽管提交打印作业很简单，但作为系统管理员，你可能会花费大量时间管理打印。打印机有许多活动部件，比计算机内部的任何东西更容易出现故障。打印还会消耗纸张和墨粉等资源，即使系统正常工作也必须补充。（一些公司指定一名员工负责这些事情，而不管理打印的其他方面。）由于所有这些原因，许多组织制定打印策略：简要说明打印资源如何使用以及打印机应如何管理的规则声明。

Linux 包含多个用于帮助你管理打印资源的实用程序。其中之一是 `lpc` 实用程序。此命令行实用程序让你控制 LPRng 或 CUPS 打印，指定如何接受和处理打印作业。

> 许多 Linux 系统管理员更喜欢使用本节后面描述的图形实用程序之一，而不是 `lpc`。

尽管在第 3 章中并不明显，Red Hat Linux 和 Fedora 使用一种替代打印系统，该系统根据你使用的打印系统将输入的命令映射到不同的程序：LPRng 或 CUPS。你可以使用 `alternatives` 命令查看和配置此系统。实际的符号链接维护在 `/etc/alternatives` 目录中。`lpr` 命令和 `lpc` 命令实际上都是符号链接。例如，`lpc` 命令是 `/etc/alternatives/print-lpc` 的链接，后者又指向 LPR 或 CUPS 打印系统的适当控制程序。在 Fedora Core 2 中，此链接引用的默认控制程序是 `/usr/sbin/lpc.cups`。如果切换到 LPRng 打印系统，链接将被更改，这在 Fedora 中是不寻常的，因为更新的 CUPS 系统是默认设置。LPR 和 CUPS 的控制程序提供类似的功能，但作用于不同的底层系统。

使用 `lpc` 你可以：

- 阻止新打印作业被打印队列接受。
- 阻止打印作业被发送到打印机。
- 取消当前正在打印的打印作业。
- 查看任何打印机的状态（例如它是否已启用，对应的打印队列是否包含任何打印作业，或当前文档已发送到打印机的程度）。

你必须以 root 用户身份登录才能使用 `lpc`。你可以将 `lpc` 命令作为参数包含在命令行中。此命令显示默认打印机的状态：

```
## lpc status
```

你也可以交互式地使用 `lpc` 来输入多个命令。要开始以交互模式使用 `lpc`，请在不带任何参数的情况下输入实用程序名称：

```
## lpc
lpc>
```

表 12-1 列出了你可以在 `lpc` 提示符下使用或作为 `lpc` 命令的参数使用的命令（如果你不希望对某些任务使用交互模式）。

对于所示的每个命令，`lpc` 作用于默认打印机（`printcap` 文件中列出的第一个打印机），除非你指定打印机名称。例如，如果 `printcap` 中的第一台打印机是 `hp`，使用此命令会关闭 `hp` 打印机：

```
## lpc down
```

如果 `printcap` 文件包含另一个名为 `stylus` 的打印机定义，你可以使用此命令关闭 `stylus` 打印机：

```
## lpc down stylus
```

### 表 12-1 lpc 命令

| Command | Description | Example (noninteractive mode) |
|---|---|---|
| help | Display a list of all lpc commands | lpc help |
| status | Display status of the lpd printer daemon and the print queue indicated (or the default if none is indicated) | lpc status |
| abort | Cancel the print job currently being printed (use the start command to restart printing) | lpc abort |
| stop | Stop sending print jobs to the printer after the current print job has finished printing | lpc stop |
| start | Start sending print jobs to the printer (used after abort or stop) | lpc start |
| disable | Prevent users from submitting new print jobs | lpc disable |
| enable | Allow users to submit new print jobs | lpc enable |
| down | Stop sending print jobs to the printer and prevent new print jobs from being submitted (equivalent to using stop and disable) | lpc down |
| up | Begin sending print jobs to the printer and allow new print jobs to be submitted (equivalent to using start and enable) | lpc up |

### 表 12-1 lpc 命令（续）

| Command | Description | Example (noninteractive mode) |
|---|---|---|
| exit or quit | Exit the lpc program | Used only in interactive mode |
| restart | Attempt to restart the lpd printer daemon (equivalent to using the command `/etc/rc.d/init.d/lpd restart`) | lpc restart |
| clean | Remove any temporary, data, or control files that could not be printed | lpc clean |
| topq | Move a print job to the top of the named print queue; this command requires a printer name (where the print job is placed) and the print job number (which you can obtain using the `lpq` command) | lpc topq hpj 16 |

在使用任何 `lpc` 命令（`topq` 除外）时，你可以使用 `all` 指代所有打印机。例如，要完全关闭打印，以便无法提交任何打印作业，并且在当前打印作业完成后所有打印都停止，请使用此命令：

```
## lpc down all
```

> 注意 你之前学习的 `lpr` 命令使用 `-P` 参数来定义打印机名称。对于 `lpc` 命令，你只需将打印机名称作为附加参数添加。

图 12-17 说明了一些关键 `lpc` 命令如何影响打印过程。图中使用的相同术语也在 `lpc` 手册页和图形打印管理工具中使用。

![](img/43f64015de86d989e30eff5bb284fb96_581_0.png)

图 12-17 使用 `lpc` 控制打印过程

你也可以使用 `lpstat` 命令来快速查看每台打印机正在执行的操作。

## 跟踪打印作业

要查看默认打印队列中的打印作业，请输入命令 `lpq`。`lpq` 实用程序列出打印队列中的每个打印作业，并提供以下信息：

- 打印作业的状态，例如 `active`（正在打印）、`ready` 或 `error`
- 所有者（提交打印作业的用户）
- 打印作业的类别（其优先级；通常为 `A`，除非使用 `lpr` 命令的 `-C` 选项）
- 打印服务器分配的作业编号
- 文件的大小（以字节为单位，即字符数）
- 打印作业提交的时间
