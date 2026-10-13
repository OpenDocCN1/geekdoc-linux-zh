
用户可配置的打印机数据库。

+ `/etc/printers.conf`

系统配置。

+ `$HOME/.printers`

用户可配置的打印机数据库。

+ `/etc/printers.conf`

系统配置。

+ `/etc/printers.conf`

系统配置。

+ `$HOME/.printers`

用户可配置的打印机数据库。

+ `/etc/printers.conf`

系统配置。

+ `/etc/printers.conf`

系统配置...（此处省略重复的路径描述）

+ `/etc/printers.conf`

系统配置。

## Attributes

描述以下内容的：

| Attribute Type | Attribute Value |
| :--- | :--- |
| nobannner | 不随请求打印标题页。此选项可以被 LP 管理员禁用。 |
| nofilebreak | 打印多个文件而不在它们之间插入分页符。 |
| length=number\|number\|number | 以特定长度的页面打印打印请求。以英寸、厘米或行数指定长度。使用数字指定英寸、厘米或行数。在数字后附加字母 i 表示英寸，附加 c 表示厘米。通过指定 number=number 指明行数，例如 number=66 表示单页，length=66 lines 表示长度为 66 行，length=111 表示页面长度为 11 英寸。length=27.94 表示页面长度为 27.94 厘米。不能与 -f 选项一起使用。 |
| width=number | 以特定宽度的页面打印打印请求。以英寸、厘米或列数指定宽度。使用数字指定英寸、厘米或行数。在数字后附加字母 i 表示英寸，附加 c 表示厘米。通过指定 number=number 指明行，例如 number=65 表示页面宽度为 65 列。width=6.5 表示页面宽度为 6.5 英寸。width=10 表示页面宽度为 10 厘米。不能与 -f 选项一起使用。 |
| lpi=number | 以行距为每英寸 number 行打印打印请求。使用数字指定每英寸的行数。不能与 -f 选项一起使用。 |
| cpi=number\|pica\|elite\|compressed | 以字符间距为每英寸 number 个字符打印打印请求。使用数字指定每英寸的字符。使用 pico 将字符间距设为 pica（每英寸 10 个字符），或使用 elite 将字符间距设为 elite（每英寸 12 个字符）。使用 compressed 将字符间距设为打印机能处理的最多个字符。所有打印机没有标准的每英寸字符数；使用 terminfo 数据库（见 `terminfo(4)`）获取你打印机的默认字符间距。不能与 -f 选项一起使用。 |
| tty=stty-option-list | 使用 `stty` 命令有效的选项列表（见 `stty(1)`）打印请求。如果列表包含空格，请用单引号（''）将列表括起来。如果请求了格式且需要使用除 -s 选项指定的字符集或打印轮来打印请求，则拒绝该请求。使用可挂载打印轮或字模盒的打印机在未指定 -s 选项的情况下，将使用打印时挂载的打印轮或字模盒。文件打印后，在用户的终端上写入消息。如果用户未登录，则发送邮件。 |

## 724

- `-y mode-list`

根据 `mode-list` 中列出的打印模式打印请求。`mode-list` 的允许值是本地定义的。只有当有可用过滤器处理它时，你才能使用此选项；否则打印请求将被拒绝。

## Operands

- `file`: 要打印的文件名。使用路径名指定文件，或使用减号 (`-`) 表示标准输入。如果不指定文件，则使用标准输入。

## Usage

`file(5)` 用于描述 `lp` 遇到大于或等于 2 Gbytes（***31 bytes）的文件的行为。

## Exit Status

+ `0`: 成功完成。
- non-zero: 发生错误。

## Files

（此处重复的路径列表已根据要求不重复输出原文，仅保留核心翻译结构）

## lpc 727

将打印机作为原子名称。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

```
enable [all | printer...]
```

启用 `lpr(1B)` 向后台打印队列添加新作业。`all` 对所有本地连接的打印机执行此命令。`printer` 对所有本地特定的打印机执行此命令。将打印机作为原子名称指定。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

