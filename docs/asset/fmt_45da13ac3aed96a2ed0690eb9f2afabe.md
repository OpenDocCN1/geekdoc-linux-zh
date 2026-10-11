
```
john@4nx.vms.com:~home/john
File Sessions Options Help
# dir sys$system:decw*
DIRECTORY SYS$COMMON:[SYSEX]
DECW$BOOKREADER,EXE:1      DECW$CALC,EXE:1       DECW$CALENDAR,EXE:1
DECW$CARDFILE,EXE:1      DECW$BI,EXE:1         DECW$CLOCK,EXE:1
DECW$DWT,EXE:1           DECW$INT_FONT_DAEMON,EXE:1
DECW$DWT_XDRIVER,EXE:1 DECW$MSESSION,EXE:1
DECW$COMPILER,EXE:1     DECW$MAIL,EXE:1
DECW$MESSAGEPANEL,EXE:1  DECW$MEMMAP,EXE:1
DECW$OVERLAY,EXE:1      DECW$NOTEPAD,EXE:1     DECW$PAINT,EXE:1
DECW$PUZZLE,EXE:1       DECW$REINIT,EXE:1      DECW$SCREEN,EXE:1
DECW$SEEKVER,EXE:1      DECW$SERVER_QUICK,EXE:1
DECW$SESSION_MAIN,EXE      DECW$SETSHODIS,EXE:1  DECW$PVRM,EXE:2
DECW$STARTLOG,EXE:1      DECW$TABLE,EXE:1       DECW$TERMINAL,EXE:1
DECW$TERMINAL_CREATE,EXE:1 DECW$UILMOTIF,EXE:1  DECW$WML,EXE:1
DECW$TERFORM,EXE:1      DECW$WINDOW,EXE:1
DECW$ACUST,EXE:1        DECW$WSINIT,EXE:1      DECW$XFS,EXE:1
Total of 37 files.
#
```

> 图 5-5 标准 VMS X Windows 应用程序位于 SYSTEM 目录。

与它们的 Linux Windows 对应程序。这些程序可以通过输入以下命令定义显示器后运行：

```
RUN SYS$SYSTEM:DECW$CLOCK.EXE
```

`RUN/DETACH SYS$SYSTEM:DECW$CLOCK.EXE` 会为您的程序创建一个分离进程以便运行，并将您带回终端窗口的 `$` 提示符以执行更多命令！

关于 DECwindow 应用程序：某些应用程序非常直观（例如 `DECW$CLOCK`），但另一些则并不那么清晰。`DECW$TERMINAL`、`DECW$WINMGR` 等程序似乎可以启动窗口管理器或创建新的终端（以及进程）。事实上，这正是这些程序的功能，但它们通过 VMS 启动程序访问，以便在 VMS 服务器上运行 Windows；而另一些则被 VMS 命令行解释器用于创建终端或启动 X 窗口；这类似于 Linux 上的 `xinit` 或 `xbfconfig`。

> 注意：不要直接运行窗口管理器程序，因为它们可能会搞乱你在两台机器上的 Windows 会话！

快速访问 OpenVMS Windows 应用程序的一种简单方法是使用 `DECW$SESSION.EXE` 或 `DTSESSION.EXE` 会话管理器。`DECW$SESSION` 是较旧的 Windows 会话管理器

![](img/3ba916f144e94350147c366c3485e02e_63_0.png)

图 5-6 使用此 VMS 命令文件，你可以轻松自动化你的显示器和 X Windows 命令。默认设置会启动非常实用的 DECwindow 会话管理器。

第 5 章 – X Windows 应用程序：X Windows 与 VMS 和 Linux 的互操作性 63

![](img/3ba916f144e94350147c366c3485e02e_64_0.png)

图 5-7 那么这有什么用呢？让我们看看菜单。

![](img/3ba916f144e94350147c366c3485e02e_64_1.png)

图 5-8 现在，你可以创建需要的所有 VMS 终端，检查正在进行的 X Windows 任务状态，或者更改你的 X Windows 安全或启动选项——这一切只需点击鼠标，且完全可以在你的 Linux 设备的显示上完成！

![](img/3ba916f144e94350147c366c3485e02e_64_2.png)

图 5-9

Linux & OpenVMS 互操作性

图 5-10 但如果你想从此菜单中启动自己的命令或 X Windows 应用程序怎么办？使用“Menu Control”窗口中 Options 下拉菜单上的 Menus 按钮。

图 5-11 创建你的新命令/菜单选项（VMS 命令文件或可执行文件），并将其添加到相应的下拉菜单。

第 5 章 – X Windows 应用程序：X Windows 与 VMS 和 Linux 的互操作性 65

![](img/3ba916f144e94350147c366c3485e02e_66_0.png)

图 5-12 然后只需点击你的下拉菜单即可！

![](img/3ba916f144e94350147c366c3485e02e_66_1.png)

图 5-13 嘿！这些 VMS 应用程序和菜单是从哪里来的！我以为这是一台 Linux 机器！

66 Linux & OpenVMS 互操作性

注意，所有这些应用程序都同时来自 VMS CDE/DTSESSION 管理程序，此时 `DECW$SESSION` 管理程序和 Linux KDE 会话管理器也在运行！请小心，因为现在任何会话管理器都可以让你注销。

## 在 OpenVMS 上显示你的 Linux Windows 应用程序

在 20 世纪 80 年代，当 VMS 工作站还是尖端技术时，你的桌子上可能有一台 VMS 工作站。Alpha 工作站同样可能使用 Linux 或 True-64。OpenVMS PC 同样可能运行 Windows，而今天的 Linux 或 Windows 显卡可能比三年前 Alpha 工作站的显卡好得多。X Windows 的妙处在于，你不再限于自己的电脑或旧显卡；你可以限制显示器来享受应用程序！

但假设你足够幸运，你的桌子上有一台运行最先进的 VMS 工作站（而不是房间里的 GS320 集群），而你的 Linux 机器显卡有点老化了。你可以简单地将你的 Linux 应用程序重定向到新的 OpenVMS 显示器。过程与 VMS 类似，只是命令必须重定向到 VMS 工作站。首先，你必须授权 VMS 使用 TCP/IP 作为 X Windows 的传输（进入 VMS），因为默认是不开启的。你或你的 VMS 管理器应该添加此行：

```
SYS$MANAGER:DECW$SERVER.COM
```

如果你不方便修改此文件，可以将定义放在 `SYS$MANAGER:STARTUP_VMS.COM` 中。我把它放在 `DECW$SERVER.COM`，因为 TCP/IP 应该是默认开启的（带安全）！

![](img/3ba916f144e94350147c366c3485e02e_68_0.png)

图 5-14 不要以此方式修改此文件，否则可能会可能会不稳定。

现在让 VMS 工作站上使用 VMS 会话管理器（见图 5-15）。

![](img/3ba916f144e94350147c366c3485e02e_68_1.png)

图 5-15 点击 Security 按钮，你将进入授权框。

![](img/3ba916f144e94350147c366c3485e02e_68_2.png)

图 5-16 点击 Add，你就可以填写 Linux/UNIX 信息。对于 TCP/IP 传输，用户名始终使用 `"*"`，否则无法工作（图 5-17 至 5-19）！

68 Linux & OpenVMS 互操作性

![](img/3ba916f144e94350147c366c3485e02e_69_0.png)

图 5-17 你现在准备好 `telnet` 到你的 Linux 系统并发送 X Windows 应用程序了。

![](img/3ba916f144e94350147c366c3485e02e_69_1.png)

图 5-18

![](img/3ba916f144e94350147c366c3485e02e_69_2.png)
