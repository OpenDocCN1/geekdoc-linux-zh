
由于没有活动的互联网连接，无法立即递送的邮件存储在 `/var/spool/queue` 目录中。`sendmail` 会定期尝试再次递送。当邮件长时间一段时间无法递送时，`sendmail` 会向发送者发送警告。

即使你的计算机只是通过 PPP 经常连接互联网，`sendmail` 也应该作为后台进程运行，因为该程序还处理

计算机内部邮件投递。（例如，在发生故障或问题时，程序会自动向 `root` 发送邮件。）

> 可以通过 `sendmail` 获取在线信息。根据分发版的不同，可以在 `/usr/doc/packages/sendmail` 中找到更多信息。进一步的帮助来源还包括 `Mail-HOWTO` 和《Linux 网络管理指南》的第 15 章。

# 配置

`sendmail` 通过配置文件 `/etc/sendmail.cf` 控制。所有发行版都至少包含一个现用的配置文件。某些发行版（如 Slack 和 SuSE）根据预期用途提供多种配置变体以供选择：例如，用于没有 Internet 连接的本地局域网、UUCP 等。最适合离线使用的版本是带有 Internet 连接和服务器支持（DNS）的变体。

即使预设的配置文件已经运行良好，你通常也需要对其进行细微调整，以使 `sendmail` 优化地适应 PPP/SLIP 的特性。幸运的是，`sendmail.cf` 提供了详细的注释，使得许多设置的含义变得一目易见。

在修改 `sendmail.cf` 之前，你应该先停止并随后重启 `sendmail`。在 Red Hat Linux 中，你需要执行以下命令：

```
# /etc/rc.d/init/sendmail stop
# /etc/rc.d/init/sendmail start
```

在 SuSE 中，路径略有不同：

```
# /sbin/init.d/sendmail stop
# /sbin/init.d/sendmail start
```

# 主机名问题

`sendmail` 将状态和错误消息记录在 `/var/log/mail*` 文件（文件名取决于发行版，参见 `/etc/syslog.conf`）。如果你在使用 `sendmail` 时遇到问题，应该检查此文件。

一个特别常见的问题是信息“unqualified host name (localhost) unknown”。随后 `sendmail` 会等待一分钟才恢复工作。这个问题的原因通常是使用了 `localhost` 作为计算机名。在这种情况下，`/etc/hosts` 的内容可能像某个发行版中的所示（例如在 SuSE 中）：

```
# /etc/hosts: sendmail 抱怨主机名未限定
127.0.0.1 localhost
127.0.0.2 localhostdomain localhost
```

虽然大多数程序实际上可以处理这种情况，但建议选择一个不同的计算机名（如果符合 Unix 标准的方案更好，可以使用 `myhost`）。据此，你生成以下 `/etc/hosts` 文件，`sendmail` 也能接受。（当然，现在 `/etc/HOSTNAME` 必须包含名称 `myhost`。）

```
# /etc/hosts: 这样是可以的 (SUSE)
127.0.0.1       localhost
127.0.0.2       myhost.localdomain      myhost
```

另一种方法是继续使用 `localhost` 作为计算机名，并将 `/etc/hosts` 中的 `localhost` 替换为完整的计算机名。（然而，这违反了完整规则，即 `localhost` 被认为是完全限定的（不带扩展名）。RedHat Linux 通常配置为这样，如果网络只设置了环回。）

```
# /etc/hosts: 这也是可以的 (RedHat)
127.0.0.1       localhost.localdomain   Localhost
```

# 设置发件人地址

当你通过 PPP/SLIP 使用 `Elm`、`Mail` 或 `sendmail` 发送邮件时，系统会自动插入 `loginname@domainname` 作为发件人地址。这是不理想的——无法向该地址回复，但你必须使用你在 Internet 服务商处的地址（在本章示例中：`hofer@provider.de`）。

在 `/etc/sendmail.cf` 中进行细微更改可以确保 `sendmail` 使用不同的发件人，而不是主机名和域名的主名。在以字母 DM 开头的 `masquerade` 行中，你可以指定所需的发件人域名。这会导致 `sendmail` 根据登录名、`@` 字符和伪装文本来组装发件人。

