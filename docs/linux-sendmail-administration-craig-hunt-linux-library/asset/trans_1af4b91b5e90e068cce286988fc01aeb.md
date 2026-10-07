

# 第 5 章 理解供应商的配置

canonify input: craig
Canonify2 input: craig
Canonify2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromL input: craig
AddDomain input: craig
AddDomain returns: craig < @LOCAL*
MasqHdr input: craig < @ @LOCAL*
MasqHdr returns: craig < @wren.foobirds.org.
HdrFromL returns: craig < @wren.foobirds.org.
final input: craig < @wren.foobirds.org.
final returns: craig < @wren.foobirds.org
> ^D

我们使用 Sendmail -bt 模式运行了两个测试。在两种情况下，我们都使用了一个头/地址，并提供了地址 `craig` 以通过本地邮件传输器处理。第一次测试使用了 `generic-linux.cf` 配置，它没有使用 `always_add_domain` 特性。地址进入后输出的仍然 `craig`。在第二次测试中，我们使用了 `redhat.cf` 配置，它使用了 `always_add_domain` 特性。在此测试中，`craig` 被转换为 `craig@wren.foobirds.org`。`always_add_domain` 的效果显而易见。

这是一个非常好用的特性。本地邮件上显示的地址在任何地方都是有效的。这有助于避免用户之间的困惑，而你正想避免那些困惑的用户！

`access_db` 此功能允许 Sendmail 使用访问数据库来决定哪些主机、域名和网络是可接受的邮件来源。可以使用可选参数定义数据库类型和路径来配合 access_db 功能。默认数据库类型为 `hash`，默认路径为 `/etc/mail/access`。访问数据库在第 6 章中描述。对抗垃圾邮件将在第 11 章介绍。

`blacklist_recipients` 此功能允许使用访问数据库来阻止来自特定收件人的邮件。通常，访问数据库用于控制来自不良源的邮件。通过此功能，访问数据库也可以用于控制发往某些目的地的邮件。`blacklist_recipients` 特性将在第 11 章中详细介绍。

`accept_unresolvable_domains` 告诉 Sendmail，如果源域名无法通过 DNS 解析，则接受来自该源的邮件。默认情况下，Sendmail 获取 `MAIL FROM:` 请求头中的主机名，并在请求 DNS 将该名称映射回地址之前才会接收入站邮件。此选项覆盖了该默认行为。

允许来自不可解析域的邮件是一个潜在的安全问题，但对于没有全天 DNS 服务的系统，此特性通常是必要的。此类系统包括可能断开连接的笔记本电脑，或者位于防火墙后未赋予完全 DNS 访问权的系统。Red Hat 配置包含了此特性，因为 Red Hat 必须创建一个适用于最广泛范围系统的配置。如果你为网络拥有全天 DNS 服务——你本应该拥有——请从你的配置中删除此特性。

在匹配 `FEATURE` 命令之后有两个 `MAILER` 命令。第一个是我们已经描述过的 `MAILER(smtp)` 命令。第二个是 `MAILER(procmail)` 命令。看到它，你可能会认为与之前描述的 `local_procmail` 参数有关。其实不是。`local_procmail` 意味着名为 `local` 的邮件传输器将使用 `procmail` 程序。而 `MAILER(procmail)` 意味着将添加一个名为 `procmail` 的邮件传输器，它将使用 `procmail` 程序。这两者是无关。通过 `MAILER(procmail)` 安装的邮件传输器仅在 `mailtable` 中配置了使用它时才会被使用。

这是一个大型配置，包含了重要的功能（如 `smsh`）和不重要的功能（如 `MAILER(procmail)`）。正如我们在第 4 章看到的，该配置运行良好并为我们的 Red Hat 系统投递邮件。但这只是一个开始。对 `accept_unresolvable_domains` 特性的讨论以及 `redhat.mc` 文件内部的注释明确表明，我们应该创建一个适合我们自己的配置。在下一节中，我们将这样做。从 `redhat.mc` 文件开始，我们创建自己的 Red Hat 配置。

# 修改 Red Hat 配置

`redhat.mc` 配置中有很多好的地方，也有一些不尽人意的地方以及冗余。由于我们要重写配置，我认为我们还应该重新组织它，将某些内容从宏配置文件移动到更适合这些项目的宏源文件中。因此，我们将编辑 `redhat.mc` 文件，创建一个新的 `OTYPE` 类型，并创建一个新的 `DOMAIN` 文件。为了做到这一点，我们首先

![](img/9639113aa446fb8976cb3d377f7aafdd_154_0.png)

将 `redhat.mc` 拷贝到 `redhat81.mc`，将 `octype/linux.m4` 拷贝到 `octype/redhat7.0.m4`，并将 `domain/generic.m4` 拷贝到 `domain/foobirds.m4`。

接下来我们编辑这些文件。首先我编辑了宏配置文件 `redhat81.mc`，将 `DOMAIN` 命令改为 `foobirds.m4` 而不是 `generic.m4`。然后我将 `CONF_USER_ID` 参数移动到新的 `OTYPE` 文件，因为我认为用户 ID 和组 ID 设置是 Red Hat Linux 特有的。我删除了 `undef` 定义，它们没有意义。我还删除了 `CONFAUTO_REBUILD`，这是一个已弃用的选项。

我考虑过将 `CONF_CONNECT` 移动到 `OTYPE` 文件，因为它设计用于覆盖 Linux 操作系统的默认 TCP 超时设置。相反，我决定将其移动到 `DOMAIN` 文件，因为我希望以非标准的方式处理 MX 记录。我删除了 `CONF_PROBE_INTERFACES` 选项，因为我拥有全天 DNS 服务，因此不需要该特性。

