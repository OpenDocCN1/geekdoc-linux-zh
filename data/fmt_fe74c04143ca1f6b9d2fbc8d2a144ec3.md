
你可以将此类命令放在 `.login` 中以便自动执行。同样，请将 `name` 替换为你终端的相应名称。例如，如果你正在使用控制台和 `tcsh`（`tcsh` 提示符为 `>`），请执行以下命令设置你的终端类型：

```bash
> setenv TERM linux
```

## 12. 如何将文件发送到打印机？

大多数 Linux 系统至少有一个打印机用于制作纸质副本。通常，你可以使用 `lpr` 实用发送到打印机。如果你的系统有多个打印机，你需要使用 `lpr` 的 `-P` 选项来请求特定的打印机。请参阅第 43 页的“使用 lpr 打印文件”。

## 我的登录名是什么？929

图 B-1 标准键盘（由 Maxi Switch, Inc. 感谢）

## 13. 我的登录名是什么？

这是你用于向 Linux 标识身份的名称。这也是其他用户向你发送电子邮件的名称。如果你是第一次登录自己的个人 Linux 系统，你将以 `root` 登录并为用户创建一个登录账户。请参阅第 616 页的“添加和删除用户账户”。确保你尽快以自己的名字登录，并根据需要成为 `root` 或超级用户（Superuser）。以 `root` 身份运行有许多危险。请参阅第 582 页的“系统管理员与超级用户”。

## 14. 我的密码是什么？

在具有多个用户或连接到网络的系统中，密码可以防止他人访问你的文件。首先，系统管理员会为你分配一个密码。在你自己的系统中，你在设置账户时会给自己分配一个密码。你可以随时更改密码（见第 23 页）。

## 15. 哪个键结束了一行？

不同的键盘使用不同的键将光标移动到下一行的开头。本书始终将结束一行的键称为 `RETURN` 键。你的终端键盘可能有 `RET`、`NEWLINE`、`ENTER`、`RETURN` 或其他键。某些终端使用带有带有弯曲箭头的键。（带有弯曲箭头的键不是箭头键。箭头键的轴线是笔直的。）图 B-1 显示了一个标准键盘。

## 附录 B：帮助！

## 16. 哪个是擦除键？

Linux 下默认的擦除键是 `BACKSPACE`。此键将回退并擦除你刚刚输入的字符，一次一个。如果此键不起作用，请使用 `CONTROL-H`（在按住 `CONTROL` 或 `CTRL` 键时按 `H`）。如果这两个键都不能擦除字符，请参阅第 867 页，查看如何确定哪个是你的擦除键以及如何将其更改为更方便的键示例。

## 17. 哪个是行删除键？

通常，删除你正在输入的整行的键是 `CONTROL-U`。此键被称为行删除键（line kill）或简单称为 `kill`。请参阅第 867 页，查看如何确定哪个键是你的行删除键以及如何更改它的示例。

## 18. 哪个键中断执行？

中断你运行的几乎任何程序的默认键通常是 `CONTROL-C`。其他系统可能使用 `DELETE`（或 `DEL`）键。请参阅第 867 页，查看如何确定哪个是你的键。

## 19. 我的终端的 Termcap 或 TermInfo 名称是什么？

中断你运行的几乎任何程序的默认键通常是 `CONTROL-C`。其他系统可能使用 `DELETE`（或 `DEL`）键。请参阅第 867 页，查看如何确定哪个是你的键。

## 20. 我将使用哪个 Shell？

中断你运行的几乎任何程序的默认键通常是 `CONTROL-C`。其他系统可能使用 `DELETE`（或 `DEL`）键。请参阅第 867 页，查看如何确定哪个是你的键。

# 用于 linux-msdos/vger.rutgers.edu 的错误、补丁与新代码

已安装 DPMI 服务器版本 0.9

启动 MS-DOS...

[Linux 文件系统]驱动器 D: 是目录 `/`

[已安装 dosemu 0.52 EMS 4.0 驱动]

[欢迎使用 dosemu 0.63!]

```
C:\dir/w
```

```
C 驱动器的卷为 doseMU49
卷序列号为 374A-09CF
C:\ 目录：

BOOTOFF.COM   EXITEMU.COM   CONFIG.SYS     EMUFS.SYS      AUTOEXEC.BAT

BOOTON.COM    CONFIG.BAK     AUTOEXEC.BAK VGAON.COM      VGAOFF.COM

LREDIR.EXE     DOSDBG.EXE     PDIPX.COM       LANCHECK.EXE   ISEMU.COM

EJECT.COM     SPEED.COM      DOSDBG.COM      LREDIR.EXE      MGARROT.COM

MOUSE.EXE     UNIX.COM       DUMPCONF.EXE   CHDIR.EXE      GETCHWD.EXE

SYSTEM.EXE    CDROM.SYS      EMS.SYS        COMMAND.COM    [JURASSIC]

             30 个文件     216.989 字节

                             749.568 字节可用
```

```
C:\>
```

图 C-1 在 X Window 系统下的 xterm 窗口中运行的 dosemu 模拟器

