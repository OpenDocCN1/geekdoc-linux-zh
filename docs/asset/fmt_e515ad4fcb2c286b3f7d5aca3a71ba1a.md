
表 25-2: CUPS 打印客户端

| 打印管理 | 描述 |
|---|---|
| GNOME Print Manager | GNOME 打印工具 (CUPS)。 |
| CUPS Configuration | 打印、管理和配置 CUPS。 |
| `lpr options` | 打印文件列表，将文件复制到打印机溢空目录并放入队列打印。`-P printer` 在指定的打印机上打印。 |
| `lpq options` | 显示队列中的打印作业。`-P printer` 显示指定打印机的队列。`-l` 打印详细列表。 |
| `lpstat options` | 显示打印机状态。 |
| `lprm options` | 从打印队列中删除打印作业。通过 `lpq` 列出的编号识别特定的打印作业。`-P printer` 删除指定打印机的所有打印作业。 |
| `lpc` | 管理打印机。在 `lpc>` 提示符下，你可以输入命令 |

# lpc

要使用 `lpc`，在 shell 提示符处输入命令 `lpc`。你会得到一个 `lpc>` 提示符，可以在其中输入 `lpc` 命令来管理打印机并重新排序、启用或禁用打印机等。`status` 命令显示打印机是否就绪以及有多少个打印作业。`stop` 和 `start` 命令可以停止打印机并启动它。

```
lpc
```

```
lpc> status myepson
```

```
myperson:
printer is on device 'parallel'
queuing is enabled
printing is enabled
1 entry in spool area
```

# lpq 和 lpstat

你可以使用 `lpq` 和 `lprm` 命令来管理打印。`lpq` 命令列出当前打印队列中的打印作业。通过使用 `-P` 选项和打印机名称，你可以列出特定打印机的作业。如果你指定用户名，可以列出该用户的作业。通过 `-l` 选项，`lpq` 提供关于每个作业的详细信息。如果你想获取特定作业的信息，请配合 `lpq` 使用作业 ID 号。要检查每个作业的状态，请使用 `lpstat`。

```
lpq
```

```
myperson is reading and printing
Rank Owner File(s) Total Size
active chris 1 report 1024
```

# lprm

`lprm` 命令允许你从队列中删除作业，在作业打印之前将其删除。`lprm` 命令具有许多与 `lpq` 相同的选项。要删除某个特定作业，请配合作业号使用 `lprm`。要删除特定打印机的所有打印作业，请使用 `-P` 选项和打印机名称。不带任何选项的 `lprm` 会删除当前正在打印的作业。以下命令删除队列中的第一个作业（使用 `lpq` 获取作业号）。

```
lprm 1
```

# CUPS 管理工具

CUPS 提供了如 `lpadmin`、`lpoptions`、`lpoinfo`、`enable`、`disable`、`accept` 和 `reject` 等命令行工具。`enable` 和 `disable` 命令启动和停止打印队列，而 `accept` 和 `reject` 命令启动和停止特定作业。`lpoinfo` 提供有关打印机的信息，`lpoptions` 你设置选项。`lpadmin` 命令允许你执行添加打印机和更改配置等管理任务。CUPS 管理工具列于表 25-3。

# lpadmin

你可以使用 `lpadmin` 命令设置默认打印机或为打印机配置各种选项。你可以使用 `-d` 选项指定特定打印机作为默认目标（你也可以在 `redhat-config-printer` 中进行）。这里 `myperson` 是默认打印机：

```
lpadmin -d myperson
```

表 25-3：CUPS 管理工具

| 管理工具 | 描述 |
| --- | --- |
| `lpadmin` | CUPS 打印机配置 |
| `loptions` | 设置打印选项 |
| `enable` | 激活打印机 |
| `disable` | 停止打印机 |
| `accept` | 允许打印机接受新作业 |
| `reject` | 防止打印机接受打印作业 |
| `linfo` | 列出可用 CUPS 设备 |

`p` 选项指定要对其设置各种选项的打印机。以下示例设置了打印机描述：
`lpadmin -p mypson -D Epson550`

某些选项允许你控制打印作业的用户队列。`job-count-limit` 设置每个用户允许的作业数量，`job-page-limit` 设置作业的页数限制，`job-quota-period` 限制在特定时间范围内的作业数量。以下命令为每个用户设置了 100 的限制：
`lpadmin -p mypson -o job-page-limit=100`

用户访问控制通过带有 `-u` 选项的 `allow`（允许）或 `deny`（拒绝）列表来确定。允许的访问列在 `allow:` 条目之后，拒绝的访问列在 `deny:` 条目之后。这里允许 `chris` 访问，但拒绝 `aleina` 和 `larisa`。
`lpadmin -p mypson -u allow:chris deny:aleina,larisa`

使用 `all`（所有）或 `none`（无）来允许或拒绝所有或无用户的访问。你可以通过将 `all` 或 `none` 与特定用户的访问结合来创建异常。以下示例允许除 `justin` 外的所有用户访问：
`lpadmin -p mypson -u allow:justin`

# loptions

`loptions` 命令允许你设置打印选项和默认值，这些值主要决定如何打印。`loptions` 让你设置打印机默认默认值。通过 `-P` 选项可以查看打印机选项。`loptions` 允许你通过 `-l` 选项列出可用的 CUPS 设备，其默认设置维护在 `/etc/cups/` 文件中。通过 `-p` 选项列出打印机：
`loptions -p mypson`

