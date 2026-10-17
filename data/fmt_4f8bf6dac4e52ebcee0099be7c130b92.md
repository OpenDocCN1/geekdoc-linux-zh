
这是一个在你的区域文件中相当混乱的记录——为了方便复制和粘贴。`k=sa` 标签标识密钥类型；唯一定义的数值是 `rsa`。`t=y` 标志意味着你只是在测试 DKIM，如果你的签名没有通过，接收站点将忽略它们。`p` 子句是公钥本身。分号必须用反斜杠转义，因为它们是 DNS 数据文件中的注释符号。

DKIM TXT 记录通常包含一个版本标签 `v=DKIM1`。与 TXT 记录一样，所有内容必须包含在双引号中。

要为你的区域文件生成相应格式的 RSA 密钥对，请使用 `openssl` 命令生成密钥并从中提取正确的公钥：

```
$ openssl genrsa -out rsa.private 1024

$ openssl rsa -in rsa.private -out rsa.public -pubout -outform PEM
```

然后，从 `rsa.public` 中复制公钥并粘贴到你文本记录的 `p` 子句中。它不能包含任何空格或换行符，因此请小心复制粘贴，不要引入任何额外的字符。

你可以选择任何名称作为选择器（selector）。

在上面的 Gmail 示例中，名称 `gamma._domainkey.gmail.com` 的 `_domainkey.gmail.com` 部分并不是 `gmail.com` 的真实子域名。你可以通过搜索该区域的名称服务器（`dig _domainkey.gmail.com ns`）来验证这一点，如果它是正式的委托子域名，则它必须存在。下面来自 `yahoo.com` 的示例将 `_domainkey` 实现为了正式的子域名。

### ADSP 记录

RFC5617 定义了一种可以存放在特殊子域名中的 TXT 记录，用于表示你对签名消息的整体策略。该记录在最近被标准化（2009年），被称为 ADSP（授权域名签名策略）文本记录。该子域名是 `_adsp._domainkey.domain`。

在 TXT 记录内部，你包含一个 `dkim=` 子句来声明你站点的签名策略。可能的值有：

- `all`，适用于签名所有出站邮件的域名
- `unknown`，适用于签名部分邮件的域名
- `discardable`，适用于签名所有邮件并建议丢弃无法通过签名验证消息的域名

例如，`discardable` 标签可能被银行使用，他们从为此目的创建的子域名发送敏感的客户账户信息。如果用户根据伪造邮件的指令操作，该域名可能会产生灾难性的后果，最好让此类邮件在到达收件人之前被拒绝或丢弃。

如果你正在测试 DKIM 且不想收件者认真对待你的签名，ADSP TXT 记录也可以包含一个 `t=y` 子句。

在 ADSP 系统开发期间（RFC5617 之前），域名的 ADSP TXT 记录存储在不同的子域名（`_domainkey.domain`，无前缀），且语法略有不同：`o=-` 表示该域名签名了部分邮件，而 `o=all` 表示它签名了所有邮件。

由于两种约定使用不同的子域名，它们可以共存。在编写中，原始格式仍然占据主导地位。如果你准备让收件者审查你的签名，最好的做法是在未来几年内同时使用这两种约定，直到所有人都符合 RFC5617 标准。

让我们来看一个例子。Gmail 没有 ADSP 记录，但 Yahoo! 有：

```
_domainkey.yahoo.com 7200 IN TXT "t=y; o=-\;
n=http://ispam.yahoo.com/domainkeys"
```

`n=` 子句是一个注释，引导人类用户查看更多关于 Yahoo 使用 DKIM 记录的信息。一些站点会包含一个电子邮件地址（为了带垃圾邮件，不包含任何 @ 符号）。这里是 yahoo.com 用于选择器 `s1024` 的 DKIM TXT 记录：

```
s1024.yahoo.com 86400 IN TXT "k=rsa; t=y;
n=MIGMAQGCSqSibD3BEQAAAGNADQBiKBQgDreeOR4j/cutQFiYUY
E9UCSHa/R2PLjInTD8V4Unn+2FAZGEK3lb23eOUlyV4Peleb3Bgm"
jjDIOKU3NSL4KJAUJHFwDebtOp+s8VKKYETATL2Yr/s37Ahy+1t4JKrd
V7VXtn56lb4dUnwwxK4YH5bDOJ+XcwiDIQAB;n=1024 bit key."
```

在这里 `n=` 子句是一个注释，这次是关于密钥本身的。

本节显示的 DKIM 记录都是 TXT 记录，但它们实际上将迁移到格式相同的 DKIM 记录类型。在此期间，站点可以使用这些类型来确保没有 DNS 问题。第 17 章：DNS 系统