- `-C` 导致 DOS 从 C 硬盘启动。这可以是一个真实的 DOS 磁盘分区，也可以是一个磁盘镜像文件，取决于 `/etc/dosemu.conf` 中的设置。
- `-c` 如果 DOS 设置为 root 的 setuid，在 Linux 控制台下运行时使用此选项将导致 DOS 使用直接视频以提高性能。如果 dosemu 视频没有设置妥当，此选项可能会导致您的 Linux 系统崩溃。
- `-k` 导致 dosemu 使用原始键盘输入，而不是 Linux 操作系统提供的任何映射。当直接在 Linux 控制台上运行时，您可以使用此选项。
- `-V` 启用允许从 Linux 控制台访问某些 VGA 优化功能。

如果你不使用 `-A` 或 `-C` 选项，dosemu 将根据 `/etc/dosemu.conf` 文件中的设备列表作为启动设备启动。在 dosemu 运行期间，你可以输入 DOS 命令并运行 DOS 程序。如果你在 Linux 控制台上运行，仍然可以切换到另一个虚拟控制台；例如，`CONTROL-ALT-F2` 会将你切换到控制台二。如果你在窗口中运行 dosemu，你可以在其他窗口中继续进行活动。你甚至可以启动多个 dosemu 副本，每个副本都运行在自己的 xterm 窗口中。

## 附录 C：模拟器

图 1 显示了在 X Windows 系统下的 xterm 窗口中运行的 dosemu。由于 xterm 是单色窗口，显示内容为黑白。

使用 `-C` 命令来启动 dosemu。在这里，dosemu 被配置为从一个像 DOS 的磁盘镜像启动，因为这是一个较小的硬盘。正如 DOS 命令 `dir/w` 所示，此磁盘镜像文件中仅提供了几个命令。Linux 文件系统的根目录被提供为 DOS 磁盘 D:。这让你能够访问 Linux 文件系统上的所有文件，就像访问你在 Linux 下挂载的任何 DOS 分区一样。

在图 C-2 中，用户利用了 `lredir`，它将 DOS C 盘从磁盘镜像重定向到 Linux 下挂载为 `/dos` 的 DOS 分区。现在，DOS C 盘就是这个硬盘分区。`dir/w` 命令现在显示此磁盘分区中的文件。通过仔细设置，你可以配置 dosemu 在启动 dosemu 时自动执行 `lredir`，但在此阶段尝试使用 `lredir` 之前，你应该是 DOS 的精通用户，并仔细阅读 dosemu 的说明。

![](img/939921397ef655bc55c88108788663a7_983_0.png)

图 C-3 在 DOS 程序中运行的 dosemu

```
$ lredir: linux/dos

$ LINEXFS:/dos write READ/WRITE

$ cd/w

/dos 中的 C 盘卷

C: 目录：

nMSDOS.SYS [DOS] GUMP91X.ZIP COMMAND.COM

AUTOEXEC.BAT [EGAFNT] AUTOEXEC.EXE EXTIEM.COM

WIN.BAT [WINDOWS] CONFIG.SIT EDIT.G

COMMAND.COM [16-000] IO.SYS..OLD

MSDOS.EAT [C1492] DOS.EXE PARMPT.EXE

REHI.EXE [C1492] FORMAT.COM CHKDSK.EXE

WINDIR.EXE [C1827] HELP.EXE COPY.EXE

NHCUP.BAT [C1492] (PIP) (POLL)

60 个文件

527,528 字节可用
```

图 C-2 dosemu：运行 lredir

![](img/939921397ef655bc55c88108788663a7_983_1.png)

图 C-3 显示在彩色 xterm 窗口中运行 Turbo for DOS 的 dosemu。运行 dosemu 允许 DOS 程序使用颜色，但在 xterm 窗口或彩色 xterm 窗口中都无法进行图形工作。如果你在 Linux 控制台上直接运行 DOS，那么你可以配置 dosemu 为自定义 DOS 程序提供高级图形能力。要停止模拟器，请使用在系统首次构建和安装 dosemu 时安装的特殊命令 `exit`。

另一个正在进行的项目是 Windows 模拟器，或称为 `wine`。虽然这仍在进行中，但 `wine` 允许 DOS 程序使用颜色，但在 xterm 窗口或彩色 xterm 窗口中都无法进行图形工作。如果你在 Linux 控制台上直接运行 DOS，那么你可以配置 dosemu 为自定义 DOS 程序提供高级图形能力。要停止模拟器，请使用在系统首次构建和安装 dosemu 时安装的特殊命令 `exit`。（注：此处原文似乎存在重复内容，已按要求逻辑翻译）

```
$ lredir: linux/dos

$ LINEXFS:/dos write READ/WRITE

$ cd/w

/dos 中的 C 盘卷

C: 目录：

nMSDOS.SYS [DOS] GUMP91X.ZIP COMMAND.COM

AUTOEXEC.BAT [EGAFNT] AUTOEXEC.EXE EXTIEM.COM

WIN.BAT [WINDOWS] CONFIG.SIT EDIT.G

COMMAND.COM [16-000] IO.SYS..OLD

MSDOS.EAT [C1492] DOS.EXE PARMPT.EXE

REHI.EXE [C1492] FORMAT.COM CHKDSK.EXE

WINDIR.EXE [C1827] HELP.EXE COPY.EXE

NHCUP.BAT [C1492] (PIP) (POLL)

60 个文件

527,528 字节可用
```
