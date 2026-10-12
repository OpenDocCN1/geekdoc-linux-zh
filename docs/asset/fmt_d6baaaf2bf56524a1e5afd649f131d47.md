
/etc/postfix/main.cf 的其余部分处理虚拟域名、垃圾邮件过滤和地址重写。这些是某些高级的话题，可能大多数管理员并不感兴趣。通过上述概述的基础设置，你应该能够放心地使用这些其他条目中的默认值。

## 启动 Postfix

Postfix 文档（例如 `/etc/postfix/main.cf` 中的注释）非常详尽且有用。Postfix FAQ 是一份长文档，包含了多个 Postfix 配置示例——独立机器、网络机器、防火墙上或内网内的 Postfix 等，以及一份良好的故障排除解决方案列表。你可以在 http://postfix.sparks.net/faq.html 找到 FAQ。

一旦你完成 `/etc/postfix/main.cf` 的配置，保存文件并退出文本编辑器。现在你可以启动 Postfix，通常是通过执行以下命令完成的：

```
/usr/bin/postfix
```

以 root 身份运行。（如果你恰好有 Postfix 的 System V init 脚本，请运行该脚本）。确保 25 端口（默认 SMTP 端口）对入站连接开放。你应该能够接收你系统的邮件，并且它应该被递送到每个用户相应的 `/var/spool/mail/$USER` 目录。

## 提示

Postfix 文档（如 `/etc/postfix/main.cf` 中的注释）是详尽且实用的。Postfix FAQ 是一份长文档，包含了几个 Postfix 配置示例——独立机器、网络机器、防火墙上或内网内的 Postfix 等，以及一份良好的故障排除解决方案。你可以在 http://postfix.sparks.net/faq.html 找到 FAQ。

## Exim

Exim 邮件服务器是一个在剑桥开发的英语程序，用于替代 smail（下文描述）。与 smail 类似，Exim 以 GNU 许可证发布并免费提供。然而，Exim 整合了一些 smail 分发版从未包含的功能，包括地址验证和一些垃圾邮件过滤工具。Exim 体积很小，在机器上占空间有限，且 CPU 开销低。对于不发送大量邮件的小型网络，它是一个很好的替代方案，尽管它已经在生产环境中经过良好测试。

Exim 越来越流行。许多曾经使用 smail 并喜欢在系统中拥有 GPL 邮件服务器的管理员，由于其更高的性和易于管理，将 smail 替换为 Exim。Exim 甚至作为某些 Unix 发行版的默认邮件传输代理，并被一些每天传输数千条消息的大型网站采用——Exim。

## 获取和安装 Exim

你可以从 Exim 项目网站 http://www.exim.org 获取 Exim 的最新版本。最新版本是 3.16。Exim 团队建议你避开 2.0.x 及更早的版本，因为它们本质上是测试版本；3.0 及更高版本具有极大改进的安全性和工具。

按照安装任何其他 Unix 软件包的方式安装 Exim，使用第 31 章“安装和管理软件”中介绍的方法。确保阅读 Exim 包中包含的文本文件，特别是 README 文件。该文件将包含任何最后的更改，以及关于在系统上编译和配置 Exim 的有用指导。

在开始安装 Exim 之前，创建一个名为 `Makefile` 的本地配置文件。当你下载并压缩 Exim 文件后，你会在 `/src/EDIT` 文件找到它；你可以将 `/src/EDIT` 复制到正确的位置。

在构建包之前阅读此 `Makefile`，因为你可能需要在安装前进行一些编辑。

Exim 通过一个在启动时运行的文件进行配置，该文件同时使用普通条目和宏来处理设置。Exim 配置语法非常复杂，我们建议如果你想安装 Exim 并使其在你的系统上运行，请咨询 Exim 项目网站上的 FAQ。FAQ 说明每个配置选项并显示了启用禁用选项的正确语法。

## 注意

Exim 的默认配置文件位于 `/src/configure.default`。该文件在安装时会被复制到实际配置位置（取决于所使用的 Unix 变体）。如果你想知道之后变化的默认配置，可以查看此文件，或者如果你编辑了文件，可以将其从 `/src` 位置复制到当前的配置位置。

## 测试与监控

完成配置后，通过执行命令测试 Exim 是否正常工作：

