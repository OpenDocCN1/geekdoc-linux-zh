
更改默认域名。根据默认和搜索选项，默认域名将附加到查找请求中。如果默认域名包含至少两个部分，则搜索列表包含该默认域名的父级。例如，如果域名是 `CC.Berkeley`，则搜索列表为 `CC.Berkeley, Berkeley.EDU`。使用 `set search` 命令指定不同的列表。使用 `set` 命令显示来自 `hostname`、`/etc/resolv.conf` 或 `LOCAL_DOMAIN` 的 `auth` 值，缩写 = `to`。

将默认名称更改为 `name`，并将域名搜索列表更改为 `name1,name2` 等。最多可以指定六个用斜杠（`/`）分隔的名字。例如，`set search-lists .MIT/EDU/.MIT/EDU` 将域名设置为 `.MIT.EDU`，并将搜索列表设置为这三个名字。此命令覆盖了 `domain` 命令的默认名称和搜索列表。使用 `set` 命令显示列表。（默认 = 基于 `hostname`、`/etc/resolv.conf` 或 `LOCAL_DOMAIN` 的值，缩写 = `schrl`）

如果设置，则将域名附加到单组件查找中（即不包含点的查找）。（默认 = `defname`，缩写 = `[no]def`）。

如果查找请求包含至少一个点，则搜索域名列表，直到收到以点结尾的答案。（默认 = `search`，缩写 = `[no]search`）。

将 TCP/UDP 名称服务器端口更改为 `value`。（默认 = `53`，缩写 = `port.`）。

将信息查询类型更改为以下之一：

- `A`: 主机的互联网地址。
- `CNAME`: 别名的规范名称。
- `HINFO`: 主机的 CPU 和操作系统类型。
- `MJFO`: 邮箱或邮寄列表信息。
- `MX`: 邮件交换器。
- `NS`: 指定域名的名称服务器。
- `PTR`: 如果查询是互联网地址，则返回主机；否则指向其他信息的指针。
- `SOA`: 域的“权限起始”信息。
- `TXT`: 文本信息。
- `INFO`: 用户信息。
- `WKS`: 支持的已知服务。

其他类型（`ANY`, `AXFR`, `MD`, `MF`, `NULL`）在 RFC-1035 文档中描述。（默认 = `A`，缩写 = `q, ty`）。

告诉名称服务器查询是否拥有该信息。（默认 = `recurse`，缩写 = `[no]recurse`）。

将重试次数设置为 `number`。当在一定时间内（通过 `set timeout` 修改）未收到请求时，超时时间将翻倍并重新发送请求。重试值控制在放弃之前重新发送请求的次数。（默认 = `4`，缩写 = `ret`）。

# overchan

1353

```
root=host
timeout=number
[novc]
[noignore]
```

更改根服务器的名称为 `host`。这会影响 `root` 命令。（默认 = `ns.internic.net.` 缩写 = `.ro`）
将等待回复的初始超时更改为 `number` 秒。每次重试都会超时时间翻倍。（默认 = `5` 秒，缩写 = `t.i`）
在向服务器发送请求时始终使用虚拟电路。（默认 = `novc`，缩写 = `[no]vc`）
忽略数据包截断错误。（默认 = `noignore`，缩写 = `[no]ig`）。

## 诊断

如果请求未成功，将打印错误信息。可能的错误有：

- `Tim out`（超时）：服务器在一段时间（通过 `set timeout=value` 修改）和经过多次重试（通过 `set retry=value` 修改）后未响应。
- `No response from server`（服务器无响应）：名称服务器运行在服务器上。
- `No records`（无记录）：服务器没有当前主机查询的资源记录，尽管主机名是有效的。通过 `set querytype` 命令指定查询类型。
- `Non-existent domain`（不存在的域名）：主机或域名不存在。
- `Connection refused`（拒绝连接）：当前无法连接到 finger 服务器。此错误常见于 it 和 finger 请求。
- `Network is unreachable`（网络不可达）：名称服务器在其数据库中发现内部不一致，无法返回有效答案。
- `Server failure`（服务器故障）：名称服务器拒绝提供服务。
- `Refused/Format error`（拒绝/格式错误）：名称服务器拒绝请求包格式不正确。这可能表明 `nslookup` 存在错误。

# 文件

- `/Et/Resol.Conf`
- `$HOME/.nslookuprc`
- `/usr/share/misc/nslookup.help`

