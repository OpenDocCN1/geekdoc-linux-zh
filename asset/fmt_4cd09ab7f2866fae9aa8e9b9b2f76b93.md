
如果一个用户不再位于邮件服务器上，但仍然接收发送到其旧地址的电子邮件，你需要在该账户中实现一个 `.forward` 文件。这样，该用户仍可在新的位置接收发送到其旧地址的电子邮件。虽然你可以在 `/etc/aliases` 文件中添加条目将邮件重定向到新地址，但该文件条目很容易被忽略。相反，一旦该用户的账户被删除，请立即在其主目录中插入一个 `.forward` 文件，同时保留主目录完好无损。

请注意，`.forward` 文件的权限应仅允许该用户写入，其他人不可写入。攻击者很容易向该用户发送一个文件，然后成为该用户。像 `bin` 和 `root` 这样的特权用户永远不应该有 `.forward` 文件，而应使用 `/etc/aliases` 文件中的条目。

`.forward` 文件的标准语法是将新的电子邮件地址放在第一行。如果你希望该用户也能保留发送到旧地址的电子邮件，只需输入一个反斜杠（`\`），然后跟上旧账户名称。

例如，为了将来自 `mydomain.com` 上 `jsmith` 账户的邮件发送到 Joe 的新电子邮件地址 `joes@newdomain.com`，同时保留他在 `mydomain.com` 上收到的邮件用于缓存目的，你只需将以下条目放入他的 `.forward` 文件中，并确保该文件仅由 Joe 可写：

```text
# Joe's new email address
joes@newdomain.com
\jsmith
```

这样，Joe 将在新地址接收电子邮件，但也可以检查缓存的同样存储在他旧地址的消息。

### 为你的程序增加额外安全性

在 sendmail 主页上的常见问题解答（FAQ）中，对与 sendmail 程序相关的某些额外安全问题进行了非常详细的解释。本节摘录自该页面，并稍作编辑以提高清晰度。

sendmail 程序经常因许多实际上是其他问题（例如目录权限过于宽松）导致的问题而受到指责。因此，sendmail 会检查系统目录和文件的权限，以确定它们是否可信。为了让 sendmail 正常运行而不抱怨，你必须执行以下命令：

```bash
# chmod go-w / /etc /etc/mail /usr /var /var/spool /var/spool/mqueue
# chown root / /etc /etc/mail /usr /var /var/spool /var/spool/mqueue
```

你可能需要根据你的环境调整这些命令。例如，一些系统将 spool 目录放在 `/usr/spool` 而不是 `/var/spool`，并使用 `/etc/mail` 目录而不是 `/etc` 存放别名文件。在 Red Hat Linux 中，`/var/spool` 目录是 `mqueue/` 的位置。如果在 `sendmail.cf` 中设置了 `runAsUser` 选项，那么 `runAsUser` 必须拥有 `/var/spool/mqueue` 目录。作为一般规则，在编译 sendmail 后，运行以下命令以初始化别名数据库：

```bash
/usr/lib/sendmail -v -bi
```

该命令可能会生成如下消息：

```text
WARNING: writable directory /etc
WARNING: writable directory /usr/spool/mqueue
```

如果是这样，列出的目录具有不适当的写权限，你应该保护它们以避免各种可能的安全攻击。

从 sendmail 8.9.x 开始，这些检查变得更加严格，以防止用户访问他们通常无法读取的文件。特别是，位于不安全目录路径中的 `.forward` 和 `:include:` 文件，或将传入电子邮件重定向到可执行文件的文件（不安全目录路径是指组或任何人都具有写权限的目录路径）将不再被允许。因此，如果用户 `joe` 的主目录对组 `staff` 可写，sendmail 将不使用 Joe 的 `.forward` 文件。你可以通过设置 `DontBlameSendmail` 选项来改变这种行为，但这会牺牲系统安全性。

![](img/a0884097af3186d9b4f616aaa3f065b0_672_0.png)

例如，为了允许在组可写目录中使用 `.forward` 文件，在 `/etc/sendmail.cf` 文件中输入以下代码行。通常你只需取消该行开头的注释并添加额外的变量：

- `O DontBlameSendmail=forwardfileingroupwritabledirpath`

或者，为了允许这些文件在组可写和任何人可写的目录中使用，输入以下内容：

- `O DontBlameSendmail=forwardfileinunsafedirpath`

来自这些不安全 `.forward` 和 `:include:` 文件的项被标记为不安全地址——这些项不能将邮件投递到文件或程序。你也可以通过 `DontBlameSendmail` 选项来改变这种行为：

- `O DontBlameSendmail=forwardfileinunsafedirpath, forward-fileinunsafedirpathsafe`

第一个标志允许读取 `.forward` 文件，第二个标志允许将该文件中的项标记为可用于文件和程序投递的安全地址。

![](img/a0884097af3186d9b4f616aaa3f065b0_672_1.png)

受此加强安全措施的约束影响的其他文件包括类文件（如 `Fw`）、`/etc/sendmail.cw`、持久主机状态文件，以及由 `ErrorHeader` 和 `HelpFile` 选项指定的文件。针对类、`ErrorHeader` 和 `HelpFiles` 的类似 `DontBlameSendmail` 标志也可用。

如果你有 `forward` 和 `include` 文件的不安全配置，可以通过查找所有这些文件并对每个文件输入命令 `chmod go-w $FILE` 来使其安全。此外，对文件路径中的每个目录输入命令 `chmod go-w $DIR`。

### 设置邮件列表

有许多邮件列表程序可用于大型成员列表，但最有效的可能是 `majoromo`。`majoromo` 程序处理邮件列表，并要求订阅列表的人通过回复电子邮件来验证其身份。这是其他不要求任何验证、因此允许任何人使用任何电子邮件地址订阅的电子邮件列表管理器的显著改进。除了 `majoromo` 之外的这些较旧或动态性较差的邮件列表对于系统管理员来说可能特别麻烦，因为用户会使用虚假或伪造的电子邮件地址进行订阅。每当发送邮件时，所有使用 `root@localhost` 作为有效电子邮件的用户都会导致列表出现多次退回。`Majoromo` 通过强制新订阅者提供有效电子邮件并回复查询电子邮件以证明其身份来绕过此问题。这样，别人就不能将你订阅到不想要的邮件列表中。

第一步是从 Internet 下载最新版本的 `majoromo`。官方 `majoromo` 站点的主 URL 如下：

```text
http://www.greatcircle.com/majoromo/
```

在页面中间部分，你将看到下载源代码的位置。最新版本的 `majoromo` 还包含你可以下载并用于简化安装过程的 RPM。在其他情况下，你可以下载源代码并自行编译。

一旦你有了代码，你希望在一个目录中创建二进制文件，然后在另一个目录中安装它。我在主目录 `/home/kerry` 中解压并释放源代码，然后确定我的安装目录为 `/usr/local/etc/majoromo-1.95.5`。

## 运行各种电子邮件客户端

我本可以将后一个目录命名为 `majordomo/`，而不是使用完整版本名称，但我想了解最新版本是什么以及何时应该升级。如果你希望拥有一个简单的 `majordomo/` 目录，可以创建一个符号链接，从实际目录指向一个没有版本号的目录。使用类似于以下命令：

```
$ ln -s majordomo majordomo-1.94.5
```

一旦我手头有了源代码，我需要为 `majoromo` 运行选择一个用户和组 ID。我选择了 `majordomo` 和 `daemon`。然后我编辑了 makefile，以便它知道去哪里查找我的 Perl 库。我为我的 Perl 和编译器选择了以下两个变量：

```
PERL = /usr/bin/perl
CC = gcc
```

#### 清单 17.4 `majordomo` 配置文件的示例打印输出
