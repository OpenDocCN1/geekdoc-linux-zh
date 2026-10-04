
# 第 21 章 exim4：设置邮件服务器、客户端及更多

## 快速上手 I：配置 exim4 使用智能主机

要设置您的服务器，您需要更改 `/etc/exim4/update-exim4.conf`（第 766 页）中几个配置变量的值并重启 `exim4`。`dpkg-reconfigure` 实用（第 768 页）将引导您编辑此文件；本快速上手使用文本编辑器。在 root 权限下，使用文本编辑器对 `update-exim4.conf` 进行以下更改：

```
dc_eximconfig_configtype='smarthost'
smarthost='mail.example.net'
```

### 配置类型

将 `dc_eximconfig_configtype` 变量设置为 `smarthost`，使 `exim4` 将发往非本地系统的邮件发送到 `smarthost` 配置变量指定的。此行应与上一页显示的完全相同。

### 智能主机

当 `dc_eximconfig_configtype` 设置为 `smarthost` 时，`smarthost` 是 `exim4` 用于中继邮件到非本地系统的远程 SMTP 服务器（智能主机）的全域名（FDN）或 IP 地址（首选）。将 `mail.example.net` 替换为此 FDN 或 IP 地址。对于 `update-exim4.conf` 中的布尔变量，`exim4` 将 `""` 指定的空值解释为 `false`。进行这些更改后，文件应该如下所示：

```
$ cat /etc/exim4/update-exim4.conf

...\dc_eximconfig.configtype='smarthost'
dc_other_hosts='
dc_local_interfaces='127.0.0.1'
dc_remotehosts='
dc_domains='
dc_relay='
dc_minimaldns='false'
dc_relay_nets='
dc_smarthost='mail.example.net'
FILEMODE='644'
dc_split_mailname='false'
dc_hide_mailname='false'
dc_mailname_in_oh='true'
dc_localdelivery='mail_spool'
```

`exim4` 服务器在智能主机配置中不使用 `dc_local_interfaces` 变量的值，因此您可以将其留空。然而，在其他配置中，`127.0.0.1` 的值防止 `exim4` 接受来自非本地系统的电子邮件。建议以此方式配置 `exim4`，仅在您准备好接受其他系统的邮件时才更改此变量。

为了减少 DNS 查找的访问访问（如果您使用的是拨号线路，这可能很有帮助），请将 `dc_minimaldns` 变量的值更改为 `true`。

### /etc/mailname

`/etc/mailname` 文件最初持有存储在 `/etc/mailname` 中的服务器字符串节点名称 (`-n`)。该字符串出现在本地系统发送的邮件的 `envelope-from` 和 `From` 行中，作为发送系统的名称。如果您希望邮件看起来像是来自不同的系统，可以修改此文件的内容。您可以使用文本编辑器修改此文件；`dpkg-reconfigure` 实用也可以更改它。

以下文件会导致从本地系统发送的邮件看起来像是来自 `username@example.com`，其中 `username` 是发送邮件的用户名：

```
$ cat /etc/mailname
example.com
```

有关 `exim4` 配置变量的更多信息，请参阅第 766 页。完成这些更改后，重启 `exim4`（第 757 页）。

### 测试 exim4

使用以下命令测试 `exim4`：

```
$ echo "test" | exim4 user@remote.host
```

将 `user@remote.host` 替换为您想要接收测试邮件的电子邮件地址。

## 快速上手 II：配置 exim4 发送和接收邮件

* 接收来自本地系统的电子邮件并投递到本地系统。
* 接收来自本地系统的电子邮件并投递到非本地系统，使用 SMTP 服务器（智能主机）——通常是 ISP——来中继邮件并发送到其目的地。
* 不投递来自非本地系统的电子邮件。通常情况下，您需要使用 POP 或 IMAP 来接收电子邮件。
* 不转发来自非本地系统的电子邮件到其他非本地系统（不中继邮件）。

