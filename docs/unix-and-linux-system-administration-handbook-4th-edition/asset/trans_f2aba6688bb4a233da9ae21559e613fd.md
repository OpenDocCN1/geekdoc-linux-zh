
变更。这里我们仅介绍 DKIM 的 DNS 方面。邮件方面的含义见第 845 页开始的第 20 章“电子邮件”。

DKIM 资源记录尚未被标准化为一种 DNS 记录类型；而是使用一种特殊格式的 TXT 记录。它们使用的 DNS 记录名由“选择器”（selector）与字符串 _domainkey 拼接而成。记录的数据就是站点的 DKIM 公钥。可能存在多个选择器，以便可以轻松地轮换和撤销密钥。

使用 DKIM 签名的站点会使用其 DKIM 私钥，对指定的头部字段和邮件正文计算签名。它将该签名以名为 DKIM-Signature 的头部字段形式放入外发邮件中。

相应的公钥可通过发送站点的 DNS 区域获取，它是一个与名称 selector._domainkey.domain 关联的 TXT 记录。接收站点对该密钥执行 DNS 查询，并用其验证邮件签名。成功的签名验证可认证该邮件确实来自所声称的发送域，并验证邮件在传输过程中未被修改。

下面是一个已签名邮件中的 DKIM-Signature 头部行示例：

```
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=gmail.com; s=gamma; h=domainkey:signature:mime-version:received:reply-to:date:message-id:subject:from:to:content-type;
 bh=24HFUvt1AO4jxRNbmg94pNGZJUPdQbSkOdZppon4sL;
 b=UyYWupx/UdQj75d1nH5zSlDK7r/Gw+HwYbXMoLCSlhwhqrhYhy1ea3s0s8
 EmXJEY13jyzj3VN GemO AOSUqH fMmdLSlDP7AvxptY0VflGyG M9ID4uw
 B0l4a7zJuoI VHJmsEA/ExK48rvq1OJ2Y+A gRd bpx6/56phSVJt+aA=
```

签名中的各个标签在表 17.7 中说明。

## 表 17.7 DKIM-Signature 邮件头部中的标签

| 标签 | 示例值 | 含义 |
| --- | --- | --- |
| v | 1 | 版本号；必须为 1 |
| a | rsa-sha256 | 加密算法：rsa-sha1 或 rsa-sha256 |
| c | relaxed/relaxed | 规范化算法：simple 或 relaxed |
| d | gmail.com | 发送者的域 |
| s | gamma | 选择器或密钥名称 |
| h | domain... | 要包含在头部签名中的头部字段 |
| bh | 24HFUvt1... | 邮件正文的加密哈希 |
| b | UyYWupx... | 整封邮件的加密签名 |

a. 该算法指定了在加密之前如何对头部和正文进行处理。

选择器标签 s=gamma 告诉我们公钥的名称，而 d= 标签给出父域。要获取公钥，我们需要用 dig 查询伪主机 gamma._domainkey.gmail.com 的 TXT 记录。

```
gamma._domainkey.gmail.com. 300 IN TXT "k=rsa; t=y;" p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDlhyR3oltQyZZOaBriVe9mIM3E8RqOjeasANSpG2YTH7YV+Xtp4wxfSgTjCMHQEMs0qYu0FyYNQPQqg2t0mFx9zNu6OrfRBDJijU9ptx2T+NGIWZ8qbhbLo5By8apJavLygTLavyPSrv sx0B3YzC63T4Age2CdZQYA+OwSMWQJDQAB"
```

这条记录相当杂乱，如果非要手工输入到区域文件中会很麻烦——幸好可以剪切粘贴。k= 标签标识密钥的类型；迄今为止唯一定义的值是 rsa。t=y 标志表示你只是在测试 DKIM，因此即使你的签名验证失败，接收站点也应宽容处理。p= 子句就是公钥本身。分号必须用反斜杠转义，因为分号在 DNS 数据文件中是注释符号。

DKIM TXT 记录通常包含一个版本标签 v=DKIM1。与所有 TXT 记录一样，所有内容都必须放在双引号中。

要为你的区域文件生成合适格式的 RSA 密钥对，请使用以下 openssl 命令生成私钥并从中提取相应的公钥：

```
$ openssl genrsa -out rsa.private 1024
$ openssl rsa -in rsa.private -out rsa.public -pubout -outform PEM
```

然后将 rsa.public 中的公钥剪切并粘贴到你的文本记录的 p= 子句中。它不能包含任何空格或换行符，因此要小心剪切粘贴时不要引入任何额外字符。

你可以选择任意名称作为选择器。

在上面的 Gmail 示例中，名称 gamma._domainkey.gmail.com 中的 gamma._domainkey.gmail.com 部分，从 DNS 的角度来看并不是 gmail.com 的真正子区域。你可以通过查找该区域的名称服务器（dig _domainkey.gmail.com ns）来验证这一观察；如果它是一个真正委派的子区域，这些名称服务器就应该存在。下面来自 yahoo.com 的示例将 _domainkey 实现为一个真正的子域。

RFC5617 定义了一种 TXT 记录，你可以将其存放在一个特殊的子域中，以表达你关于邮件签名的总体策略。该记录直到最近（2009 年）才被标准化，称为 ADSP（作者域签名策略，Author Domain Signing Policy）文本记录。该子域是 _adsp._domainkey.domain。

在 TXT 记录内部，你包含一个 dkim= 子句来声明你站点的签名策略。可能的值有：

- all，针对对所有外发邮件签名的域
- unknown，针对可能对部分邮件签名的域
- discardable，针对对所有邮件签名并建议接收方丢弃无法验证签名的邮件的域

例如，discardable 标签可能会被一家银行使用，该银行从为此目的创建的子域发送敏感的客户账户信息。A