```
exim -v
```

接下来，要查看 Exim 是否能识别本地，请执行命令：

```
exim -bv
```

如果 Exim 工作正常，它将返回一条显示版本和构建日期的消息。要测试你是否可以接收邮件，执行命令：

```
exim -v localhost@yourdomain.com
```

如果 Exim 工作正常，邮件将被递送到你的 `/var/spool/mail/$USER` 目录。如果有错误，请检查 `/var/log/mail` 中的日志以获取更多信息。

# 邮件列表与 qmail

qmail 最实用的功能之一允许个人用户设置和管理他们自己的邮件列表。这减轻了你作为管理员的负担，因为你不需要在中央文件中添加或删除列表或列表成员。相反，你的用户可以自行决定列表的名称、加入列表的人员以及列表的管理方式。

要在 qmail 下设置一个由用户管理的邮件列表，请登录你的用户账户。在你的主目录下创建一个名为 `qmail-listname` 的文件，将 `listname` 替换为列表的简单名称，该名称不要包含空格或特殊字符。在该文件中，每行输入一个该邮件列表成员的电子邮件地址，每行一个。保存文件并退出编辑器。现在，当邮件发送到 `youruserid-listname@yourdomain.com` 电子邮件地址时，qmail 将自动将邮件副本发送给你主目录下 `qmail-listname` 文件中列出的所有人。

为了确保你在你的地址处接收到退信和其他管理消息（且退信不会发送给邮件管理员），请使用命令 `touch qmail-listname-owner` 在你的目录中创建一个空文件 `qmail-listname-owner`，这会将你标识为列表所有者。

你的系统中，单个用户可以管理的邮件列表数量没有限制。然而，由于用户的订阅和删除必须手动完成，因此任何用户可能想要花时间管理邮件列表存在有效限制。qmail 的开发者 Dan Bernstein 使用 `ezmail` 包作为替代方案；`ezmail` 支持自动订阅、存档和其他功能。它是全局安装的，但个人用户的使用方式与普通的 qmail 邮件列表相同。你可以在 http://cr.py.to/ezmail.html 了解更多关于 ezmail 的信息。

![](img/c297036e8ead34f32fa6046c0fa309ee_725_0.png)

# smail

smail 邮件服务器是 GNU 基金会的邮件服务器程序。它已经很久没有更新了，并且存在严重的安全漏洞，因为它允许未经授权的邮件中继。我们不建议你运行 smail，尽管我们支持大多数 GNU 软件；它的安全性还不足以部署在连接到互联网的机器上。

过去运行 smail 的大多数站点现在都在运行 exim、qmail 或其他小型且健壮的邮件服务器程序。只有极少数切换到了 sendmail，因为 smail 最初的设计是作为 sendmail 的较小替代品。如果你对免费邮件服务器感兴趣，你必须在 GNU 基金会之外寻找。遗憾的是，smail 目前没有被开发，因为它曾经发挥过很有作用。

# 设置 POP 和 IMAP 服务

在 Unix 上设置 POP 和 IMAP 服务非常简单。通常，你只需要安装 IMAP 包，该包通常包含在你的 Unix 发行版中或可以从 Unix 软件库获取，通常同时支持 IMAP 和 POP 协议。一旦安装了包，使用第 31 章“安装和管理软件”描述的常规 Unix 软件安装方法，访问 POP 或 IMAP 服务只需取消 `/etc/inetd.conf` 中相关行的注释即可使服务运行。

在 `/etc/inetd.conf` 文件中（如第 43 章“远程访问 (inet) 服务”介绍所示），你会看到如下所示的代码：

+ # Pop and imap mail services et al

```
#-pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#-pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
#-imap stream tcp nowait root /usr/sbin/tcpd ipmapd
```

只需在文本编辑器中打开文件并删除相应行前面的哈井标记（#），即可取消你想要使用的服务的行注释。

> POP2 是 POP 协议的一个较旧版本。大多数最近的邮件程序都支持较新的 POP3 版本。我们建议，如果可能，优先使用 POP3 而非 POP2。只有当你有非常有力的理由说明必须支持旧版客户端程序时，才使用 POP2。

假设你选择使用 POP3 服务，代码与上面相同，但第二行没有哈井标记：