要设置您的服务器，您需要更改 `/etc/exim4/update-exim4.conf`（第 766 页）中几个配置变量的值并重启 `exim4`。`dpkg-reconfigure` 实用（第 768 页）将引导您编辑此文件；本快速上手使用文本编辑器。在 root 权限下，使用文本编辑器对 `update-exim4.conf` 进行以下更改：

```
dc_eximconfig_configtype='smarthost'
smarthost='mail.example.net'
```

`exim4` 服务器在智能主机配置中不使用 `dc_local_interfaces` 变量的值，因此您可以将其留空。然而，在其他配置中，`127.0.0.1` 的值防止 `exim4` 接受来自非本地系统的电子邮件。建议以此方式配置 `exim4`，仅在您准备好接受其他系统的邮件时才更改此变量。

为了减少 DNS 查找的访问访问（如果您使用的是拨号线路，这可能很有帮助），请将 `dc_minimaldns` 变量的值更改为 `true`。

### /etc/mailname

`/etc/mailname` 文件最初持有存储在 `/etc/mailname` 中的服务器字符串节点名称 (`-n`)。该字符串出现在本地系统发送的邮件的 `envelope-from` 和 `From` 行中，作为发送系统的名称。如果您希望邮件看起来像是来自不同的系统，可以修改此文件的内容。您可以使用文本编辑器修改此文件；`dpkg-reconfigure` 实用也可以更改它。

以下文件会导致从本地系统发送的邮件看起来像是来自 `username@example.com`，其中 `username` 是发送邮件的用户名：

```
$ cat /etc/mailname
example.com
```

有关 `exim4` 配置变量的更多信息，请参阅第 766 页。完成这些更改后，重启 `exim4`（第 757 页）。

## exim4 的工作原理

`exim4` 接收电子邮件，来自本地和非本地系统，它在 `/var/spool/exim4/input` 创建文件，在 `exim4` 处理期间持有这些邮件。为了识别特定的邮件，`exim4` 生成一个 16 字符的 ID 并使用与邮件相关的字符串。`exim4` 守护进程将邮件正文存储在以邮件 ID 后接 `-D` 命名的文件中。它将头和信封信息存储在以邮件 ID 后接 `-H` 命名的文件中。如果 `exim4` 无法投递邮件，它会将邮件标记为冻结并且不再再次尝试投递。一旦成功投递邮件，`exim4` 将从 `/var/spool/exim4/input` 删除与该邮件相关的文件。

默认情况下，`exim4` 将发往本地系统的邮件投递到用户邮件池目录 `/var/mail` 中的 `mbox` 格式。在该目录中，每个用户都有一个以用户名命名的邮件文件。邮件保留在这些文件中直到被收集（通常由 MUA 收集）。一旦 MUA 从邮件池中收集邮件，MUA 将按照用户的指示存储邮件，通常位于用户的家目录。

### 发往非本地系统的邮件

`exim4` 用于处理发往非本地系统的邮件方案取决于其配置方式：它可以将邮件发送到智能主机（`smarthost`），也可以发送到邮件地址所属域的 DNS MX 记录指向的系统，或者拒绝发送邮件。

### mbox 与 maildir

`mbox` 格式将用户的所有消息存储在单个文件中。为了防止损坏，进程在向文件中添加消息的同时删除消息时，不能锁定该文件；即当 MTA 正在添加消息时，MUA 无法删除消息。另一种竞争格式 `maildir` 则将每条消息存储在单独的文件中。这种格式不使用锁，允许 MUA 在邮件投递到同一用户的同时，删除该用户的消息。此外，当你使用 IMAP 等协议检查邮件时，`maildir` 格式的开销更。`exim4` 守护进程支持 `mbox` 和 `maildir` 格式（见第 767 页）。Qmail（第 779 页）作为 `sendmail` 和 `exim4` 的替代方案，使用了 `maildir` 邮箱。

## 日志

默认情况下，`exim4` 将普通日志发送到 `/var/exim4/mainlog`，其他消息进入同一目录下的其他文件。`mainlog` 中的以下行描述了直接发送到远程系统 SMTP 服务器的邮件。`exim4` 守护进程在每次接收消息时写入一行，在尝试投递消息时写入一行。`Completed` 行表示 `exim4` 已完成邮件投递，其后是条目的日期和时间。

