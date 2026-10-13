
![](img/c2419364ebb911c809b6a79991707c27_211_0.png)

## 提示

如果你没有全天候的互联网连接，你可以使用 `/usr/sbin/sendmail -bd -o DeliveryMode=d` 以延迟模式启动 sendmail，这样在下次通过 `/usr/sbin/sendmail -q` 运行之前会避免使用 DNS。如果你定期连接，可以将 `/usr/sbin/sendmail -q` 放入 cron 作业中，这样当你的连接可用时，队列会自动处理。

如果你希望 sendmail 在每次启动后自动启动，请从默认的运行级别目录创建一个符号链接（以 Sxx 开头，其中 xx 为数字）到 /etc/rc.d/init.d/sendmail 脚本。例如，要在多用户系统（运行级别 3）每次启动后运行 sendmail，我可以创建以下符号链接：

```
ln -s /etc/rc.d/init.d/sendmail
/etc/rc.d/rc3.d/S85sendmail
```

这确保 sendmail 在每次启动后自动启动。/etc/rc.d/init.d/sendmail 脚本使用 -bd 选项启动 sendmail。你可能希望修改 /etc/rc.d/init.d/sendmail 脚本以反映你站点的队列间隔要求。此外，你可能希望在以下行之前添加以下代码：

```
daemon /usr/sbin/sendmail -bd
```

在脚本中以便在启动时自动对配置文件运行 newaliases 和 makemap：

```
newaliases
for i in virtusertable access domaintable mailertable
do
if [ -f /etc/mail/$i ] ; then
echo "Making $i database for sendmail..."
makemap hash /etc/mail/$i < /etc/mail/$i
sleep 1
fi
done
sleep 1
```

这确保每次启动服务器进程时，所有配置数据库都会重建。

你也可以很方便地使用 `/etc/rc.d/init.d/sendmail` 脚本来启动、停止和重启 sendmail。要停止 sendmail，运行

```
/etc/rc.d/init.d/sendmail stop
```

要重启 sendmail，运行

```
/etc/rc.d/init.d/sendmail restart
```

你还可以通过使用 `-q` 选项强制 sendmail 立即处理其队列：

```
/usr/sbin/sendmail -q
```

如果你希望部分处理队列，可以使用 `-qString` 选项仅处理发件人地址包含指定字符串的消息队列。例如，以下命令强制 sendmail 处理发件人为 kabir 的所有排队邮件：

```
/usr/sbin/sendmail -qSkabir
```

当队列中有大量邮件等待时，这非常方便。

![](img/c2419364ebb911c809b6a79991707c27_212_0.png)

## 提示

你可以运行 mailq 命令来查找当前队列中的消息。

你也可以使用 `-qRstring` 强制 sendmail 处理收件人地址包含指定字符串的消息。

## 理解和配置 /etc/sendmail.cf

`/etc/sendmail.cf` 配置文件被认为是有史以来 UNIX 管理员必须处理的最高复杂度的配置文件。