```
start [all | printer...]
```

启用打印。为打印机启动后台打印守护进程。`all` 对所有本地连接的打印机执行此命令。`printer` 对所有特定的打印机执行此命令。将打印机作为原子名称指定。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

```
stop [all | printer...]
```

在当前作业完成后停止打印守护进程。在此时禁用打印。`all` 对所有本地连接的打印机执行此命令。`printer` 对所有特定的打印机执行此命令。将打印机作为原子名称指定。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

```
topq [request-ID...] [user...]
```

将 `request-ID` 或属于指定用户的打印机作业移动到打印队列的开头。将用户作为用户名指定。将打印机作为原子名称指定。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

```
up [all | printer...]
```

开启打印机队列并启用。删除打印机状态文件中的消息（由 `down` 插入）。使用 `up` 来撤销 `down` 的效果。`all` 对所有连接的打印机执行此命令。`printer` 对所有特定的打印机执行此命令。将打印机作为原子名称指定。有关原子名称命名规范的信息，请参阅 `printers.conf(4)`。

## 退出状态

`0` 成功完成。

非零 发生错误。

## 文件

```
/var/spool/lp/*
```

LP 打印队列。

## 728

`/var/spool/lp/system/pstatus`

打印机状态文件。

## 属性

有关以下属性的描述，请参阅 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
| Availability (可用性) | SUNWscplp |

## 另见

`echo(1)`, `lpstat(1)`, `lpq(1B)`, `lpr(1B)`, `lrm(1B)`, `lpsched(1M)`, `attributes(5)`

## 诊断

模糊命令

`lpc` 命令或缩写匹配了多个命令。

?无效命令

`lpc` 命令或缩写不被识别。

?需要特权命令

`lpc` 命令或缩写只能由超级用户执行。

`lpc: printer: unknown printer to the print service`

LP 数据库中不存在该打印机对应的打印服务。请检查打印机是否指定正确。使用 `lpstat -p` 或状态命令（参阅 `lpstat(1)`）检查打印机状态。

`lpc: error`

到 `lpsched` 的连接失败。通常意味着打印服务器已崩溃或挂起。使用 `/usr/lib/lp/lpsched` 检查守护进程是否正在运行。

`lpc: Can't send message to LP service`

无法向 LP 服务发送消息。LP 服务已停止。请联系 LP 管理员。

`lpc: Can't receive message from LP service`

从 LP 服务接收到意外消息。软件出现问题。请联系 LP 管理员。

## lpq — 显示打印队列内容

### 概要

```
/usr/ucb/lpq -P destination [-interval][request-ID][user]
```

## 描述

`lpq` 命令显示有关打印队列的信息。打印队列由等待处理打印的打印请求组成。`lpq` 向标准输出显示以下信息：

- 与请求关联的人员用户名。
- 请求在打印队列中的位置。
- 组成请求的文件或文件名称。
- 请求的作业号。
- 请求的文件大小。文件大小以字节为单位报告。

通常，只显示能容一行的信息。如果与请求关联的输入文件名不可，则输入文件指示标准输入。打印客户端按特定顺序要求目标信息。详情请参阅 `printer.conf(4)` 和 `printers(4)`。

## 选项

- `-P destination` 显示打印机或打印机类的信息（参阅 `lpadmin(1M)`）。使用原子、POSIX 风格（server:destination）或联邦命名系统（FNS）指定目标（参阅 .../printer/...names.conf(4) 获取有关原子名称和 FNS 名称命名规范的信息，参阅 `standards(5)` 获取有关 POSIX 的信息）。
- `-l` 以长格式显示信息。长格式包含请求来源的主机名称。
- `-interval` 按特定间隔显示信息。当打印队列为空时停止显示信息。在显示队列前清屏。指定间隔为两次显示之间的秒数。如果未指定间隔，则执行一次。

### 操作数
