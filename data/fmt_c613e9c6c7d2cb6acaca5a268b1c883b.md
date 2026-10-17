
```
# shall we get local names from our installed interfaces?
O DontProbeInterfaces=true
```

`DontProbeInterfaces` 选项（如果设置为 True）会阻止 sendmail 自动使用所有物理网络接口的主机名和地址来修改类宏 `Cw`。默认情况下，等效的主机和地址会被添加到 `Cw` 中。接下来的行与投递状态通知（DSN）有关：

```
# Return-Receipt-To: header implies DSN request
#O RrtImpliesDsn=False
```

`RrtImpliesDsn` 选项会使投递状态通知发送到信封发件人，而不是发送到头中包含的地址。下一个选项允许你覆盖连接地址。

```
# override connection address (for testing)
#O ConnectOnlyTo=0.0.0.0
```

为了强制将所有邮件投递到特定地址，你可以使用 `ConnectOnlyTo` 选项添加一个 IP 地址。这在测试时很有用。下一个选项与定义受信任用户有关：

```
# Trusted user for file ownership and starting the daemon
#O TrustedUser=root
```

`TrustedUser` 选项可用于设置系统中哪个用户被信任拥有 sendmail 相关文件并运行 sendmail 守护进程。用户名可以是 `/etc/passwd` 文件中包含的名称或用户 ID。下一组选项可用于指示系统中证书颁发机构（CA）证书和私钥的位置：

```
# CA directory
#O CACERTPath
# CA file
#O CACERTFile
# Server Cert
#O ServerCertFile
# Server private key
#O ServerKeyFile
# Client Cert
#O ClientCertFile
# Client private key
#O ClientKeyFile
```

`CACERTPath` 选项允许你指示包含 CA 证书的目录。`CACERTFile` 允许你指示单个 CA 证书。`ServerCertFile` 和 `ServerKeyFile` 分别让你识别 sendmail 作为服务器时应使用的 CA 证书和关联私钥。`ClientCertFile` 和 `ClientKeyFile` 分别让你识别 sendmail 作为客户端时应使用的 CA 证书和关联私钥。

## 消息优先级

可以尝试将优先级与电子邮件消息关联，以赋予某些消息比其它消息更高的传输权限。`sendmail.cf` 文件中的消息优先级部分允许你设置如何处理不同的消息优先级。该部分开头的行如下：

```
#####################
#  Message precedences   #
#####################

Pfirst-class=0
Pspecial-delivery=100
Plist=-30
Pbulk=-60
Pjunk=-100
```

上述行将优先级值与消息头中可能的优先级名称对应起来。每个优先级名称的含义见表 19-5。数字本身并不重要，除了相对于其他优先级名称而言。还要注意，传入邮件会被立即处理（除非受到其他限制），因此这些优先级值仅适用于队列中的消息。

### 表 19-5：优先级名称

| 名称 | 含义 |
| :--- | :--- |
| special-delivery | 高优先级消息，应从队列中先于其他任何消息投递。 |
| first-class | 除非在消息头中被覆盖，否则这是默认优先级。 |
| list | 此优先级名称应用于大多数源自邮件列表的消息。 |
| bulk | 相对不关键的广播消息。这也表示如果存在投递问题，消息正文将不会包含在退回通知中。 |
| junk | 无价值的电子邮件，可能是程序的输出或测试消息。正文也会从退回通知中丢弃。 |

## 受信任用户

你可以允许你信任的用户发送带有与其真实用户名不同的发件人名称的消息。以下行出现在“受信任用户”部分中，用于设置受信任用户值：

```
#####################
#  Trusted users  #
#####################

# this is equivalent to setting class "t"
Ft/etc/sendmail.ct
Troot
Tdaemon
Tuucp
```

这些名称指定了允许使用 sendmail 的 `-f` 标志设置非当前运行命令的用户作为发件人的用户。你在这里可能不希望指定任何普通用户账户。但是，如果你使用允许指定 outgoing 消息发件人的邮件列表管理器（见下一节），你可能希望包含 `Tmajor domo` 行。否则，所有发送给列表收件人的 outgoing 邮件都将包含错误 *X-Authentication-Warning*：

## 标题格式

localhost：使用消息头中的 `-f` 参数，通过 majordomo 将发件人设置为 owner-bigmailinglist。如果您有大量受信任的用户，可以使用文件类 t 来指定一个包含名称列表的文件。

你可以修改 `sendmail` 使用的邮件头格式，请在你的 `/etc/sendmail.cf` 文件中操作。以下行出现在该部分的开头：

```
####################
# Format of headers #
####################

H?P?Return-Path: <$g>
HReceived: $ ?$from $S $.$?_($?$S|from $.$_)
	$.$?(auth_type)(authenticated$?(auth_ssf) (${auth_ssf} bits)$.)
	$.$?by $J ($v/$Z)$?r with $T. id $i$?(tls_version)
		(using $?(tls_version) with cipher $({cipher} (${cipher_bits} bits) \
		verified $({verify}))$.$?u
		for $u; $|;
		$.$b
H?D?Resent-Date: $a
H?D?Date: $a
H?F?Resent-From: $?x$X <$g>|$g$.
H?F?From: $?x$X <$g>]|$g$.
H?x?Full-Name: $x
# HPosted-Date: $a
# H?l?Received-Date: $b
H?M?Resent-Message-Id: <$t.$i@$j>
H?M?Message-Id: <$t.$i@$j>
```

这些行规定了消息头的格式。在将合适的值替换到上述变量之后，这段文本就会变成 `/var/spool/mqueue` 中的一个 qf 文件。

## 重写规则

`sendmail.cf` 文件中的重写规则（Rewriting Rules）部分包含了一套复杂的规则，用于处理你的 sendmail 服务。这些规则涵盖了诸如地址转换和处理本地主机名等内容。你不应该随意更改此部分的条目。重写规则部分的开头包含一个标题，显示如下：

```
###############################
####################
#######
####
REWRITING RULES
####
```

同样，如果你确实需要编辑这些行，那么各地的系统管理员都会给你至少一定程度的同情和怜悯。

## 邮件器定义

邮件投递代理（MDAs）在邮件器定义（Mailer Definitions）部分中进行描述。具体来说，该部分允许你将 `Mlocal` 和 `Mprog` MDA 定义为 procmail 和 smrsh 程序以外的其他程序：

```
Mlocal,      P=/usr/bin/procmail, F=1sDFMAW5:/ |@qSpFhn9,
	S=EnvFromL/HdrFromL,
	R=EnvToL/HdrToL,
	T=DNS/RFC822/X-Unix,
	A=procmail -Y -a $h -d $u
Mprog,     P=/usr/sbin/smrsh, F=1sDFMogeu9, S=EnvFromL/HdrFromL,
	R=EnvToL/HdrToL, D=$z:/ ,
	T=X-Unix/X-Unix/X-Unix,
	A=smrsh -c $u
```

通常，你不需要修改邮件器定义中指定的选项。然而，前面展示的 `Mlocal` 和 `Mprog` 邮件器定义值得一提。`Mlocal` 定义用于将消息投递到本地账户。使用 procmail MDA（而不是 UNIX 标准的 `/bin/mail`）将文件放入相应用户的邮箱中。