本节提供了配置文件中设置方式的简要概述，并使你能够按照 sendmail 网站 (http://www.sendmail.org/) 上的说明根据需要实现某些功能。换句话说，本章中的信息足以让你开始使用，并提供足够的知识来遵循清晰编写的说明以实施配置更改。本节不解释如何创建自己的配置规则，这需要对 sendmail 配置的内部工作原理有深入的理解。

sendmail.cf 文件包含以下类型的配置信息：

- 空行将被忽略。
- 以 # 号开头的注释行也将被忽略。
- 以 C、D、F、H、O、P、V、K、M、S 或 R 开头的行是配置行。
- 以前导空白字符开头的行是续行。

以下各节简要展示了各种配置，以便你了解它们各自的作用。

### S 和 R：地址重写规则

S 行用于标记新重写规则的开始。此类行的语法为 Srule，其中 rule 为规则名称/编号。例如，S3 标记规则集 3 的开始。

R 行定义地址重写规则。可以将重写规则视为如下语句：

```
If (current e-mail address matches rule's left-hand-side pattern) then
    Replace current address
        with the rule's right-hand-side pattern
end
```

其语法如下：

```
R<LHS>  <RHS>  <optional comments>
```

LHS 是规则的左手侧模式，RHS 是右手侧模式。例如，在以下语法中，

```
RS* < $* > $* <&>   $: $1 < $2 > $3
```

LHS 模式为 $* < $* > $* <&>，RHS 模式为 $: $1 < $2 > $3。LHS 和 RHS 模式均由各种元符号组成，例如 $*、$+、$-、$=x 和 $-x。

重写规则相当复杂，通常不需要你进行任何更改。然而，如果你计划编写自己的重写规则，你应该阅读随 sendmail 文档提供的 Sendmail 安装和操作指南。

### D：定义宏

D 行定义宏。语法如下：

```
D<macro name> <string>
```

例如，以下语法等同于 $P = someword，并且每当在其他地方引用 $P 时，它会扩展为 someword：

```
DP someword
```

通常，你不需要添加、删除或移除任何 D 宏定义。

### C 和 F：定义类

C 行与 D 行类似。此类行的语法如下：

```
C<class name> <string> <string> . . .
```

此文件必须每行包含一个条目。你在 sendmail.cf 文件中会注意到的另一个 F 行如下：

```
FR-o /etc/mail/relay-domains \
```

类 R 是 /etc/mail/relay-domains 中所有域名列表。请注意 -o 选项，它使该行成为可选的。换句话说，如果此文件为空，sendmail 不会报错。通常，你不需要在此处进行任何更改。然而，如果你希望 sendmail 在未定义中继域时报错，可以从前面的 FR 行中删除 -o 选项。

### M：定义邮件传输代理

M 行用于创建邮件传输代理定义。此类行的语法如下：

```
Mmailer name field=value, field=value, . . .
```

在以下示例中，定义了邮件传输代理 SMTP：

```
Msmtp, P=[IPC], F=mDFMuX, S=11/31, R=21/31, E=\r\n, L=990,
T=DNS/RFC822/SMTP
```

通常，你不需要对标准邮件传输代理定义进行任何更改。

### H：定义头部

H 行用于创建头部定义。此类行的语法如下：

```
H[?flags?]<header name>: <header template>
```

例如，以下每个 H 行都定义了一个邮件头部：

```
H?P?Return-Path: <$g>
HReceived: $?from $s $.$?($?s$|from $.$_)
.$ by $j ($v/$z)$?r with $r.$. id $i.$?u
for $u; $|
.$b
H?D?Resent-Date: $a
H?D?Date: $a
```

```
H2?Resent-From: $7x5x <Sg>$|Sg$.
H2?From: $7x5x <Sg>$|Sg$.
H2xFull-Name: $x
H2MResent-Message-Id: <St.$i8$j>
H2MMessage-Id: <St.$i8$j>
```

你不应对头部定义进行任何更改。

### O：设置选项

O 行用于为 sendmail 设置全局选项。此类行的语法如下：

```
O option name = value
```

表 9-1 显示了 sendmail 最新版本（8.9.x）中所有可用的选项。

## 表 9-1 Sendmail 选项

| Option | Explanation |
|---|---|
| AliasFile=/etc/mail/aliases | 设置别名数据库文件的名称。仅当你将别名数据库保存在 /etc/mail/aliases 以外的其他位置时才更改。 |
| AliasWait=30m | 启动时别名加载的默认超时时间（以分钟为单位）。请勿更改。 |
| AutoRebuildAliases=True | 如果设置为 True，sendmail 会在必要且可能的情况下尝试重建别名数据库。请勿更改。 |
| BlankSub= | 设置空白替换字符。请勿更改。 |
| CheckAliases=False | 如果设置为 True，会检查别名数据库中别名右侧的有效性。默认设置为 False。不建议更改。 |
| ClassFactor=1800 | 用于计算消息的优先级。请勿更改。 |
| ConnectionCacheSize=2 | 任何时候将被缓存的打开连接的最大数量。 |
| ConnectionCacheTimeout=5m | 在空闲期间，缓存的连接保持打开的最大时间（以分钟为单位）。 |
| ConnectionRateThrottle=20 | 允许每秒不超过指定数量的守护进程处理传入连接。将此值设置为 0 允许无限（即系统资源允许的）数量的守护进程每秒。 |

