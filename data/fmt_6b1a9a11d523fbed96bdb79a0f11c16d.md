
# 第20章 电子邮件

## 20.16 DKIM 配置

对 DKIM 的覆盖有些分散。介绍性材料在 DNS 章节（第 591 页）以及本章的第 768 页。在这里，我们关注通过外部工具`amavisid`使用 DKIM 的细节，以及与`sendmail`、`Exim`和`Postfix`直接结合的细节。`sendmail`和`Postfix`使用用于实现 DKIM 的邮件过滤器（milters）。`Exim`原生支持此功能。`Exim`的实现已广泛可用（2009 年后期），但细节略显粗糙。

### DKIM: 域名密钥标识邮件 (DomainKeys Identified Mail)

DKIM 是积极识别发送者组织的新希望。如果得到广泛部署，它将抑制垃圾邮件发送者和钓鱼攻击者伪造发送者域名的能力。来自你银行的邮件将确实来自你的银行——或者至少不会被归类为钓鱼或垃圾邮件。

DKIM 替换了早期的名为 DomainKeys 的系统。DKIM 使用公钥加密（将密钥存储在 DNS 中）让接收者验证邮件的来源和完整性。在我们许多业务通过电子方式完成的互联世界中，这些保证正变得至关重要。DKIM 还可以防止发送者否认其发送过消息，这种特性被称为“不可否认性”（nonrepudiation）。

DKIM 实现包含两个部分：在出站邮件离开你的服务器时对其进行签名的部分，以及在入站邮件到达时对签名进行验证的部分。第一项操作应由你的发送邮件主机在邮件离开服务器之前执行（在完成任何内部重写和内容扫描之后）。第二部分是验证，应在接收消息后立即完成，在其他扫描工具添加或更改其邮件头之后。

sendmail.org 有几个实用的工具，它们是通用的，可以与任何实现 DKIM 的软件配合。第一个工具接受域名名并生成相应的 ADSP TXT 记录，你必须将其添加到 DNS 中以实现 DKIM²。第二个工具是一个验证器，你可以在一切就绪后用它检查你的设置。

DKIM 和 ADSP 资源记录的细节请见第 591 页。它们目前仍是 TXT 记录，但未来可能会拥有自己的 DNS 记录类型。`OpenSSL`和`amavisid`都包含了生成 DKIM 密钥的代码。各种 DKIM 邮件过滤器包也包含生成密钥的脚本。

一旦你配置了 MTA 生成 DKIM 签名，你就可以向 sa-test@sendmail.net 发送消息，以验证一切是否运行正常。服务器将回回邮件给你，告知它检索了哪些功能。

如果你有 Gmail 账户，另一种方法是给自己发一封邮件。点击“显示详情”（show details）链接应该会显示`signed-by`字段。你也可以在下拉菜单中要求 Gmail “显示原始邮件”（Show original）——此命令将向你显示带有所有头（包括 DKIM 签名）的原始消息。

### DKIM 过滤

实现 DKIM 的软件最初由 Sendmail, Inc. 开发，用作与`sendmail` MTA 接口的过滤器。现在有两个版本：原始的 DKIM-milter；以及代码分支版本 OpenDKIM。这两个包都可以在 sourceforge.net 获取源码，也可以从各种包仓库获取预编译版本。我们在此说明`sendmail`版本即 DKIM-milter v2.8.3 的用法。

该包包含`dkim-filter`（负责创建和验证签名的邮件过滤器）以及几个帮助调试和监控 DKIM 使用的实用程序。列表如下：

- `dkim-filter` - 生成并验证 DKIM 签名
- `dkim-genkey` - 生成密钥对和所需的 DNS 记录
- `dkim-stats` - 总结由`dkim-filter`收集的统计数据
- `dkim-testkey` - 测试密钥格式是否正确且可访问
- `dkim-tespsp` - 测试 ADSPD 记录（曾称为 SSP）

设置 DKIM-milter 包的第一步是创建一个专用的用户账户和组来拥有 DKIM 相关文件。用户名和组名均使用 "dkim"。确保你的账户具有受限的 shell，例如`/bin/false`。

`dkim-genkey`脚本生成一个 DKIM 密钥。你通过`-d`参数指定密钥所属的域名，通过`-s`参数指定选择器（密钥名称），实际上默认值是 example.com 和 "default"。`-r`标志将密钥限制用于邮件签名，而`-t`则表示你正在测试 DKIM。密钥保存在单独的文件：`selector.private`存储私钥，`selector.txt`包含公钥的 DNS TXT 记录。

例如，
```
$ dkim-genkey -r -d example.com -s email
```

这会在当前目录的`email.private`和`email.txt`文件中生成密钥。将邮件服务器密钥安装在类似`/etc/mail/dkim/keys`的地方。将`/etc/mail/dkim`目录的模式设置为 600，并使用`chown`（递归使用）将其所有者改为你的用户和组。将 DNS TXT 记录添加到相应的区域文件，刷新服务器序列，并通知你的名称服务器。一旦一切测试通过并运行正常，你可以添加 ADSP 记录，但不要仅仅这样做。

运行`dkim-testkey`来验证你的密钥是否正常。如果一切正常，`dkim-testkey`不产生输出，因此沉默是金。

下一项任务是配置`dkim-filter`作为过滤器使用。创建一个由你的用户和组拥有的`/etc/mail/dkim.conf`文件。示例内容改编自 T. J. Nelson 的在线文章《使用 Sendmail 建立 DKIM》：

```
Canonicalization simple

Domain mail.example.com

KeyFile /etc/mail/dkim/keys/email.key.pem

MTA MSA

PidFile /var/run/dkim-filter.pid
```

21. 在出站邮件签名设置好并运行正常之前，切勿发布你的 ADSP 记录，以免让其他网站开始拒绝你的邮件。

（注：后续文本存在大量重复的 OCR 错误，已根据逻辑进行去重处理。）

### sendmail 中的 DKIM

你可以通过使用过滤器（行内过滤；见第 767 页）或结合`amavisid`使用双服务器设置为`sendmail`实现 DKIM。在这里，我们将介绍如何使用 DKIM-milter 对邮件进行签名和验证。

`sendmail`的配置原语`masquer_as`和`generictable`用于重写报头，这些原语在添加任何 DKIM 签名之前必须实现；否则签名将无法保持有效。

为了支持 DKIM，编译`sendmail`时必须包含 milter 支持，并提供可用的`OpenSSL`和 Berkeley DB 库，同时需要安装 DKIM-milter 软件包。使用`OpenSSL`生成密钥，并按照第 591 页的描述将其添加到你的 DNS 名称中，或如第 846 页所示使用`dkim-genkey`。

在本示例中，我们的域名是 example.com。我们选择了选择器 "email"，并将私钥存储在`email.private`中，公钥存储在`email.key.pem`中。我们可以按照如下方式使用`dkim-testkey`测试密钥：

```
$ dkim-testkey -k /var/db/dkim/email.key.pem -s ma
```

如果一切正常，`dkim-testkey`将没有任何输出。

在你的`sendmail`配置文件`sendmail.mc`中添加该行：

```
INPUT_MAIL_FILTER('dkim-filter', 's=inet:8891@localhost')
```

