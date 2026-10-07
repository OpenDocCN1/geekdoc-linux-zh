

## 列表 9.8 nullclient 配置示例

```bash
[root]$ cat client-only.mc
OSTYPE(linux)
FEATURE(`nullclient', 'wren.foobirds.org')
[root]# m4 ../cf.m4 client-only.mc > client-only.cf
[root]# grep 'wren' client-only.cf
DSwren.foobirds.org
Dwren.foobirds.org
DMwren.foobirds.org
```

在这种情况下，我们不使用 DOMAIN 名称宏配置文件。相反，我们用一个仅包含两行的 `client-only.mc` 文件替换了整个配置。与我们在书中创建的所有其他控制文件不同，`client-only.mc` 甚至不包含 `MAILER` 命令。文件中的两行：是一个必需的 `OSTYPE` 命令，用于指定我们运行的是 Linux；另一个是 `FEATURE` 命令，用于创建 nullclient 配置。`nullclient` 特性需要一个参数来识别外部服务器。在列表 9.8 中，远程服务器识别为 `wren.foobirds`。

当 `client-only.mc` 文件通过 `m4` 处理生成 `client-only.cf` 文件时，你可能会惊讶地发现，这个配置文件的并不并不任何其他 `sendmail.cf` 文件小。`nullclient` 特并没有产生截然不同的配置。它的作用是返回 `S`、`H` 和 `M` 变量中的参数值。`S`、`H` 和 `M` 直接指导 nullclient 配置中邮件的处理方式。

你通过伪装（masquerading）的讨论已经熟悉 `M` 变量。与 `nullclient` 特性相关的参数被用作伪装值，这样如果邮件来自外部服务器，来自客户端的所有邮件都将被伪装。

`S` 变量持有 `SMART_HOST` 继器的名称。`SMART_HOST` 是用于所有出站邮件的服务器。`H` 变量持有 `MAIL_HUB` 服务器的名称，它收集所有邮件，甚至是从一个本地用户发送给另一个本地用户的邮件。`MAIL_HUB` 的角色特别令人惊讶，因为本地邮件实际上并没有在本地处理：邮件被发送到 `MAIL_HUB`。如果 `H` 设置为一个值，当邮件地址是本地用户时，规则集 `localaddr`（规则集 5）会将邮件发送到由变量 `H` 指定的主机。

> nullclient 配置创建了邮件循环的可能性。如果 `MAIL_HUB` 上的别名或 `.forward` 文件将邮件转发回给客户端，客户端可能会将邮件发回 `MAIL_HUB`，从而触发邮件循环。不要从 `MAIL_HUB` 将邮件转发到其客户端。客户端使用单独工具（如 IMAP）下载邮件是最安全的。

## 配置继器客户端

`nullclient` 特性是创建一个仅客户端的 Sendmail 配置的简单方法。像许多简单解决方案一样，它缺乏灵活性。使用 `nullclient` 时，`SMART_HOST` 和 `MAIL_HUB` 被设置为相同的值。这可能不是你所想要的。你可能不想同时使用 `SMART_HOST` 和 `MAIL_HUB`。可以使用两个 `define` 命令来构建你需要的客户端配置。

`define(SMART_HOST, mailer:server)` `SMART_HOST` 选项允许你识别用于客户端出站邮件的外部服务器。可选的 `mailer` 值可用于指定将邮件继到外部服务器的继器。简单来说，如果 `SMART_HOST` 选项没有使用 `mailer` 值，则使用默认继器来将邮件继到外部服务器。提供的 `SMART_HOST` 选项的值将按其输入格式存储在变量 `S` 中——即 `mailer:server` 或直接是 `server`。

`define(MAIL_HUB, mailer:server)` `MAIL_HUB` 选项识别客户端用于入站邮件的外部服务器。同样，可以指定可选的 `mailer`，如果没有指定，则使用默认继器将邮件继到服务器。为 `MAIL_HUB` 指定的值将按照输入的内容写入变量 `H`。

> **注意**：除了灵活性外，使用 `SMART_HOST` 和 `MAIL_HUB` 相比 `nullclient` 的优势在于你可以选择要使用的继器。如果你在 `nullclient` 中使用 `mailer:server` 格式，`mailer:server` 值将写入 `S`、`H` 和 `M`，导致无效的伪装值。

当使用 `MAIL_HUB` 时，所有本地用户都被设置为 `MAIL_HUB`。这可能不是你想要的。例如，你可能不想将发给 root 的邮件发送到 `MAIL_HUB` 递送。即使定义了 `MAIL_HUB`，可以使用 `LOCAL_USER` 宏来识别本地用户。例如，以下命令防止将发给 root 的邮件发送到 `MAIL_HUB`：

```
LOCAL_USER(root)
```

`LOCAL_USER` 宏将值添加到类 `L`。没有从文件加载类 `L` 的宏。要从文件加载类 `L`，请使用 `sendmail -cf` 命令。假设你有一个名为 `/etc/mail/local-user` 的文件，包含不应发送到 `MAIL_HUB` 的用户列表。你可以在宏配置中添加以下内容将文件加载到类 `L`：

```
LOCAL_CONFIG
/etc/mail/local-users
```

相反，可能某些用户的邮件应该发送到 `MAIL_HUB`，尽管这些用户并不是真正的本地用户。“伪本地”用户的概念需要一些

## 特殊配置

nullclient 配置创建了邮件循环的可能性。如果 `MAIL_HUB` 上的别名或 `.forward` 文件将邮件转发回给客户端，客户端可能会将邮件发回 `MAIL_HUB`，从而触发邮件循环。不要从 `MAIL_HUB` 将邮件转发到其客户端。客户端使用单独工具（如 IMAP）下载邮件是最安全的。

nullclient 特性是创建仅客户端的 Sendmail 配置的简单方法。像许多简单解决方案一样，它缺乏灵活性。使用 `nullclient` 时，`SMART_HOST` 和 `MAIL_HUB` 被设置为相同的值。这可能不是你所想要的。你可能不想同时使用 `SMART_HOST` 和 `MAIL_HUB`。可以使用两个 `define` 命令来构建你需要的客户端配置。

`define(SMART_HOST, mailer:server)` `SMART_HOST` 选项允许你识别用于客户端出站邮件的外部服务器。可选的 `mailer` 值可用于指定将邮件继到外部服务器的继器。简单来说，如果 `SMART_HOST` 选项没有使用 `mailer` 值，则使用默认继器将邮件继到外部服务器。提供的 `SMART_HOST` 选项的值将按其输入格式存储在变量 `S` 中——即 `mailer:server` 或直接是 `server`。

`define(MAIL_HUB, mailer:server)` `MAIL_HUB` 选项识别客户端用于入站邮件的外部服务器。同样，可以指定可选的 `mailer`，如果没有指定，则使用默认继器将邮件继到服务器。为 `MAIL_HUB` 指定的值将按照输入的内容写入变量 `H`。

> **注意**：除了灵活性外，使用 `SMART_HOST` 和 `MAIL_HUB` 相比 `nullclient` 的优势在于你可以选择要使用的继器。如果你在 `nullclient` 中使用 `mailer:server` 格式，`mailer:server` 值将写入 `S`、`H` 和 `M`，导致无效的伪装值。

