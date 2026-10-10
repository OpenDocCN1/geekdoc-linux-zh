
# 第四部分 OpenLinux 网络与服务器设置

## 第20章 设置邮件服务器

`MatchGECOS` 选项让 `sendmail` 将邮件发送到根据 `/etc/passwd` 文件中 `GECOS` 字段指定的用户全名的转换形式。例如，如果用户 `wharris`（根据 `GECOS` 字段）的全名是 Wayne Harris，则可以收到 `wharris@mybox.com`、`Wayne_Harris@mybox.com` 或 `Wayne.Harris@mybox.com` 的邮件。该选项不推荐，因为它可能导致歧义，并且用户可能会更改其 `GECOS` 字段，从而绕过 `sendmail` 的常规投递机制。

### 跳数设置
下面的行涉及跳数：
- 最大跳数
```
O MaxHopCount=17
```
`MaxHopCount` 选项指定在消息从一台机器传输到另一台机器之前允许的最大 hop 数（即消息传输的次数），超过该数值后消息将返回给发送者并被视为无法投递。默认值为 17。

### 帮助文件设置
下面的行涉及 `sendmail` 帮助文件：
- 帮助文件位置
```
O Helpfile=/usr/share/sendmail/sendmail.hf
```
`Help` 选项列出包含在线帮助文本的文件名。要查看这些数据，请执行 `telnet localhost 25` 命令并输入 `help`。
> **注意**：`Help` 还可用于大多数 SMTP 命令，使用 `help` 命令并通过帮助命令名称来调用。

### 点作为终止符设置
下面的行涉及点作为终止符：
- 忽略入站消息中的点作为终止符
```
O IgnoreDots
```
`IgnoreDots` 选项决定当 `sendmail` 收到包含行内点 (`.`) 的消息时的行为。如果该选项不存在、被注释或设为 `False`，单个点被视为消息结束（符合 `RFC 821` 的行为）。如果设为 `True`，点则不具有特殊意义。

### 解析器选项设置
下面的行涉及解析器选项：
- 名称解析器选项
```
O ResolverOptions=+AAONLY
```
`ResolverOptions` 用于调节 DNS 查找的行为。可用标志的描述可在 `resolver` 主页面（输入 `man resolver`）查阅。

### MIME 错误设置
下面的行涉及 MIME 错误：
```
# 发送封装在 MIME 中的错误消息？
O SendMimeErrors=True
```
`SendMimeErrors` 定义送达状态通知消息是否应进行 MIME 编码（`True`）或保持为纯文本（`False`）。

### 转发文件搜索路径设置
下面的行涉及用于转发电子邮件消息的搜索路径：
```
# 转发文件搜索路径
O ForwardPath=$z/.forward.sw=$z/.
```
`ForwardPath` 选项指定个人用户转发文件的搜索路径。在上一行中，`$z` 表示用户的主目录，而 `$sw` 表示本机的主机名。例如，如果 `/home/kzabon` 是用户 `kzabon` 在本机的主目录，`sendmail` 会先查找 `/home/kzabon/.forward_al`，然后查找 `/home/kzabon/.forward`。如果两个文件都不存在，邮件将投递到 `/var/spool/mail/kzabon` 的收件箱中。

### 连接缓存设置
下面的行涉及在打开连接时如何使用缓存：
```
# 打开连接缓存大小
O ConnectionCacheSize=2
# 打开连接缓存超时
O ConnectionCacheTimeout=5m
```
与其它方式不同，打开连接、发送消息、关闭连接，再重新打开连接到同一主机，连接缓存允许在同一台机器上通过单一连接发送多条消息。`ConnectionCacheSize` 选项可以降低创建和销毁连接的开销。默认值 `2` 表示最多可保持两个同时连接。`ConnectionCacheTimeout` 指定连接可以保持的最大时间。默认值为 `300s`，即 `5m`（5 分钟）。

### 主机状态目录和线程投递设置
下面的行涉及主机状态目录和线程投递：
```
# 持久化主机状态目录
O HostStatusDirectory=.hoststat
# 单线程投递（需要 HostStatusDirectory）？
O SingleThreadDelivery
```
`HostStatusDirectory` 可以建立一个目录（相对于队列目录 `/var/spool/mqueue`，如果未指定完整路径），用于存储 `sendmail` 已建立连接的所有机器的状态信息。该选项默认未设置，因为其实现消耗资源，但可能收益不大。

