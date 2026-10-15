
`lpstat` 命令显示打印机状态。`lpstat` 的 `-p` 选项限制输出仅显示打印机及其可用性。`lpstat` 的 `-D` 选项显示该打印机的描述（如果有）。你应该看到看到所示的输出：

printer p04 is idle. enabled since Sat Aug 23 16:32:49 1998. available. Description:

printer p08 is idle. enabled since Thu Aug 21 16:28:28 1998. available. Description: Laser III by copy room

printer p206 is idle. enabled since Sat Feb 14 16:50:49 1999. available. Description: HP LaserJet in Accting

# 打印文件和管道 第 8 章

## 启用与接受
每个置空程序或打印队列都可以由管理员设置为接受或拒绝用户的请求。如果置空程序长时间停止服务，则会被设置为拒绝。管理员可以设置物理打印机设备的启用或禁用打印。例如，禁用某个设备是为了停止打印以修复卡纸。置空程序仍然可以接受用户请求，一旦打印机再次启用即可进行打印。

前面的示例显示有三个可用打印机名称：`p104`、`p108` 和 `p206`。它们目前都处于空闲状态，这意味着它们没有在打印任何作业。没有一个被禁用（例如，没有一个在维修）。

## 打印文件或管道
有两个通用命令处理文件或管道：

- `lp`（系统实用程序）
- `lpr`（BSD 实用程序）

你应该学习这两种样式，以便在 UNIX 下工作。

### UNIX 置空也适用于网络打印机
你可以在本节中使用 `lp` 或 `lpr` 命令打印到网络打印机。系统管理员必须先配置这些打印机以便它们出现。

在最简单的情况下，你可以直接给 `lp` 或 `lpr` 提供文件列表，如下：

```bash
lp file!
lpr file!
```

在这些示例中，文件将在系统管理员设置的任何默认打印机上打印。如果没有设置系统默认值，这两个命令都会报错。这这些命令有两个重要的选项：
`lp -dlaser2 -n3 file1 file2`
`lpr -Plaser -n3 file1 file2`

在前面的示例中，`lp -d` 选项和 `lpr -P` 选项允许指定打印机。你在上一节中见过如何列出可用打印机。

置空系统使用接口脚本传递给打印机。不同的脚本可能允许唯一的字母和参数。在 System V UNIX 上，你通常可以在以下目录找到接口脚本：

`/usr/spool/lp/admin/lp/interfaces`

每个脚本的名字与其控制的打印机相同。读取脚本以查看是否有可以尝试的有用选项。例如，你可能会发现你的打印机脚本支持这些选项：

- `o landscape`
- `o nobanner`
- `o nb` (no banner)
- `o raw` (发送原始输出)

你的 `lp` 或 `lpr` 命令将排队输出请求。你应该看到为你的（合并）输出显示一个请求 ID，以便你可以跟踪作业是否已经打印，并在在需要时取消打印，如下：

```bash
$ ls -l | lp -n2
request id is hp-85 (standard output)
```

系统 `lp` 命令有一个 `-c` 选项，如果你打印一个文件并立即删除它，就必须注意这一点。`lp` 命令通常排队文件名。如果在你的作业打印之前还有几个作业，那么你的作业打印可能需要一段时间。如果你在打印之前修改或删除了文件，这将影响打印内容。`-c` 选项强制 `lp` 在运行时复制文件，这样后续对文件的更改就不会影响输出：

```bash
lp -c file1
```

表 8.11 显示了 `lp` 和 `lpr` 命令的其他属性。

# 第二部分
打印文件与流水线 第 8 章

## 表 8.11 ip 和 lpr 命令的其他属性

| 属性 | 参见页码 |
|---|---|
| 允许相对路径和绝对路径参数 | 70 |
| 处理文件名参数或标准输入 | 115 |
| 允许文件名列表和文件名通配符 | 292 |

## 检查打印队列
在 System V UNIX 上，你可以通过不带任何参数输入 `lpstat` 来检查打印队列中的请求，例如所示：

```
$ lpstat
hp-85 mori 111946 Feb 23 22:03 on hp
hp-86 fred 203 Feb 23 22:04
$
```

> `lpstat` 仅限于你的请求
> 在 UNIX 系统上，`lpstat` 只会显示你自己的正在排队的打印任务。如果你在队列中只看到自己的任务，请记住前面可能有你看不见的大型打印任务。

`lpstat` 输出的每行都以打印任务请求 ID 开始，该 ID 以打印机名称开头。在前面的示例中，Fred 和 Mori 同时为打印机 `hp` 排队了打印任务。由于 Mori 先来，所以他的任务在 `hp` 上排队。即使 Fred 的任务很小（203 个字符），他的任务也不会等到 Mori 的任务完成后才开始。

如果你的系统不支持 `lpstat`，请尝试 `lpq` 获取特定打印机的排队打印任务列表。在下面的示例中，你使用 `-P` 参数指定所需的打印机，并添加 `-l` 获取更详细的输出：

```
$ lpq -P sp7
Queue Dev Status Job Name From To
Submitted Rnk Pri Blks Cp
sp7 lp7 RUNNING 713 STDIN.41278 dooreen doreen
07/19/1999 11:32:18 1 15 2 1
/var/pool/qdaemon/t5pEtua
QUEUED 717 STDIN.37282 dick
07/19/1999 11:33:22 2 15 2 1
/var/pool/qdaemon/tbnAia
```

## 第二部分 与 UNIX文件操作

## 第 8 章 显示和打印文件与流水线
如果你的系统中没有 `lpc`，请尝试 `lpc`。进入 `lpc` 后，有用的命令有 `help`、`status` 和 `quit`：

```
$ lpc
lpc- help
命令可以缩写。命令：
abort enable disable help restart status topq ?
clean exit down quit start up
lpc- status
lpc:
	queuing enabled
printing is enabled
no entries
no daemon present
lpc- quit
$
```

## 取消打印任务
在 System V UNIX 上，你可以通过请求 ID 号来取消打印任务。如前一节所示，使用 `lpstat`、`lpq` 或 `lpc` 命令来确定你想要取消的哪个当前打印请求，例如所示：

```
$ lpstat
hp-85 mori 111946 Feb 23 22:03 on hp
hp-86 fred 203 Feb 23 22:04
$ cancel hp-85
request "hp-85" canceled
$ lpstat
hp-86 fred 203 Feb 23 22:04 on hp
$
```

在 BSD UNIX 上，使用带有任务号的 `rm` 来移除（即取消）当前打印请求。

在 AIX UNIX 上，使用 `qcan` 取消打印请求，例如所示：

```
qcan -P printername -x jobid
```

在所有系统中，非 root 用户只能取消他们提交的任务；root 可以取消任何打印任务。

## 第二部分
打印文件与流水线 第 8 章

## 从故障打印机移动打印请求
如果打印机出现故障，系统管理员（root）可以使用 `lmove` 命令将该打印机的某些或所有待处理打印请求移动到另一个打印机。

要将一个或多个特定的打印任务移动到另一个打印机，root 可以输入语法：
`lpmove list-of-req-ids new-printer`

要显示指定打印机的所有用户的待处理打印任务请求 ID，root 可以输入语法：

```
lpstat -p printer-name
```
