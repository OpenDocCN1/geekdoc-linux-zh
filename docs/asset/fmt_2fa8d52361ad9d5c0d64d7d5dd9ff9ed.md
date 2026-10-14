
某些命令参数允许你指定所有空闲打印机，或指定一个或多个打印机变量来指示特定的打印机。

表 8-3 列出了命令行参数。

| 表 8-3: lpc 参数 |
| lpc 参数 | 说明 |
|---|---|
| help [argument] | 打印 `lpc` 命令的行描述。如果未指定参数，则显示参数列表。 |
| ? [argument] | 与 `help` 同。 |
| abort | 终止活动的 `lpd` 守护程序并禁用打印。 |
| check | 检查每个打印机文件和其他组件 |
| clean | 从打印池目录中删除临时文件、数据文件和控制文件（例如不构成打印作业的文件）。 |
| disable | 关闭指定的打印队列，禁用打印并在打印状态中输入指定的消息。如果打印机离线，`lpc` 命令指示打印机离线。 |
| enable | 启用指定打印机的池化。允许 `lpr` 或 `lp` 命令作业进入池区。 |
| exit | 退出 `lpc`。 |
| quit | 退出 `lpc`。 |

表 8-3: Lpc 参数（续）

| Lpc 参数 | 说明 |
|---|---|
| restart | 尝试为指定的打印机启动新的 `lpd` 守护程序。如果某些异常导致守护程序意外终止并将作业留在队列中，此参数非常有用。发生这种情况时，`lpq` 命令指示不存在守护程序。如果守护程序忙，你需要杀死进程并重启守护程序。 |
| start | 为指定的打印机启用打印并启动打印池守护程序。 |
| status [printer] | 显示指定打印守护程序和队列的状态。显示启用、队列项数以及守护程序状态。如果没有提供打印机名称，则显示所有打印守护程序和队列的信息。 |
| stop | 在当前作业完成后停止打印池守护程序并禁用打印。 |
| topq printer | 按指定顺序将作业放入队列。你可以通过指定 `request_ID` 变量或用户名变量来指定打印作业。 |
| up | 启用所有打印并启动新的打印守护程序。取消 `down` 参数。 |

以下示例显示打印机 `tester` 上运行 `lpd` 守护程序且队列中有一项：

```
# /usr/sbin/lpcnpc status tester

tester:

    打印机位于设备 '/dev/tty02' 速度9600

    队列已启用

    打印已启用

    池区 1 项
```

`lpc>` 更多信息请参阅 `lpc(8)`。

## 8.4.5 启用打印机计费

打印机计费允许你对打印服务收费，并确定打印机的使用量。

### 注意

计费仅适用于未格式化的文本文件；不适用于诸如 PCL 和 PostScript 等预格式化文件。

打印机计费有两种类型：

- 打印机用户计费：打印机用户计数根据发布打印请求的系统和用户名提供打印机使用信息。
- 打印机摘要计数：打印机摘要计数提供有关打印机产生的介质数量（打印页数或卷纸/胶片长度等）的信息。通过带有 `-s` 选项的 `pac` 命令来生成打印机摘要计数信息。

打印机计数文件默认位于 `/var/adm` 目录。使用 `lprsetup` 命令添加打印机会创建您指定的计数文件。`/usr/adm/lpd/lpacct` 是默认的计数文件。

`printconfig` 工具在“高级选项”中提供默认的计数文件。如果您不需要计费，可以在配置打印机期间或之后的任何时候使用 `Modify` 选项删除这些条目。如果您手动添加打印机，则必须手动创建计数文件。

### 注意

用户 `admin` 所有 `/var/adm/lpd` 目录，该目录属于 `ad` 组。用户 `admin` 也拥有打印机计数文件，其保护模式为 644 且系统 组。

