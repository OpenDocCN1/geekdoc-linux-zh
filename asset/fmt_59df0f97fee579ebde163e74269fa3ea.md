
- Postfix——由 Wietse Venema 编写作为 Sendmail 的替代方案，设计比 Sendmail 更快、更安全且更容易操作。你将在本章结束处学习关于 Postfix 的信息。

- Qmail——另一个对 Sendmail 的响应，Qmail 由 Dan Bernstein 编写，由于其安全和速度的声誉而日益流行（尽管据报道 Postfix更快）。此外，与 Postfix（它在与系统交互时尝试模仿 Sendmail，例如保留自己的池化文件和配置文件）不同，Qmail 使用自己的结构，并不试图为 Sendmail 用户简化过渡。对于运行由 Bernstein 编写的 EZMLM 邮件列表管理的管理员来说，Qmail 是一个很好的选择，因为 Qmail 与其紧密集成。

互联网上通有许多 MTA 在在使用；移植到 FreeBSD 的版本可以在 `/usr/ports/mail` 中找到。

# 常见的 MUA

邮件用户代理的数量比 MTA 还要多。由于 Windows 和 Macintosh 电子邮件客户端（如 Microsoft Outlook/Outlook Express、Eudora、Apple Mail、Mozilla Thunderbird 等）已广为人知，以下列表仅包含 FreeBSD 可用的流行的 MUA：

- Pine——表面上是“Program for Internet News and Email”（互联网新闻和电子邮件程序）的缩写，但一直有传闻这种来自华盛顿大学的开源产品名称实际上是“Pine Is Not Elm”的缩写。无论何种情况，Pine 都被广泛使用，它提供了直观的用户界面、许多现代处理功能、集成的 USENET 新闻组阅读功能，以及一个包含了 Pine 自带的坚固 pico 编辑器的消息编辑器。

- Elm——Pine 的祖先（至少，Elm 是从古老的 mail 和 mailx 程序演化而来的，这些程序在现代商业互联网之前为大学和政府网络执行邮件职责）。按今天的标准来看，Elm 虽然很原始，但仍有很多忠实用户。

- Mutt——被构想为一种“杂种”MUA，结合了 Elm、Pine 以及许多其他 MUA 的功能。

- mail——标准的命令行邮件客户端，是所有 Unix 类系统上的事实标准。

# 使用 Sendmail 配置基础电子邮件服务

FreeBSD 附带了 Sendmail，并已经配置好，可以开箱即用以满足基本需求。启用 Sendmail（使其在启动时运行）你需要做的就是在 `/etc.conf` 中添加以下行：

```
sendmail_enable="YES"
```

你可以通过重启来启用 Sendmail，或者通过输入 `/etc/rc.d/sendmail start` 来启动它。

当系统运行后，你可以向互联网上的任何人发送消息，他们也可以向你发送消息——前提是你妥善设置了某些项。大多数情况下，这些不是 Sendmail 本身的配置项，而是针对整个系统的。如果你决定用另一个 MTA（如 Postfix 或 Qmail）替换 Sendmail，你将在本章结束处学习如何操作。与此同时，由于 Sendmail 的默认配置适用于大多数服务器，我们将讨论如何管理 Sendmail 本身。

# 第 25 章 配置电子邮件服务

注意

`/usr/bin/sendmail` 实际上并不是 Sendmail 本身——它实际上是一个指向“包装器”（wrapper）的链接，这是一个小型程序，它接收命令并将输入并将其传递给 Sendmail 或另一个 MTA（邮件传输代理）。包装器的目的是允许你用 Postfix 等其他 MTA 替换 Sendmail；因为你所有的程序都是与包装器而非 Sendmail 本身交互，所以包装器确保了这种转换对你所有的系统功能都是无缝的。

`/var/mail` 中的邮箱文件（邮件队列 mail spools）是纯文本文件，每个文件以其所有者用户命名，并将权限设置为 600（仅所有者可读可写）。新消息会被附加到接收者邮件队列的末尾。此外还有一些长度为 0 的临时 POP 锁文件，名称格式为 `.username.pop`。当 POP3 连接打开时，它们会接收相应邮件队列的内容，任何未传输的剩余部分随后会被复制回邮箱箱。我们将在本章稍后详细介绍 POP3 服务器是如何运作的。

# 配置文件

以下是运行 Sendmail 时你会发现的一些 `/etc/mail` 中的重要文件。

## `/etc/mail/sendmail.cf`