```
$ tail -3 /var/log/exim4/mainlog
2007-07-19 23:13:12 11B1Jk-0000018-12 <= zachs@example.com U=sam P=local S=304
2007-07-19 23:13:12 11B1Jk-0000018-12 => zachs@example.com R=dnslookup T=remote_smtp
H=filter.mx.meer.net [64.131.141.12]
2007-07-19 23:13:18 11B1Jk-0000018-12 Completed
```

除 `Completed` 行外，下一条记录是一个两个字符的状态标志，告诉该行描述的是哪种事件：

* `+` 接收到消息
* `=>` 正常投递邮件
* `->` 正常投递到附加地址（相同投递）
* `*` 因为 `-N` 命令选项未投递
* `**` 因为地址退回而未投递
* `==` 因为临时问题未投递

紧随标志后的信息由以下字母之一加等号引导：

* `H` 远程系统（主机）名称
* `U` 发送消息的用户名
* `P` 接收消息的协议
* `R` 处理消息的路由
* `T` 处理消息的传输层
* `S` 消息的大小（字节）

上一个示例中的第一行表示 `exim4` 正在从本地系统的 `sam` 投递 `zachs@example.com` 的消息。下一行表示 `exim4` 使用 DNS (`dnslookup`) 查找了地址，并将其投递到 `filter.mx.meer.net` 的远程 SMTP 服务器 (`remote_smtp`)，其 IP 地址为 `64.131.141.12`。

以下日志记录了 `exim4` 从远程系统接收并投递到本地系统的消息：

```
2007-07-19 23:13:22 1B1k4-0000t0-8L <= zachs@gmail.com Hw=out-0506.google.com
[66.249.82.229] P=esmtp S=9913 ID=71a25fd507079213y304a1b27t3f9f... 
2007-07-19 23:13:22 1B1k4-0000t0-8L => sams@example.com R=local_user T=mail_spool
2007-07-19 23:13:22 1B1k4-0000t0-8L Completed
```

更多关于日志文件的信息请参考 `exim4` 规范。如果你发送和接收大量邮件，邮件日志可能会变得很大。`logrotate`（第 684 页）`exim4-base` 文件定期归档这些文件。

## 处理消息

你可以使用许多不同的选项调用 `exim` 来处理系统上的消息，并生成通过该系统的邮件记录。这些选项中的大部分都以 `-M` 开头，并需要你想要处理的邮件的消息 ID（见前一节）。以下命令从队列中移除消息：

```
$ sudo exim4 -Mrm 1IEKKJ-0006CQ-LM
Message 1IEKKJ-0006CQ-LM has been removed
```

以下是你可以用于处理消息的某些 `exim4` 选项。每个选项后都必须跟上消息 ID。`exim4` 手册页提供了完整的列表：

* `-Mf` 将消息标记为冻结
* `-Mrm` 移除消息
* `-Mmt` 显示正文
* `-Mvh` 显示头部

## 别名与转发

你可以使用别名和 `.forward`（第 764 页）文件来转发邮件。大多数时候，当你发送邮件时，它投递到特定的个人；`user@system` 映射到指定系统上的真实用户。有时你可能想将邮件投递到一个类而不是特定的收件者。类的包括 `postmaster`、`webmaster` 和 `tech_support`。你可以使用 `/etc/aliases` 文件将本地地址和类映射到本地用户以及非本地地址。`/etc/aliases` 中的每行包含本地（伪）用户名称，后面跟着用逗号分隔的目的地列表。由于发往 `root` 账户的邮件很少被检查，默认安装包含一个类似的条目，将邮件重定向到：

```
root: sam
```

你可以设置别名将邮件转发给多个用户。以下行将发往本地系统 `abuse` 的邮件转发给 `sam` 和 `max`：

```
abuse: sam, max
```

你可以使用这种别名创建简单的邮件列表。例如，以下将本地系统 `admin` 的邮件拷贝给多个用户，包括位于不同系统的 `zach`：

```
admin: helen, max, zach@example.com
```