初始域名和名称服务器地址。
用户的初始选项。
命令摘要。

## 环境

- `HOSTALIASES` 包含主机别名的文件。
- `LOCALDOMAIN` 覆盖默认域名。

# 另请

`resolver(3)`, `resolver(5)`, `named(8)`, RFC 1034 “域名 – 概念与设施,” RFC 1035 “域名实现与规范”

## 作者

Andrew Cherenson

1990年6月24日

# overchan

`overchan`—通过数据库更新新闻。

# 第八部分：管理与特权命令

`overchan`—通过数据库更新新闻。

用法 `[d] [c]`

## 描述

`overchan` 读取输入或数据库。对于每个条目，它会更新数据库。如果未指定输入，则从标准输入读取。数据库通过 `-d` 标志指定。默认数据库为 `/var/spool/overchan`。

## 选项

- `-d file`: 指定要更新的数据库。默认是 `/var/spool/overchan`。
- `-c`: 按字母顺序排序输出。
- `-m`: 按名称过滤输出。
- `-p price`: 指定要更新的价格。
- `-r`: 反转排序顺序。
- `-s`: 汇总输出。

# 另请

`resolver(5)`

# 第八部分：管理与特殊命令

```
uidrange range[range]...
```

写入 `/etc/pnfsd.conf` 文件。在这里，每个范围的格式为 `uid` 或 `uid-uid`，表示包含性范围。

# 打印

`pnfsd` 支持基于使用 NFS 将实际打印数据从客户端传输到服务器的打印模型。客户端系统使用 `PNFDS_PR_INT` 或 `PGN_PR_INT` 请求，该请求请求客户端可以使用的且由 NFS 导出的溢打印目录的路径。`pnfsd` 为其每个客户端创建一个子目录：父目录是 `user:///pool/pnfs`，子目录是客户端系统的主机名。如果你想使用不同的目录，应该在 `/etc/pnfsd.conf` 文件中添加一行：

```
spooldir path
```

一旦客户端使用 NFS 挂载了溢打印目录并将数据传输到该目录，它就会发出 `PNFDS_PR_START` 或 `PNFDS2_PR_START` 请求。`pnfsd` 通过根据服务器操作系统的打印服务构建命令，并使用 PC 用户的身份执行命令来处理这些以及其他相关请求。由于这涉及用户 ID 权限，`pnfsd` 必须以 root 身份运行。

每个打印请求都包含要使用的打印机名称。在 Linux 中，此名称对应 `/etc/printcups/5` 数据库中的打印机定义。如果你想定义非标准的数据处理方式，你应该定义一个新的打印机并安排客户端打印到那里。设置新打印机有两种方法。第一种是在 `/etc/printcups/5` 中添加条目并创建执行所需处理的过滤器。这不在本文讨论的范围内。此外，`pnfsd` 有一种机制，你可以仅通过 `/etc/pnfsd.conf` 文件中以下格式的行来定义虚拟打印机：每个打印机由以下行定义：

```
printer name alias-for command
```

`name` 是你想定义的打印机名称。`alias-for` 是对应此打印机的“真实”打印机名称。例如，当 `name` 翻译为对应打印机 `alias-for` 的相应请求时，显示队列的请求。如果你定义打印机的方式没有其对应的“真实”打印机，请在该字段中使用单个的 `-`。（参见打印机测试的定义以获取示例。）`command` 是当在 `name` 上打印文件时执行的命令。该命令由 shell `/bin/sh -c` 执行执行。

考虑以下示例：`/etc/pnfsd.conf` 文件：

```
printer test 1w /usr/local/bin/encrypt -r $FILE
printer test /usr/bin/cp $FILE/$HOSTUB
```

如果客户端将作业提交到 `rotated` 打印机，将调用 `encrypt` 工具来预处理 `$FILE`。在这种情况下，`-r` 选项会导致文件在默认的 PostScript 打印机上以双列格式打印。如果客户端请求 `rotated` 打印机的打印列表，`pnfsd` 守护进程将其翻译为对打印机名称的列出请求。

`printer test` 仅用于测试。发送到此打印机的任何文件都会复制到 `/usr/tmp`。对 `printer test` 的队列查询、状态检查等请求都会被拒绝，因为 `alias-for` 被指定为 `-`

# 重新配置