这是 Sendmail 的主配置文件。然而，与几乎所有其他程序的任何配置文件不同，你不应该通过编辑此文件来更改 Sendmail 的行为。相反，你应该在更高层次的“宏”级别在主配置 `.mc` 文件中进行更改（该文件将在介绍），然后从该文件编译出 `sendmail.cf` 文件。

`sendmail.cf` 包含了选项、规则集和功能——其格式可能非常令人望而畏，几乎难以人类可读。最好的做法是让 `sendmail.cf` 保持现状。

`sendmail.cf` 定义了 Sendmail 处理发送给本地用户的入站邮件的行为。相应的配置文件 `submit.cf` 处理由本地用户生成的出站邮件，并定义了如何将其传输到远程 SMTP 服务器。

请参阅本章稍后的“消息队列”和“独立工作站的电子邮件”以获取更多关于配置 Sendmail“提交”（submission）侧的详细信息。

## `/etc/mail/freebsd.mc`

`/etc/mail/freebsd.mc` 是 Sendmail 的“主配置”文件。它包含了一个功能和选项列表，这些选项会覆盖标准配置文件中的默认值，这类似于 `/etc/rc.conf` 覆盖 `/etc/defaults/rc.conf` 的方式。然而，通过 `freebsd.mc`，设置的格式更加奇异。命令使用 `m4` 宏语言给出（该语言在 Sendmail 配置之外几乎不使用）。.mc 文件随后与默认的 `config.m4` 文件一起编译，在 `/usr/share/sendmail` 或 `/usr/src/contrib/sendmail` 中生成 `sendmail` 文件，从而创建一个 `.cf` 输出文件。然后你可以将此文件安装为新的 `sendmail.cf` 文件。

# 使用 Sendmail 配置基础电子邮件服务

听起来很困惑且反其道倒？是的，确实如此。Sendmail 的配置方法一直以来以复杂闻名，向后兼容性的担忧阻止了它获得迫切需要的彻底改版。然而，通过 FreeBSD 开发者的努力，特别是在最近的几个中，配置过程已经变得简单得多。过去，为了重新生成你的 `sendmail.mc` 文件，你必须进入你的源码目录，尽可能根据在线文档找出哪些更改，然后找出生成输出文件的 `m4` 编译命令——你必须手动安装它。现在的情况比以前有了很大改进，尽管它仍然不是任何人会认为的用户友好的东西。

`m4` 语言中的每一行在某处都包含字符串 `dnl`；这代表“删除到换行符”，并标记了可读行的结束（每一行都必须如此）。要注释掉一行，将 `dnl` 放在开头。否则，将其放在末尾。

在 `/etc/mail` 中有一个 `makefile`，其目标允许你通过简单执行 `make cf` 从 `freebsd.mc` 文件创建一个新的 `.cf` 文件。然后你使用 `make install` 将此输出文件（`freebsd.cf`）安装到 `sendmail.cf` 中：

```bash
# cd /etc/mail
# make cf
/usr/bin/m4 -D_CF_DIR=/usr/share/sendmail/cf/ /usr/share/sendmail/cf/m4.m4
>freebsd.mc > freebsd.cf
# make install
install -c -m 444 freebsd.cf /etc/mail
```

文件 `/etc/mail/Makefile` 有许多用途，正如你稍后将看到的。`Makefile`（通常命名为 `Makefile`）是位于任何源代码树顶层的特殊文件；它包含“构建目标”，允许你以预定义的方式编译代码。我们在第 16 章“安装软件”中涵盖了 ports 使用的 makefiles。在本章中，`make` 命令和 `install` 目标将指定该端口 `/etc/mail` 中规定的任何安装、FreeBSD 提供的用于编译组成 Sendmail 配置的各种数据库的 Makefile，甚至可以控制 Sendmail 本身。它本身并不是配置文件。相反，它是系统的一部分。因此，除非你知道自己在做什么，否则不应修改它。正如 `freebsd.mc` 文件为入站邮件生成默认的 `sendmail.cf` 文件一样，`submit.cf` 文件定义了出站邮件的选项。请参见本章稍后的“消息队列”和“独立工作站的电子邮件”以获取更多关于配置 Sendmail“提交”侧的详细信息。

## `/etc/mail/aliases`

`/var/mail` 中系统中的每个用户都有邮箱；然而，在你的机器上拥有电子邮件地址的人并不拥有账户。你始终可以为入站邮件地址设置任何其他地址的别名，无论是在互联网的其它地方甚至是一个程序。默认的 `/etc/mail/aliases` 包含了所有这些示例。别名行包含别名名称、逗号、空格或制表符（可选）以及目标地址或管道：
