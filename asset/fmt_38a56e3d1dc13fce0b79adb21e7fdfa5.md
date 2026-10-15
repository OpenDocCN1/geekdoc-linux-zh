
### 列表 10.4：列出打印队列

```
lpc-tqqq lp 840

Printer: lprobin

lpc: selected 'sara@robin+840'

lprobin.foobirds.org: started

lpc-tqqq lpq

Printer: lprobin 'Canon'

Queue: 3 printable jobs

Server: pid 1830 active

Spooler: pid 1831 active

Status: waiting for subscriber to exit at 11:35:55.158

| Rank | Owner/ID | Class | Job | Files | Time |
| --- | --- | --- | --- | --- | --- |
| 1 | sara@robin840 | A | 840 | rev.txt | 833 | 11:35:00 |
| 2 | root@robin829 | A | 829 | ndc.txt | 344 | 11:35:00 |
| 3 | ed@robin842 | A | 842 | conf.txt | 399 | 11:35:27 |

lpc-exit
```

在列表 10.4 中，使用 `lpq` 命令列出 `lpr` 队列的内容。当显示队列时，作业号列在“job”标题下。`topq` 命令将指定的作业移动到所选打印队列的顶部。第二个 `lpq` 命令显示作业 840 是排队等待打印的第一作业。

列表 10.4 所示的 `lpq` 命令实际上是一个独立命令；它不需要在 `lpc` 会话内部运行。可以从命令行请求作业列表。`-P` 命令行参数选择显示哪台打印机。以下是显示打印机 `hp` 队列的示例：

```
[root# -lpq

Printer: lprobin

Queue: 3 printable jobs

Server: pid 1369 active

Spooler: pid 1420 active

Status: waiting for subscriber to exit at 11:28:39.365

| Rank | Owner | Class | Job | Files | Time |
| --- | --- | --- | --- | --- | --- |
| 1 | root | A | 368 | conf.txt | 399 | 11:28:16 |
| 2 | alana@robin+395 | A | 395 | ndc.txt | 344 | 11:28:31 |
| 3 | tyler@robin+421 | A | 421 | rev.txt | 833 | 11:28:39
```

这是在 `lpc` 内部相同的队列。

`lpc` 并不是唯一可以在 `lpc` 外部使用的命令。`lprm` 命令也是一个独立命令。使用 `lprm` 删除队列中的作业。作业可以由所有者或 `root` 用户删除。假设 `alana` 想要删除上一个示例中显示的作业号 395。她输入了列表 10.5 所示的命令。

### 列表 10.5：从打印队列中删除作业

```
$ lprm -Plp 395

Printer: lprobin:

checking perms 'alena@robin+395'
```

### 使用 Samba 共享打印机

第 9 章展示了如何使用 `Samba` 软件包让 `Linux` 服务器成为 `SMB` 服务器，并展示了如何使用 `Samba` 共享文件。第 9 章没有显示的是，`Samba` 也可以用于与 `SMB` 客户端共享打印机。在这里，你将看到如何实现这一点。

首先，当然，你需要确保系统中安装了 `Samba`。（详情请参阅第 9 章。）安装 `Samba` 后，通过 `smb.conf` 文件配置共享打印机。

#### 在 smb.conf 文件中定义打印机

理解 `smb.conf` 配置文件的最佳方法是查看一个运行正常的示例。带有预配置 `smb.conf` 的红帽（`Red Hat`）系统包含了共享打印机的支持。红帽 `smb.conf` 文件中的活动行所示列表 10.6。

列表 10.6：带有打印机共享功能的 `smb.conf`

```
[global]

workgroup = MYGROUP

server string = Samba

printcap name = /etc/printcap

load printers = yes

printing = lpr

log file = /var/log/samba/log

max size = 0

security = user

encrypt passwords = yes

smb passwd file = /etc/samba/smbpasswd

socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192

proxy = no

[homes]

comment = Home Directories

browsable = no

writable = yes

valid users = *

create mode = 0664

directory mode = 0775

[printers]

comment = All Printers

path = /var/spool/samba

browsable = no

guest ok = no

writable = no

printable = yes
```

你可能在第 9 章见过这些行，因此你已经知道如何将 `workgroup` 选项更改为网络正确的工作组名称，并将 `server string` 更改为描述服务器的有意义的内容。然而，这些行中的某些在该章节中并未介绍。打印机共享行位于全局部分：

- `printcap name`: 定义 `printcap` 文件的位置。
- `load printers`: 告诉系统是否将 `printcap` 文件中的所有打印机作为共享打印机提供。默认值是 `yes`，这意味着如果未指定 `no`，则所有打印机必须单独定义。在列表 10.6 中，此项设置为 `yes`。
- `printing`: 指定服务器使用的打印系统。`Samba` 支持的打印系统包括：`BSD`, `AIX`, `LPR`, `SYS`, `HPU`, `QNX`, `SOL`，以及 `CUPS`。红帽使用 `LPR`。在列表 10.6 中，此项设置为 `yes`。

#### printers 机 部分

`printers` 部分的功能与 `homes` 部分类似，它为用户提供主目录。`printers` 部分定义为使所有打印机可用：

```
[printers]

comment = All Printers

path = /var/spool/samba

browsable = no

guest ok = no

writable = no

printable = yes
```

你可能在第 9 章见过这些行中的某些部分，因此你已经知道如何将 `workgroup` 选项更改为网络正确的工作组名称，并将 `server string` 更改为描述服务器的有意义的内容。然而，这些行中的某些在该章节中并未介绍。

- `printcap name`: 定义 `printcap` 文件的位置。
- `load printers`: 告诉系统是否将 `printcap` 文件中的所有打印机作为共享打印机提供。默认值是 `yes`，这意味着如果未指定 `no`，则所有打印机必须单独定义。在列表 10.6 中，此项设置为 `yes`。
- `printing`: 指定服务器使用的打印系统。`Samba` 支持的打印系统包括：`BSD`, `AIX`, `LPR`, `SYS`, `HPU`, `QNX`, `SOL`，以及 `CUPS`。红帽使用 `LPR`。在列表 10.6 中，此项设置为 `yes`。

这些行用于准备服务器共享打印机，并自动共享 `printcap` 文件中的打印机。除了这些全局行外，还有一个标记为 "printers" 的部分。

`printers` 部分的功能与 `homes` 部分类似，它为用户提供主目录。`printers` 部分被定义为使所有打印机可用：

```
[printers]

comment = All Printers
```
