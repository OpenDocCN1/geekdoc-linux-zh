
`smtpGreetingMessage` 选项定义了客户端连接到本地机器上的 `sendmail` 守护进程时显示的横幅文本。在前一行中，`$j` 解析为本地机器的全限定域名 (FQDN)；`v` 和 `$Z` 分别代表配置文件和可执行程序版本；`$b` 是当前的日期和时间。这将打印出类似下面的行：

```
220 al.mbox.com ESMTP Sendmail\n8.9.3/8.9.3: Mon, 19 Jul 1999 18:47:23 -0400
```

# UNIX 初始 From 头部格式（旧的 $1 宏）

```
#0 UnixFrom=$g $d
```

`UnixFrom` 选项定义了 "From" 行的格式。默认值 `$g` 打印发送者地址，随后是接收消息的日期和时间。接下来的几行定义了如何处理嵌入的换行符：

## From: 有换行符

```
#0 SingleLineHeader=False
```

如果将 `SingleLineHeader` 选项设置为 `True`，头部内的任何换行符将被转换为一行。接下来的几行与 SMTP 响应 HELO 相关：

## 允许关联主机名的 HELO

```
#0 AllowBogus=False
```

如果 `AllowBogus` 选项设置为 `True`，则不强制 HELO 限制。接下来的几行与特殊字符有关：

## 名称中需要引号的字符

```
#0 MustQuoteChars.:%!
```

`MustQuoteChars` 选项列出了除了 `sendmail` 定义的字符外，可以作为地址内分隔符的字符。此选项不应更改。接下来的几行与 `initgroups` 有关：

## 我是否应该由于开销而避免调用 initgroups(3)？

```
#DontInitGroups=False
```

`DontInitGroups` 选项（如果设置为 `True`）强制 `sendmail` 不处理组系统调用。如果组成员很多或网络设备较慢，这非常有用。默认值为 `False`。接下来的几行与一个过时的函数有关：

## 可写入的 :include 和 .forward 文件（不可信）

```
#UnsafeWrites=True
```

`UnsafeWrites` 选项已被 `DontBlamemail` 选项的各种参数实际上取代，该选项在本节早期讨论过。接下来的几行与发送错误有关：

## 错误发生时错误发送到哪里？

```
#DoubleBounceAddress=postmaster
# 如果其他方式失败，退信保存在哪里
#DeadLetter=/var/tmp/dead.letter
```

`DoubleBounceAddress` 指定了由于投递早期错误失败而产生的错误消息的接收者。默认值为 `postmaster` 别名。`DeadLetter` 选项指定了当退信邮件无法写入其他位置时保存的备份位置（默认情况下是 `/var/tmp/dead.letter`）。接下来的几行与用于 `sendmail` 处理的用户 ID 有关：

## 大大部分处理假设哪个用户？

```
#RunAsUser=sendmail
```

通过使用 `RunAsUser` 选项，可以配置 `sendmail` 执行大部分处理（读取配置文件和在特权端口上监听传入连接除外）。`RunAsUser` 选项指定用户名或 UID。这听起来可能是个好主意，但它的副作用是要求无权限用户访问所有 `.forward` 文件、`:include` 和队列目录。这可能需要大量使用 `DontBlamemail` 选项，并可能产生比解决的更多问题。接下来的几行与 SMTP 信封中的接收者有关：

## 每个 SMTP 信封中的最大接收者数量

```
#MaxRecipientsMessage=100
```

`Max` `MaxRecipientsMessage` 选项规定了每个 SMTP 信封中每条消息个人接收者数量的上限，以阻止垃圾邮件（未经请求的商业电子邮件或未经请求的批量电子邮件），这类邮件通常发送给大型分发列表。默认情况下，没有限制。接下来的行与获取本地名称有关：

## 我们是否从已安装的接口获取本地名称

```
0 DontProbeInterfaces=true
```

`DontProbeInterfaces` 选项（如果设置为 `True`）可防止 `sendmail` 自动修改类宏 `Cw`，使其包含所有物理网络接口的主机和地址。默认情况下，等效的主机和地址会被添加到 `Cw` 中。接下来的行与状态通知（DSN）有关：

## Return Receipt-To: 标头意味着 DSN 请求

```
0 RrtmpliesDsn=False
```

`RrtmpliesDsn` 选项会导致投递状态通知发送给信封发送者，而不是标头中包含的地址。下一个选项允许你覆盖连接地址。

## 覆盖连接地址（用于测试）

```
0 ConnectOnlyTo=0.0.0.0
```

为了强制将邮件投送到特定地址，你可以使用 `ConnectOnlyTo` 选项添加 IP 地址。这对于测试目的非常有用。接下来的选项与定义信任用户有关：

## 用于文件所有权和启动守护进程的信任用户

```
0 TrustedUser=root
```

`TrustedUser` 选项可以设置系统中的哪个用户被信任发送 `sendmail` 相关文件并运行 `sendmail` 守护进程。用户名可以是 `/etc/passwd` 文件中的名称或用户 ID。下一组选项可用于指定系统上证书颁发机构（CA）证书和私钥的位置：

```
# CA 目录
0 CACERTPath
# CA 文件
0 CACERTFile
# 服务器证书
0 ServerCertFile
# 服务器私钥
0 ServerKeyFile
# 客户端证书
0 ClientCertFile
# 客户端私钥
0 ClientkeyFile
```

## 第四部分 + 红帽 Linux 网络和服务器设置

`CACERTPath` 选项允许你指定一个包含 CA 证书的目录。`CACERTFile` 允许你指定单个 CA 证书。`ServerCertFile` 和 `ServerKeyFile` 分别允许标识 `sendmail` 在作为服务器运行时应使用的 CA 证书和关联私钥。`ClientCertFile` 和 `ClientKeyFile` 分别允许标识 `sendmail` 在作为客户端运行时应使用的 CA 证书和关联私钥。

## 邮件优先级

优先级可以与电子邮件关联，尝试让某些邮件在传输其他邮件时具有更高的权限。`sendmail.cf` 文件中的邮件优先级部分允许你查看如何处理不同的邮件优先级。以下行出现在该部分的开头：

```
############################
# 优先级 (邮件优先级) #
############################
first-class=0
special-delivery=-100
Plist=-30
Pbulk=-60
Pjunk=-100
```

之前的行将优先级值与邮件标头中可能的优先级名称等同。每个优先级名称的含义如表 19-5 所示。数字本身没有重要意义，但在与其他优先级名称的关系上除外。此外，请注意，入站邮件是立即被处理的（除非另有限制），因此这些优先级值仅适用于队列中的邮件。

| 表 19-5 优先级名称 |
| 名称 | 含义 |
|---|---|
| special-delivery | 一种高优先级邮件，应在任何邮件之前从队列投递。 |
| first-class | 除非在邮件标头中覆盖，否则这是默认优先级。 |
| list | 此优先级名称应用于大多数从邮件列表发出的邮件。 |
| bulk | 一种相对不重要的广播邮件。这也表示存在投递问题，邮件正文将不会包含在退信通知中。 |
| junk | 无价值的电子邮件，可能是程序的输出或测试邮件。正文也会从退信通知中丢弃。 |

## 信任用户

你可以允许你信任的用户发送发者名称并非真实用户名的邮件。以下行出现在“信任用户”部分，用于设置信任值：

```
################
# 信任用户 (Trusted users) #
################
# 这相当于设置类 *t*
Ft/etc/sendmail.ct
Troot
Daemon
uucp
```
