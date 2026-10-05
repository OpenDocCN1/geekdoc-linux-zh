

# 第 6 章 使用 Sendmail 数据库

选项。所有选项在需要时都可用，只是你不太可能真的用不到。对于 Linux 管理员来说，最有用的选项是：

- NEWDB 此选项添加了 Linux 系统上使用的数据库支持。它提供了哈希（hash）和 B 树（btree）数据库。此选项提供了构建和访问大多数本地 Sendmail 数据库所需的所有功能。

- MAP_REGEX 此选项为 Sendmail 增加了一个新功能，允许使用正则表达式对数据库进行搜索。任何在 grep 中使用过正则表达式的人都知道，它们比简单的通配符字符要强大得多。当你需要创建复杂的规则来拦截垃圾邮件发送者时，这种增加的功能非常有用。

- USERDB 此选项支持用户数据库，可用于处理入站和出站邮件。相关的选项是 `UDB_DEFAULT_SPEC`，它定义了用户数据库的默认路径。也可以通过 Sendmail 配置中的 `CONFUSERDB_SPEC` 设置路径，正如我们在第 5 章“理解厂商配置”中在 `redhat.file` 中看到那样。我倾向于在配置中设置路径值，而不是将其编译到 Sendmail 中，因为在配置中它易于更改。然而，在 Sendmail 使用用户数据库之前，必须显式定义某些路径值。

- NIS 此选项提供对网络信息系统（NIS）数据库的访问。这些是管理数据库，例如 `/etc/mail/aliases` 和 `/etc/hosts`，存储在 NIS 服务器上。相关的数据库选项 `NISPLUS` 和 `YCOMPAT` 在 Linux 系统中很少使用。`NIS+` 是 NIS 的升级版本，在 Linux 环境中未使用；`YCOMPAT` 创建了与多年未生产的 NIS 版本兼容的兼容性。`YCOMPAT` 允许使用“加号语法（plus syntax）”，即在本地管理数据库末尾放置 `a+`，告诉系统首先搜索本地数据库，然后搜索 NIS 服务器上的数据库。通过 `YCOMPAT` 和在 `/etc/mail/aliases` 数据库末尾添加 `+`，Sendmail 会先检查本地别名数据库，然后检查 NIS 服务器，而无需使用过时的语法（在 Linux 系统上设置 NIS 服务器的详细信息见本系列中的《Linux DNS 服务器管理》一书）。

要强制 Sendmail 使用这些数据库选项，你可以编辑 `devtools/OS/linux.m4` 文件，或者在 `devtools/Site` 目录下创建一个包含以下行的行的文件：

```
define(`confDEFMAP`, `-NEWDB -NIS -DMAP_REGEX -DUSERDB`)
```

# 添加数据库支持

一旦在选择的文件中插入该行，请重新编译 Sendmail 以生效。（编译 Sendmail 的说明请参见第 3 章。）

然而，在费这些精力之前，请检查你的 Sendmail 程序已在使用哪些选项。默认数据库选项设置取决于 Sendmail 源码分发版构建程序所检测到的数据库库。在 Linux 系统上，默认通常是 `-DNEWDB`。但构建程序能够很好地检测你系统的能力，因此你的 Sendmail 程序可能包含额外的选项。列表 6.1 显示了在随随 `sendmail-8.11.0.i386.rpm` 文件分发的 Sendmail 程序中编译入的选项。

## 列表 6.1 检查 sendmail 编译选项

```
[root]# sendmail -bt -d0.4
Version 8.11.0
Compiled with: MAP_REGEX LOG MATCHHEGECOS MIME7TO7 MIME8TO7 NAMED_BIND
NETINET NETWOB NEWDB NIS QUEUE SASL SCANF SFIOT
STARTLS USERDB
canonical name: wren.foobirds.org
a.k.a.: wren
UUCP nodename: wren.foobirds.org
a.k.a.: wren
a.k.a.: [172.16.12.3]

========== SYSTEM IDENTITY (readcf) ==========
(short domain name) Sw = wren
(canonical domain name) Sj = wren.foobirds.org
(subdomain name) Sm = foobirds.org
(node name) $ = wren.foobirds.org
==================================
```

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
^ >
```

列表 6.1 显示了 Sendmail 在 `-bt` 测试模式下运行。同时 Sendmail 还接收了调试值 `-d0.4`。该调试值会导致 Sendmail 在接受输入之前显示几行信息。我们并没有真正要给 Sendmail 处理的输入；我们只是想查看显示内容，然后使用 `Ctrl+D` 退出。Sendmail 程序显示的第一行告诉我们这是 Sendmail 8.11.0。第二行是我们感兴趣的行。它列出了 Sendmail 编译时包含的所有选项。其中四个 `MAP_REGEX`、`NEWDB`、`NIS` 和 `USERDB` 与数据库相关，且 (img/b8082498451dba2bf0cf2907c85c4c83_0.png) 是我们想要的四个选项。