### Errors-To 头行设置
下面的行涉及 `Errors-To` 头行：
```
- Errors-To: 头行？
O Errors-To=False
```
`ErrorsTo` 选项允许使用或忽略 `Errors-To:` 头行。如果设为 `True`，任何投递错误都将报告到头行中指定的地址。否则，该行将被忽略。默认设置为 `False`，因为这违反了 `RFC 1123-Internet Hosts` 要求。
> 请求注释（`RFC`）是涵盖 Internet 主题的文档：从最严格的协议和服务要求到轻松的 Internet 主题（例如如何将咖啡壶连接到 Internet）。可以说，如果没有 `RFC`，Internet 上的许多位置将不会存储 Internet `RFC`。请尝试访问 `RFC` 编辑器页面（`http://www.rfc-editor.org`）或 Internet `RFC` 档案（`http://www.faqs.org/rfc-faqs/`）开始查找 `RFC`。

### 日志级别设置
下面的行涉及日志级别：
```
# 日志级别
O LogLevel=9
```
`LogLevel` 选项设置向 `syslog` 设施发送消息的优先级和严重程度。值从 `0`（仅报告严重错误）到 `9`（记录最大调试信息，以及所有重要消息）。除非您需要在查找邮件投递问题时查看大量调试信息，默认值 `9` 提供了合适的详细程度。

### 消息发送给发送者设置
下面的行涉及消息如何发送给发送者：
```
# 即使在别名展开时也发送给我？
O MeToo
```
`MeToo` 选项决定当消息发送者同时也是邮件列表的分发列表成员时的行为。除非指定为 `True`，否则发送者不会收到该消息（基于假设：如果发送者编写了消息，则不需要查看它）。

### 地址评估设置
下面的行涉及地址的评估：
```
# 验证 newaliases 中的右侧？
O CheckAliases=False
```
如果设为 `True`，`CheckAliases` 选项会评估冒号左侧的地址，并保证右侧地址有效的投递代理。默认值为 `False`。

### 旧式头设置
下面的行涉及旧式头：
```
# 默认使用旧式头，如果没有特殊标点？
O OldStyleHeaders=True
```
最初，收件人列表由空格分隔。最近，由于收件人经常包含空格，使用了逗号。当设为 `True` 时，`OldStyleHeaders` 选项允许逗号分隔的列表，但未加引号的空格会被转换为逗号。如果设为 `False`（默认），未加引号的空格会被转换为 `BlankSub` 选项所指定的字符。

### SMTP daemon 选项设置
下面的行涉及 SMTP daemon 选项：
```
# SMTP daemon 选项
O DaemonPortOptions=Port-esmtp
```
`DaemonPortOptions` 可用于限制 `sendmail` 监听的端口号和网络，同时到达的连接数量，以及 TCP/IP 发送和接收缓冲区的大小。

### 隐私设置
下面的行涉及隐私：
```
# 隐私标志
O PrivacyOptions=authvarnings
```
`PrivacyOptions` 选项可用于要求 incoming connections 严格遵守正确的 SMTP 行为，禁用 `EXPN`（展开）或 `VRFY`（验证）标志，禁用返回运行，并限制可以运行 `mailq -q` 命令的用户。`mailq` 命令显示队列中的所有条目，而 `sendmail -q` 命令同步处理队列。上一行启用使用 `"X-Authentication-Warning: header line"`。

## 第20章 设置邮件服务器

### 错误消息副本设置
下面的行涉及错误消息的副本：
```
# who (if anyone) should get extra copies of error messages

#0 PostMasterCopy=Postmaster
```
`PostMasterCopy` 选项可以指定一个地址（或多个），这些地址应接收发送给消息发送者的任何投递状态通知的副本。默认是不发送任何副本。

### 邮件队列设置
下面的行涉及邮件队列：
```
# slope of queue-only function

#0 QueueFactor=600000
```
```
# queue directory

O QueueDirectory=/var/spool/queue
```
`QueueFactor` 等参数的段落。

随后是超时行。

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于`理查德·费曼`，诺贝尔物理奖得主。

1. 运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，`难以遗忘`。

```
if (condVar > someVal) {console.log("xxx")}
```