```
# /etc/sendmail.cf 中的另一种修改
# 指定固定的计算机名
DMprovider.de
```

这两项设置都不影响 `pine`！`pine` 会为自己构建发件人字段。关于如何告知 `pine` 指明指定的发件人，请见第 351 页。在 Netscape 和 `kmail` 中，该工具由程序直接插入。

通常情况下，`sendmail` 只发送电子邮件，不发送新闻文章。新闻文章的发件人也必须单独设置——程序和 `tin` 请参阅第 376 页和第 380 页。

# 调用 Internet 服务商作为中继

在标准设置下，`sendmail@hostname` 负责转发你的消息。通常，你可以将此任务交给你的 Internet 服务商。为此，你需要设置 `sendmail` 仅将你的邮件投递到系统（不再进一步传递）。这具有基本优势：即使你向另一个国家发送消息且 Internet 连接阻塞，你也可以延迟将邮件投递给你的服务商并节省成本。

`sendmail.cf` 中必要的更改再次限制于一行：你必须在以 DS 开头且通常为空的行中指定你的 Internet 服务商邮件服务器的地址：

```
# /etc/sendmail.cf 中的修改
# "Smart" 中继（可能为空）
Provider.de
```

# 修改超时设置

`sendmail.cf` 包含一个单独章节，可以在其中指定各种超时设置。这些设置控制当邮件消息在规定时间内无法投递时 `sendmail` 的行为。通常必须增加这些时间，否则你将收到来自 `sendmail` 的烦人消息，通知你无法投递。如果你在早上写了一条消息，但决定只在晚上通过 PPP 发送（因为白天你无法访问服务商，或者意识到这条消息无法投递且不需要警告）。

```
# /etc/sendmail.cf 中的修改
# 一天后，无法投递的邮件
# 寄件人将收到警告；sendmail
# 仍然尝试投递
# 0.queuewarn=1d
# 五天后，无法投递的
# 邮件将返回给寄件人
# 0.queuereturn=5d
```

`sendmail` 尝试投递邮件的频率由启动 `sendmail` 时使用的选项 `-q` 控制（例如 `-q1h` 每小时投递一次）。在 RedHat 中，通过 `/etc/rc.d/init.d` 执行；在 SuSE 中通过 `/sbin/init.d` 执行。

# 创建你自己的 sendmail.cf

`sendmail.cf` 的构建方式使得该文件通常不被编辑，而是通过重新编译宏文件来实现。这种过程的优点是，源文件比 `sendmail` 本身更易理解，因此更容易适配。创建完全新的配置文件的前提是安装了 `sendmail` 配置文件（并非所有发行版都包含）以及宏处理器 `m4`，后者的功能与 C 编译器相比更好。此外，你还需要许多基础知识。`sendmail` 的官方文档是 O'Reilly 出版的 800 页书籍。

`sendmail.cf` 的源文件通常位于 `/usr/share/sendmail` 或 `/usr/src/sendmail` 目录。`cf` 子目录包含了多个现成的配置文件，你可以调用 `m4` 生成新的 `sendmail.cf`。在以下指令中，使用 `linux.smtp.mc` 代替 `cf` 中的许多其他文件。

```
root cd /usr/src/sendmail/cf
root m4 linux.smtp.mc > sendmail.cf
root mv sendmail.cf /etc/
```

在执行 `m4` 时，`detail`、`osype` 等目录中的各种配置文件将被读取并处理。关于此过程和各种设置的详细描述可以在 `README` 文件中找到。

# mailq

`mailq` 或等效命令 `sendmail -bp` 显示所有由邮件程序发送但无法投递的邮件（例如，由于没有 Internet 连接）。因此，`mailq` 是判断是否存在未发送邮件的简单方法。

# 发送本地邮件

如果你没有 Internet 连接，也可以在你的计算机上尝试发送电子邮件。作为地址，你只需输入收件人的名称（例如 `hofer` 或 `root`）。在某些程序（`pine`，Netscape）中，你必须为收件人名称添加 `@localhost`，例如 `rootlocalhost`。原因是：某些邮件程序会自动为 `root` 补充 `@hostname.domainname`，这本身是正确的，但可能会导致通过 `sendmail` 的本地投递出现问题。

# 通过 POP 获取邮件 (fetchmail)
