
> 注意。左括号后的第一个字符必须是反引号（`）。

在配置文件中，在 `DOMAIN` 定义之后、本地宏定义之前指定 `FEATURE` 定义。

如果你提供了参数，它将用作 `smrsh` 的路径名；否则将使用 `CONFBINDIR` 定义的路径。默认路径为 `/usr/lib/exec/smrsh`。

### 参考表

本节包含了 `sendmail` 命令行参数、配置选项、邮件程序标志和处理选项的参考表。

### 命令行参数

以下章节描述了可以在命令行上使用的 `sendmail` 参数。表 15 简对这些参数进行了简要描述。

表 15 `sendmail` 命令行参数

| 参数 | 说明 |
| --- | --- |
| -bx | 将操作模式设置为 x。操作模式列在下方。 |
| m | 递送邮件 |
| a | 作为守护进程运行。 |
| s | 与 SMTP 通信。 |
| d | 作为守护进程运行。 |
| t | 测试模式。 |
| v | 验证收件者。 |
| i | 初始化数据库。 |
| p | 队列消息。 |
| z | 使用配置文件。 |
| -C | 使用配置文件。 |
| -d | 调试级别。 |
| -f | 使用名称。 |
| -n | 设置名称。 |
| -h | 设置跳数。 |
| -M | 设置消息 ID。 |
| -n | 不允许超过 n 个接收者。 |
| -o | 设置选项值。 |
| -q | 队列消息。 |

### 参考表

表 15 `sendmail` 命令行参数（续）

| 参数 | 说明 |
| --- | --- |
| -r | 检查发送者。 |
| -R | 队列消息。 |
| -t | 运行消息。 |

### 配置选项

表 16 `sendmail` 配置选项

| 选项 | 说明 |
| --- | --- |
| b | 递送邮件（默认）。 |
| e | 回回错误并返回退出状态。 |
| q | 无消息，只返回退出状态。 |
| m | 将错误回给发送者。 |
| w | 写回错误（如果用户未登录）。 |
| f | 在头部开头保存 UNIX 风格的 From 行。 |
| F | 在模式 x 下设置临时队列文件。 |
| g | 将运行邮件程序的默认组 ID 设置为 n。 |
| H | 指定 SMTP 的帮助文件。 |
| h | 设置最大跳数为 n。 |
| i | 忽略输入邮件中的点。 |
| L | 将默认日志级别设置为 n。 |
| m | 即使我在别名展开中，也发送给我。 |
| x | 将宏 x 设置为值。 |
| o | 假设头部可能为旧格式。 |

## 自定义配置文件

表 16 `sendmail` 配置选项（续）

| 选项 | 说明 |
| --- | --- |
| B | 需要时重建别名数据库。 |
| d | 以模式 x 递送。 |
| i | 交互式（同步）递送。 |
| b | 后台（异步）递送。 |
| q | 仅队列消息（在运行队列运行时递送）。 |
| e | 回回错误并返回退出状态。 |
| x | 使用模式 x 处理错误。 |
| p | 打印错误信息（默认）。 |

### 参考表

## 表 16 `sendmail` 配置选项（续）

| 选项 | 描述 |
| --- | --- |
| Pname | 设置本地邮局管理员（postmaster）的名称。如果定义了，来自 `MAILER-DAEMON` 的错误消息将把头信息发送到此名称。 |
| Qdir | 使用 `dir` 变量中指定的目录作为队列目录。 |
| qlimit | 设置在重负载下待队消息的大小限制。默认为 10,000 字节。 |
| Rserver | 远程移动。通过远程 SMTP 服务器投递。默认是 `/var/mail` 的位置。 |
| rtime | 在时间间隔后超时。 |
| s | 在运行任务时保持安全；即即使你打算隐式传递，始终创建队列文件。在任何情况下，`sendmail` 程序在将控制权返回给客户端之前都会创建队列文件。 |
| Sfile | 在名称文件中保存统计信息。 |
| Ttime | 设置队列超时为指定的时间。超过此间隔后，未成功发送的消息将返回给发送者。 |
| un | 设置邮件投递器的默认用户 ID 为 n。在投递器定义中没有 `s` 标志的投递器将以此用户运行。 |
| v | 在详细模式下运行。 |
| Xn | 设置负载平均值，使 `sendmail` 守护进程拒绝传入的 SMTP 连接以减轻系统负载。默认值为 0，禁用此功能。 |
| xn | 设置负载平均值，使 `sendmail` 仅对邮件进行队列（忽略 `dx` 选项）以减轻系统负载。默认值为 0，禁用此功能。 |
| yn | 收件者因子。降低每个收件者指定字节数消息的投递优先级。 |
| Yname | 设置用于别名的 NIS 映射名称。默认是 `mail.aliases`。 |
| Zn | 降低每次投递尝试具有指定字节数消息的投递优先级。 |
| zn | 降低每种类型指定字节数消息的投递优先级。 |

# 自定义 `sendmail` 配置文件

## 邮件投递器标志 (Mailer Flags)

在投递器描述中可以设置的标志见表 17。

## 表 17 在 `sendmail` 邮件投递器描述中可以设置的标志

| 标志 | 描述 |
| --- | --- |
| C | 如果从投递器接收的邮件头信息在被 `ruleset3` 重写后，包含任何不带 `@` 符号的名称，则在后面加上发送者的 `@domain` 子句。 |
| D | 为此邮件投递器设置 `Date:` 头行 |
| E | 转义 `Escape From:` 行以重写为 `>From` |
| e | 尝试避免正常连接，因为此投递器的连接开销较大；在队列运行期间执行任何必要的连接 |
| F | 为此邮件投递器设置 `From:` 头行 |
| f | 为此邮件设置 `-f` 标志，但仅当此操作为网络转发操作时。 |
| h | 为此邮件投递器保留主机名中的大写 |
| L | 按 RFC 821 规定限制行长度 |
| l | 将此投递器设为本地（即执行最终投递）。 |
| M | 为此邮件投递器设置 `Message-Id:` 头行 |
| m | 为此邮件投递器在一次事务中向同一主机上的多个用户发送邮件。 |
| n | 不插入 UNIX 风格的 `From` |
| P | 在调用投递器之前设置 `Return-Path:` |
| p | 总是添加主机名，即使在 `s` 选项已设置的情况下。 |
| r | 与 `f` 相同，但使用 `-r` 标志 |
| S | 在调用投递器之前重置用户 ID。 |
| s | 在调用投递器之前剥离字符 |
| U | 重写为 `>From` 的行 |
| u | 保留名称中的大写 |
| X | 使用 RFC 821 指定的隐藏点算法，用于此投递器。 |
| x | 为此邮件投递器设置 `Full-Name:` 头行 |

# 处理选项

你可以通过命令行使用 `-o` 设置处理选项。如果你想永久设置这些选项，请将它们包含在配置文件中。单字符选项表示...

# 自定义 `sendmail` 配置文件

你可以通过命令行使用 `-o` 设置处理选项。如果你想永久设置这些选项，请将它们包含在配置文件中。单字符选项表示...

取决于选项，值可以是字符串、整数、布尔值（true 或 false）或时间间隔。

多字符选项在前。单字符选项随其后。

## 表 18 `sendmail` 的处理选项

| 别名文件 (AliasFile) | 指定可能的别名。 |
| --- | --- |
| 等待别名 (a) | 在启动前等待 N 分钟使别名存在。N 为分钟。 |
| 允许伪造 HELO (AllowBogusHELO) | 允许不包含主机名的 HELO SMTP 命令。默认禁用此选项。 |
| 自动重建别名 (D) | 必要时重建 `/etc/aliases` 数据库。 |
| 检查间隔 (CN) | 每发送 N 个地址检查点队列。默认值为10。 |
| 类因子 (zfact) | 将指定的因子与类别相乘并从优先级中减去。默认值为1800。 |
| 冒号地址 (ColonAddr) | 将地址中的冒号视为普通字符。 |
| 空格替换 (Bc) | 将空格替换字符设置为 c。默认是空格。 |
| 检查别名 (n) | 在重建数据库时验证别名的右侧（RHS）。 |
| 连接缓存大小 (kN) | 同时打开连接的最大数量。默认值为1。 |
| 连接缓存超时 (timeout) | 设置缓存连接在无活动的情况下允许的最大时间。 |

注意，为了重建数据库，root 必须拥有 `/etc/aliases*` 文件并具有排他写权限。

## 64 自定义 `sendmail` 配置文件

表 18 `sendmail` 处理选项（续）

| | |
| --- | --- |
| | 如果另一端超时，则失败。默认值为 5 分钟。 |
| ConnectionRateThrottling | 设置连接速率节流。 |
| DaemonPortOptions (Ooptions) | 设置服务器 SMTP 选项。 |
| Addr | 地址掩码。默认为 INADDR_ANY。 |
| Family | 地址族。默认为 INET。 |
| Listen | 监听队列的大小。默认为 10。 |
| Port | 监听端口的名称/端口号。默认为 smtp。 |
| ReceiveSize | TCP/IP 接收缓冲区的大小。 |
| DefaultCharSet | 设置将未标记的 8 位输入转换为 MIME 时使用的默认字符集。 |
| DefaultUser (gid) 或 (uuid) | 设置邮件递送程序在 gid 中运行的默认组 ID，或设置邮件递送程序在 uid 中运行的默认用户 ID。 |
| DeliveryMode (dx) | 以模式 x 递送。 |
| i | 交互式递送（同步）。 |
| b | 后台递送（异步）。 |
| d | 延迟模式。 |

## 引用表

# 表 18 `sendmail` 处理选项（续）

| | |
| --- | --- |
| q | 仅将消息放入队列。 |
| DialDelay | 如果连接失败，等待指定的秒数后重试。 |
| DontBlameSendmail | 覆盖文件安全检查。 |
| DontExpandNames | 在基于 DNS 的查找中不扩展 CNAME 记录。 |
| DontInitGroups | 永远不调用 `initgroups(3)` 程序。 |
| DontProbeInterfaces | 不将任何本地接口的名称和地址插入 `=w`。 |
| DontPruneRoutes (R) | 不将 route-addr 语法的地址裁剪到最可能的长度。 |
| DoubleBounceAddress | 在发送错误消息时发生错误，向此地址发送“双重退回”错误消息。 |
| EightBitMode (8) | 使用 8 位数据处理。 |
| mimify | 对 8BITIME 到 7 位进行任何必要的转换。 |

## 自定义 `sendmail` 配置文件

表 18 `sendmail` 处理选项（续）

| | |
| --- | --- |
| pass | 原样传递未标记的 8 位输入。 |
| strict | 拒绝未标记的 8 位输入。 |
| ErrorHeader (Efile/message) | 用斜杠附加错误消息。 |

### 定制 `sendmail` 配置文件

表 18 `sendmail` 处理选项（续）

| 选项 | 描述 |
| :--- | :--- |
| | 隐私侵犯，但它似乎在某些操作系统供应商中很流行。 |
| PrivacyOptions (popt, opt, ... ) | 设置隐私选项。 |
| authwarnings | 在消息中放入 X-Authentication-Warning: 头部。 |
| goaway | 不允许基本上所有的 SMTP 状态查询。 |
| needexpnhelo | 在执行 EXPN 之前强制执行 HELO 或 EHLO 命令。 |
| needmailho | 在执行 MAIL 之前强制执行 HELO 或 EHLO 命令。 |
| needvrfyhely | 在执行 VRFY 之前强制执行 HELO 或 EHLO 命令。 |
| noetr | 完全不允许 ETRN。 |
| noexpn | 完全不允许 EXPN。 |
| norecipepts | 防止回执执。 |
| norvy | 完全不允许 VRFY。 |
| public | 允许开放访问。 |
| restrictmail | 限制 mailq 命令。 |
| restrictqrun | 限制 -q 命令行标记。 |
| QueueDirectory (Qdir) | 使用指定的目录作为队列目录。 |

## 表 18 `sendmail` 处理选项（续）

| 选项 | 描述 |
| :--- | :--- |
| QueueFactor (qfactor) | 使用因子作为 map 函数中的乘数。默认值为 600000。 |
| QueueLA (xLA) | 当系统负载平均值超过 LA 时，仅对消息进行队列。默认值为 8。 |
| QueueSortOrder | 选择队列排序算法。默认值是 Priority。 |
| QueueTimeout (rtime/wtime) | 将队列超时时间设置为 rtime。默认值为五天 (5d)。 |
| RecipientFactor (yfact) | 为每个收件者向优先级添加指定的因子值。默认值为 30000。 |
| RefuseLA (XLA) | 当系统负载平均值超过 LA 时，拒绝入站 SMTP 连接。默认值为 12。 |
| RemoteMode (>RemoteMboxHost>) | 通过此主机启用远程模式。 |
| ResolverOptions (I) | 调整 DNS 查询。 |

### 定制 `sendmail` 配置文件

表 18 `sendmail` 处理选项（续）

| 选项 | 描述 |
| :--- | :--- |
| RetryFactor (Zfact) | 每次处理作业时向优先级添加指定的因子值。默认值为 90000。 |
| RunAsUser | 在读取和交付邮件时变为此用户。 |
| SafeFileEnvironment | 在写入文件之前进入此目录进行 chroot。 |
| SaveFromLine (f) | 在头部前端保存 UNIX 风格的 From: 行。 |
| SendMimeErrors (j) | 以 MIME 格式发送错误消息。 |
| ServiceSwitchFile | 定义服务切换文件的路径。 |
| SevenBitInput (7) | 将输入裁剪为七位。 |
| SingleLineHeader | 将嵌入了换行的 From: 行折叠为单行。 |
| SingleThreadDelivery | 如果此选项和 HostStatusDirectory 选项都已设置，则对其他主机使用单线程交付。 |
| SmtpGreetingMessage or e | 设置初始 SMTP 欢迎消息。 |
| StatusFile (Sfile) | 在指定文件中记录统计信息。 |

## 引用表

表 18 `sendmail` 处理选项（续）

| 选项 | 描述 |
| :--- | :--- |
| SuperSafe (s) | 运行程序时保持超安全。 |
| TempFile (F) | 设置文件模式。 |
| Timeout (timeouts) | 间隔超时。 |
| DataBlock | 数据块。 |
| DataFinal | 数据终结。 |
| FileOpen | 文件打开。 |
| Helo | 回复 HELO 或 EHLO 命令。 |
| HostStatus | 主机重试。 |
| Inect | 首次尝试连接。 |
| Ident | 标识事实风格超时。 |
| Initial | 初始消息。 |
| Mail | 回复 MAIL 命令。 |
| Misc | 回复 NOOP 和 VERB 命令。 |
| QueueTurn | 无法交付。 |
| QueueWarn | 延迟警告。 |

### 定制 `sendmail` 配置文件

表 18 `sendmail` 处理选项（续）

| 选项 | 描述 |
| :--- | :--- |
| Quit | 回复 QUIT 命令 |
| Rcpt | 回复 RCPT 命令 |
| Rset | 回复 RSET 命令 |
| TimeZoneSpec (ttinfo) | 将本地时区设置为 tzinfo。 |
| TryNullMX | 尝试直接发送到主机，仿佛该主机没有 MX 记录。 |

## 引用表（续）

表 18 `sendmail` 处理选项

| 选项 | 描述 |
| :--- | :--- |
| Verbose (v) | 以详细模式运行。 |

## #3
## #规划邮件服务

本章描述了以下四种基础邮件配置，并概述了设置每种配置所需的任务。

- 具有互联网连接并集成集纽器和网关的单一 DNS 域。
- 具有互联网连接和独立网关的单一 DNS 域。
- 具有一个互联网连接的 DNS 域和子域。
- 带有 UU-CP 网关的 DNS 域。

如果你需要建立新的邮件系统或扩展现有系统，可能会发现以下章节对你有帮助。

无论配置如何，要建立一个邮件系统，你都需要以下元素：

- 每个系统上的一个 `sendmail.cf` 配置文件。
- 别名文件（Alias files），每个用户都有一个别名，指向邮件投递的地方。
- 每个用户一个用于存储（或缓存）邮件文件的邮箱（Mailbox）。
- 用于管理邮件服务的管理员的邮局管理员别名（postmaster alias）。

## 规划邮件服务

请参考第 4 章“设置和管理邮件服务”，获取如何设置这些元素的详细信息。

你如何设置配置文件、别名文件以及将邮箱放在哪里取决于你选择的配置。

## 具有互联网连接的单一 DNS Domain

你可以构建的最简单且常见的电子邮件配置类型是具有互联网连接、并作为一个集成邮件中心和网关的系统的单一 DNS 域。为了支持这种简单配置，你只需要两个不同的 `sendmail` 配置文件。

- 一个配置文件用于充当邮件中心和互联网网关的单一服务器。
- 第二个配置文件用于所有其他主机。

在本示例中，域名名为 `starlight.com`，作为邮件中心和网关的系统名为 `mailhost.starlight.com`。所有发出的电子邮件都被重写为看起来来自 `username@starlight.com`。

### 客户端配置

首先创建一个包含以下内容的 `/usr/lib/mail/client.mc` 客户端宏配置文件。

```
