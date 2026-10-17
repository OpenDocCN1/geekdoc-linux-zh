
语法：`nsswitch.conf`中的每行都指定如何搜索某条信息（例如用户密码）。`nsswitch.conf`中的某行具有以下语法：

```
info:
method [[action]] [method [[action]]...]
```

其中`info`是该行描述的类型，`method`是用于查找信息的方法，`action`是对返回状态的响应。当调用以提供`nsswitch.conf`描述的信息时，系统会检查带有适当`info`字段的行。使用该行上指定的方法，从左侧开始。当找到信息时，系统停止搜索。在没有指定`action`的情况下，当某种方法失败时，系统会尝试下一个。`action`包含在括号内。搜索可能会在未找到请求信息的情况下结束。

# 信息

`nsswitch.conf`文件通常控制用户名、密码、主机 IP 地址和组信息。以下列表描述了`nsswitch.conf`控制的大多数信息类型（前文给出的`info`）：

- automount (`/auto.master`；第 811 页）
- bootstrap 无盘启动选项（bootstrap 手册）
- MAC 地址（第 1174 页）
- 组 (`/etc/group`；第 506 页）
- 系统信息 (`/etc/hosts`；第 507 页）
- 网络信息
- 用户信息 (`/etc/passwd`；第 508 页）
- 协议信息（第 510 页）
- 密码信息 (`/etc/shadow`；第 511 页）

# 方法

以下是`nsswitch.conf`控制的信息类型列表。对于每种信息，你可以指定以下一个或多个方法：

- compat `passwd`、`group` 和 `shadow` 语法（第 496 页）
- dns 查询 DNS (`hosts`)
- files 搜索本地文件，如 `/etc/passwd` 和 `hosts`
- ldap 查询 LDAP 服务器（第 777 页）
- nis 查询 NIS 数据库

# 顺序

两个或多个方法提供的信息可能会冲突：例如，`files` 和 `nis` 可能为同一个用户提供信息。如果有冲突，你需要考虑哪种方法具有权威性（优先级），然后将该方法放在列表的左侧。默认情况下，`nsswitch.conf`文件列出没有`action`的方法假设没有冲突（这是正常的）。在这种情况下，顺序不是关键的：当一种方法失败时，系统将到下一个。当在方法之间使用`action`时，顺序就变得关键。`nsswitch.conf`的第一行导致系统在`/etc/passwd`中搜索密码信息，如果失败，则使用 NIS 查找。如果你查找的用户在两个地方都有，则本地文件信息被认为是权威的。第二行使用 NIS 查找主机地址；如果失败，则搜索`/etc/hosts`；如果失败，则通过 DNS 查找信息。

| passwd nis |

| hosts dns |

# 操作项

每个方法后面可选地跟一个`action`项，指定在方法成功或失败时做什么。`action`项具有以下格式：

```
[[STATUS=action]]
```

其中方括号是格式的一部分，不表示内容是可选；`STATUS`（按习惯大写）是正在测试的状态；`action`是当`STATUS`匹配前面的方法返回的状态时要采取的操作。前面的感叹号 (`!`) 是可选的，用于取反状态。

- 还存在其他不常用的方法。更多信息请参见默认的 `/etc/nsswitch.conf` 文件和 `nsswitch.conf` 手册。尽管 NIS 属于此列表，但它没有作为 Linux 服务器实现，书中未讨论。

`STATUS` 可能具有以下值之一：

- NOTFOUND——方法执行了，但没有找到要的值。默认操作是 `continue`。
- SUCCESS——方法执行了，且找到了值；没有返回错误。默认操作是 `return`。
- TRYAGAIN——方法失败是因为临时不可。例如，文件可能被锁定或服务器过载。默认操作是 `continue`。
- AVAIL——方法失败是因为永久不可用。例如，无法访问文件或服务器可能宕机。默认操作是 `continue`。

`action` 有两个可能的值：

- return——不带值返回调用程序。
- continue——继续下一个方法。任何返回的值会被后续方法的值覆盖。

示例：`nsswitch.conf`中的下一行导致系统首先通过 DNS 查找给定主机的 IP 地址。DNS 方法之后的 `action` 项测试方法返回的状态是否不是 (`!`) AVAIL。

```
hosts               dns [UNAVAIL=return] files
```

如果 DNS 方法没有返回 `AVAIL`（即 `UNAVAIL`——也就是说如果 DNS 返回 `SUCCESS`、`NOTFOUND` 或 `TRYAGAIN`），系统将采取与 `STATUS (return)` 相关的操作。结果是，方法 (`files`) 仅在 DNS 服务器不可用时使用。如果 DNS 服务器并非不可用（将两个否定读为“可用”），搜索将返回域名或报告未找到域名。只有当服务器不可用时，搜索才会使用 `files` 方法（检查本地的 `/etc/hosts` 文件）。

# compat 方法：passwd、group 和 shadow 文件中的 +

你可以在 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 文件中放入特殊代码，这使得你在 `nsswitch.conf` 中指定 `compat` 方法时，系统合并并修改本地文件和 NIS 映射中的条目。也就是说，在这些文件的某行开头加号 (`+`) 会添加 NIS 信息；减号 (`–`) 则移除它。

例如，要在 `passwd` 文件中使用这些代码，请在 `nsswitch.conf` 文件中指定 `passwd: compat`。系统会顺序遍历 `passwd` 文件，当到达每行以 `+` 或 `-` 开头的行时，添加或删除相应的 NIS 条目。

虽然你可以在 `passwd` 文件的末尾加加号，并在 `nswitch.conf` 中指定 `passwd compat` 来搜索本地 `passwd` 文件并遍历 NIS 映射，但通过在 `nswitch.conf` 中放置 `passwd: file nis` 而不修改 `passwd` 文件会更高效。

## 获取帮助

Fedora/RHEL 带有详尽的文档（第 125 页）。Fedora 维护了一个页面，指向 `docs.fedaproject.org/en/get-help` 上的许多实用支持文档，其中显示了如何访问 Fedora 论坛、邮件列表和 IRC 聊天室；Red Hat 在 `access.redhat.com` 维护了一个单一页面，并将文档保存在 `access.redhat.com/docs`。虽然这些 Red Hat 的某些部分需要账户才能访问，但任何人都可以免费获取账户。你还可以在系统管理员指南网站（`www.sage.org`）上找到帮助。互联网是另一个关于管理 Linux 系统的另一个丰富信息源；请参阅附录 B（第 1115 页）和作者的主页（`www.sobel.com`）以获取关于使用书籍本身的建议。

你不需要孤立地作为 Fedora/RHEL 系统管理员来工作；一个庞大的 RHEL 专家社区愿意帮助你充分利用 Linux 系统的价值。当然，如果你已经尝试通过阅读可用文档来解决问题，你将会获得更好的帮助。如果你无法通过查阅文档解决问题，在适当的新闻组（如 `comp.os.linux`）或邮件列表中发布一个经过深思的问题也可以产生有用的信息。务必准确描述问题并仔细识别系统。包含有关运行在系统上的 Fedora/RHEL 版本以及任何你认为与问题相关的其他软件和硬件的信息。`comp.os.linux` 新闻组的回答包含了常见问题的解决方案帖子，以及最新版本的 FAQ 和 HOWTO 文档的定期发布。请访问 `www.catb.org/~esr/faqs/smart-questions.html` 查看 Eric S. Raymond 和 Rick Moen 编写的非常有用的论文《如何聪明地提问》。

# 章节总结

系统管理员是为用户保持系统处于有用方便状态的人。你作为系统管理员的大部分工作将要求你以 root 权限工作。拥有这些权限的用户（有时称为超级用户）拥有着普通用户没有的广泛权限。具有 root 权限的用户可以读写任何文件，并执行普通用户未允许执行的程序。

系统管理员控制系统操作，包括以下任务：配置系统；启动；设置服务器；在单用户、多用户和救援模式下工作；关闭系统；处理系统崩溃。Fedora/RHEL 提供了图形和文本配置工具。许多图形化工具以 `system-config-*` 命名。

# 498 第 11 章 系统管理：核心概念

当你以单用户模式启动系统时，只有系统控制台是可用的。在单用户模式下工作时，你可以备份文件并在挂载之前使用 `fsck` 检查文件系统的完整性。`telinit` 工具可以将系统带入多用户模式，在该模式下你仍然可以执行许多管理任务，例如添加用户和打印机。