在打印机的 `/etc/printconfig` 条目中，`af` 参数指定计数文件的名称。计费进程使用此文件记录每个用户在打印机上打印的页数。对于系统中的每台打印机，计数文件的名称都是唯一的。使用 `pac` 工具显示打印机计数文件中的信息。用户 `daemon` 拥有计数文件并是 `daemon` 组成员。如果您使用 `printconfig` 工具指定打印机计数文件，系统会自动设置正确的文件所有权。

计费通过称为打印过滤器（print filters）的程序实现。`printconfig` 工具建议了一个默认的打印过滤器。计费需要 `ifprint` 符号。例如：

`if=/usr/bin/ln03rof`

如果您想为系统上的每台打印机分离计数文件，请确保文件名是唯一的。无限数量的打印机可以共享一个计数文件，但您无法为远程打印机指定计数文件。打印守护进程（daemon）拥有计数文件。如果您指定了计数文件，系统将根据需要自动创建中间目录。

# 8.5 参考信息

以下章节讨论了配置打印机、行打印守护进程（lpd）以及打印系统文件所需的信息。如果按照第 8.3.2 节所述使用 `printconfig`，系统会自动创建文件。

您也可以手动创建和修改文件。如果这样做，您还必须手动更改 `/etc/printcap` 文件以便更改生效。

## 8.5.1 /etc/printcap 文件

`lpd` 守护进程使用 `/etc/printcap` 数据库文件中的信息处理打印请求。`/etc/printcap` 文件中的每个条目都描述了一个打印机。您使用两个字母缩写的符号（symbols）来指定打印机特性。这些符号在本节以及 `printcap(4)` 中进行了描述。`lprset` 工具用于修改 `/etc/printcap` 文件。

默认打印机名为 `lp`，它可以作为任何类型（本地或远程）打印机的别名。`lp0`、`lp1` 等是 `printconfig` 提供的默认打印机名称。您可以根据需要使用它们或忽略它们。

以下示例显示了 TCP/IP 连接的打印机、LPD 远程打印机、串口打印机和并行打印机的 `/etc/printcap` 条目。

### TCP/IP 连接的打印机示例

```
lp0|myprinter:hp=8000:\n  :t=tcp:\n  if=/usr/bin/ppddof+PageSize=Letter +Chplj8000.rpd:\n  if=/usr/bin/adm/lp0err:\n    lp=#myprinter.com/9100:\n    :mx=0:\n    rof=/usr/bin/ppddof+PageSize=Letter +Chplj8000.rpd:\n    :pl=66:\n    :pw=0:\n  :rw:\n    sd=/usr/spool/lpd0:\n    xf=/usr/bin/xf:
```

### LPD 远程打印机示例

```
lp0|remote:\n  :lf=/usr/adm/lp0err:\n  :lp=\n  :rm=system:\
  :rp=queue:\n  :sd=/usr/spool/lp0d:
```

### 注意

此配置中的大多数 printcap 选项均已禁用

### 串口示例

```
lp0|myprinter|la75:\n  :af=/usr/adm/lp0acct:\n  :br=9600:\
  :ct=dev:\n  :fc=0177777:\n  :fs=0:\n  :if=/usr/bin/la75of:\n  :lf=/usr/adm/lp0err:\n  :lp=dev/tty00:\n  :mx=0:\n  :of=/usr/bin/la75of:\n  :pl=66:\n  :pw=80:\n  :rw=/usr/spool/lp0d:\n  :xc=0177777:\n  :xf=/usr/bin/xf:
```

### 并行打印机示例

```
lp0|myprinter|la75:\n  :af=/usr/adm/lp0acct:\n  :br=9600:\
  :ct=dev:\n  :fc=0177777:\n  :fs=0:\n  :if=/usr/bin/la75of:\n  :lf=/usr/adm/lp0err:\n  :lp=dev/tty00:\n  :mx=0:\n  :of=/usr/bin/la75of:\n  :pl=66:\n  :pw=80:\n  :rw=/usr/spool/lp0d:\n  :xc=0177777:\n  :xf=/usr/bin/xf:
```