通过 `-o` 选项设置打印机选项，例如双面打印。`loptions` 允许你通过 `-d` 选项设置默认值：
`loptions -p mypson -o sides=both`

通过 `-Q` 选项设置打印机选项，例如打印队列优先级：
`loptions -p mypson -o priority=10`

通过 `-m` 选项设置打印机选项，例如纸张：
`loptions -p mypson -o media=A4`

通过 `-n` 选项设置打印机选项，例如分辨率：
`loptions -p mypson -o resolution=600dpi`

通过 `-c` 选项设置打印机选项，例如颜色模式：
`loptions -p mypson -o color=grayscale`

通过 `-f` 选项设置打印机选项，例如打印文件格式：
`loptions -p mypson -o format=pdf`

通过 `-v` 选项设置打印机选项，例如打印横向：
`loptions -p mypson -o orientation=landscape`

通过 `-g` 选项设置打印机选项，例如打印字体：
`loptions -p mypson -o paper=letter`

通过 `-h` 选项设置打印机选项，例如打印页眉：
`loptions -p mypson -o header=on`

通过 `-j` 选项设置打印机选项，例如打印页脚：
`loptions -p mypson -o footer=off`

通过 `-k` 选项设置打印机选项，例如打印水印：
`loptions -p mypson -o watermark=confidential`

通过 `-l` 选项设置打印机选项，例如打印加密：
`loptions -p mypson -o encryption=aes`

通过 `-t` 选项设置打印机选项，例如打印压缩：
`loptions -p mypson -o compression=lzw`

通过 `-u` 选项设置打印机选项，例如打印用户组：
`loptions -p mypson -o group=admin`

通过 `-w` 选项设置打印机选项，例如打印日志：
`loptions -p mypson -o log=verbose`

通过 `-x` 选项设置打印机选项，例如打印超时时间：
`loptions -p mypson -o timeout=300`

通过 `-y` 选项设置打印机选项，例如打印网络地址：
`loptions -p mypson -o network=office`

通过 `-z` 选项设置打印机选项，例如打印打印协议：
`loptions -p mypson -o protocol=ipp`

# enable 和 disable

`enable` 命令启动打印机，而 `disable` 命令停止打印机。你可以使用它们控制打印队列。

```
disable mypson
```

# accept 和 reject

`accept` 命令允许打印机接受新作业，而 `reject` 命令防止打印机接受打印作业。

```
accept mypson
```

# lpinfo

`lpinfo` 命令是一个让你了解可用 CUPS 设备的方便工具。使用 `-v` 选项查看设备，使用 `-m` 选项查看驱动程序。

# 行打印守护进程: LPRng

LPRng 是 Berkeley 打印守护进程 (`lpd`) 的增强版本。它可以处理任何打印机，包括激光、喷墨、PostScript 和针式。`lpd` 守护进程安装并配置在 `/etc/rc.d/init.d` 目录。你使用 `service` 命令启动、停止和重启守护进程：`service lpd`

`lpd` 守护进程由两个配置文件组成：`lpd.conf` 和 `lpd.perms`。`lpd.conf` 包含通用 `lpd` 配置。你使用 `lpd` 设置规则，可以限制主机、用户甚至网络访问。

打印请求由 `lpr` 等打印客户端执行。当文档提交打印时，它会变成一个被放入打印机队列的作业。当作业在队列等待打印时，你可以检查其状态并将其移除。`lpq` 客户端检查打印队列，`lpc` 允许你对其进行更改，而 `lprm` 用于从队列中删除打印作业。

# LPRng 打印客户端

你可以使用多种 LPR 打印客户端来管理打印机或打印机的作业，例如 `Klpq` 以及几种命令行客户端。`Klpq` 是一个 KDE 桌面工具，标记为作业管理工具。在 `Klpq` 中，你可以列出打印机的作业、删除作业并移动到队列顶部。你还可以禁用打印。要让打印队列列表自动更新，你可以在选项中设置更新频率。

# printcap 文件

`/etc/printcap` 文件包含连接到系统的打印机条目。`printcap` 条目包含信息，如打印机缓存目录的路径和用户使用的打印机设备名称。`printcap` 条目的第一个字段是打印机的名称列表。这些是你自己创建的名称，如果你需要也可以添加其他的。每个名称之间用 `|` 符号分隔。当你输入各种打印命令或选项（例如 `-P` 选项）时，使用这些名称来识别打印机。

字段文档列出了打印机不同字段的名称列表。这些字段通过冒号分隔，并使用等号符号赋值。最重要的三个字段是 `lp`、`sd` 和 `if`。`lp` 字段设置为打印机使用的设备名称。`sd` 字段设置为打印池目录，而 `if` 则被设置为用于该打印机的特定过滤程序。某些字段具有布尔值，或仅有字段名而无赋值；参考 `man printcap`。你可以在 `printcap` 手册页中找到 `printcap` 字段的完整列表：`man printcap`。以下是一个 `printcap` 条目的示例：

```
myprinter\myprinter:
:sh=\n:ml=0=\n:mx=0=
:sd=/var/spool/lpd/myprinter=\n:lp=/dev/lp0=
:lpd_bounce=true=\n:if=/usr/share/printconf/mf_wrapper:
```
