

# 第 11 章 电子邮件

关于 LDAP 的更多信息，请参见第 13 章轻量级目录访问协议 (LDAP)。

## 11.3.2. Fetchmail

Fetchmail 是一种 MTA（邮件传输代理），它可以从远程服务器检索电子邮件并将其投送到本地 MTA。许多用户非常欣赏将下载远程服务器上消息的过程与在 MTA 中读取和组织消息的过程分开的能力。Fetchmail 在设计时考虑了拨号上网用户的需求，它可以使用任何协议（包括 POP3 和 IMAP）连接并将所有邮件消息下载到邮件队列（mail spool）中。如有必要，它甚至可以将邮件消息转发到 SMTP 服务器。

Fetchmail 通过使用用户主目录下的 `.fetchmailrc` 文件为每个用户进行配置。

通过 `.fetchmailrc` 文件中的偏好，Fetchmail 会检查远程服务器上的邮件并将其拉取。如果它尝试将邮件投送到本地机器的 25 端口，将使用本地 MTA 将邮件放入正确用户的队列中。如果 Proxym 可用，可以使用它来获取邮件并将其放入邮箱，以便 MTA 读取。

### 11.3.2.1. Fetchmail 配置选项

虽然在执行 Fetchmail 时可以通过命令行传递任何选项来检查远程服务器上的邮件，但使用 `.fetchmailrc` 文件要简单得多。所有的配置选项都位于 `.fetchmailrc` 中，并且可以在运行 Fetchmail 时通过在命令行指定该选项来覆盖它们。

用户的 `.fetchmailrc` 文件分为三种特殊类型的配置选项：

- 全局选项 (global options) —— 为 Fetchmail 提供指令，控制操作或为每个检查邮件的账户提供设置。
- 服务器选项 (server options) —— 指定被轮询服务器的信息，例如主机名，以及针对特定电子邮件服务器的偏好设置，例如检查端口或在超时前等待的秒数。这些选项会影响使用该服务器的所有用户。
- 用户选项 (user options) —— 包含使用特定服务器进行身份验证和检查邮件所需的信息，例如用户名和密码。

全局选项出现在 `.fetchmailrc` 文件的顶部，随后是一个或多个服务器选项，每个选项都指定了 Fetchmail 应该检查的不同服务器。对于每个检查邮件的账户，用户选项位于服务器选项之后。与服务器选项一样，用户选项可以为特定服务器指定，也可以用于检查同一服务器上的多个账户。

服务器选项通过 `.fetchmailrc` 文件中的特殊动词选项——`poll`（轮询）或 `skip`（跳过）调用，该选项位于任何服务器信息之前。`poll` 操作告诉 Fetchmail 在运行时使用此服务器选项，实际上会根据各种用户选项检查邮件。在 `skip` 操作之后的用户选项除非在调用 Fetchmail 时指定了此服务器主机名，否则不会被检查。`skip` 选项在 `.fetchmailrc` 中设置测试配置，并仅在需要时检查该服务器，而不影响任何工作中的配置。

一个示例 `.fetchmailrc` 文件如下所示：

```
set postmaster "user"
set bouncemail
poll pop.domain.com proto pop3
user 'user' there with password 'secret' is user here
```

mail.domain.com

```
user 'user5' there with password 'secret2' is user here
user 'user7' there with password 'secret3' is user here
```

在此示例中，全局选项被设置为用户作为最后手段（`postmaster` 选项）发送，并且所有错误都发送给发送者的邮件管理员（`bouncemail` 选项）。`set` 操作告诉 Fetchmail 这一行包含全局选项。然后指定了两个服务器，一个设置为使用 POP3 检查，另一个尝试各种协议以确定是哪一个。使用第二个服务器选项检查两个用户，但所有邮件都发送到用户的邮件池中。这允许在多个服务器上检查多个邮箱，同时出现在单个 MUA（邮件用户界面）收件箱中。每个用户的特定信息都以 `user` 操作开头。

# 注意

用户并不要求将密码放置在 `.fetchmailrc` 文件中。省略 `<password>` 部分会导致 Fetchmail 在启动时询问密码。

Fetchmail 包含许多全局、服务器和本地选项。这些选项中的许多很少被使用，或仅适用于非常特定的情况。`fetchmail` 页面详细解释了每个选项，但这里列出了最常用的选项。

## 11.3.2. 全局选项

每个选项都应放置在 `set` 动作之后的单行中。

- `daemon <seconds>` — 指定守护进程模式，其中 Fetchmail 将留在后台并按指定的间隔轮询邮件。
- `postmaster` — 指定一个本地用户，用于在投递出现问题时发送邮件。
- `syslog` — 指定错误和状态消息的日志。默认路径为 `/var/log/mailog`。

## 11.3.3. 服务器选项

服务器选项应放在 `.fetchmailrc` 中 `poll` 或 `skip` 动作之后的单独行上。

- `auth <auth-type>` — 指定使用的身份验证类型。默认使用密码认证，但协议支持其他类型的身份验证，包括 `kerberos_v5`、`kerberos_v4` 和 `ssh`。如果使用了任何认证，Fetchmail 会尝试不需要密码的方法，然后是掩码密码的方法，最后尝试将明加密密码发送到服务器。
- `interval <number>` — 每检查所有已配置服务器 `<number>` 次时，轮询一次指定的服务器。此选项用于用户很少接收消息的邮件服务器。
- `port <port-number>` — 覆盖默认端口。
- `proto <protocol>` — 指定用于检查消息的协议，如 `pop3` 或 `imap`。
- `timeout <seconds>` — 指定 Fetchmail 放弃连接之前的服务器空闲时间。如果未设置此值，默认为 300 秒。

## 11.3.2.4. 用户选项

用户选项可以放在服务器选项之后的单独行，也可以与服务器选项在同一行。无论何种情况，定义的选项必须遵循用户选项。

- `fetchall` — 命令 Fetchmail 下载队列中的所有消息，包括已查看的消息。默认情况下，Fetchmail 只拉取新消息。
- `fetchlimit <number>` — 允许检索指定数量的消息。
- `flush` — 通知 Fetchmail 在拉取新消息之前删除队列中所有已查看的消息。
- `limit <max-number-bytes>` — 指定仅检索特定大小的消息。这对于大邮件下载过慢的网络链接有用。
- `password <password>` — 指定此用户使用的密码。
- `preconnect <command>` — 在为用户检索消息之前执行指定的命令。
- `postconnect <command>` — 在为用户检索消息之后执行指定的命令。
- `ssl` — 激活 SSL加密。
- `user <username>` — 设置 Fetchmail 使用的用户名。此选项应列在其他用户选项之前。

## 11.3.2.5. Fetchmail 命令行选项

大多数 Fetchmail 可以在执行 `.fetchmailrc` 配置选项时在命令行使用。大多数用户不会配合配置文件使用它。大多数人不会在命令行使用这些选项，因为将它们留在 `.fetchmailrc` 文件中以便运行 Fetchmail 时使用更为简单。

然而，有时可能需要为了特定目的带有其他选项运行 fetchmail 命令。可以通过命令行选项来临时覆盖导致错误的 `.fetchmailrc` 设置，因为在命令行指定的任何选项都会覆盖配置文件。

## 11.3.2.6. 信息或调试选项

在 `fetchmail` 命令之后使用的某些选项可以提供重要信息。

-- config — 根据 `.fetchmailrc` 信息和 Fetchmail 默认值显示所有可能的选项。使用此选项的用户不会检索任何邮件。
- -s — 以静默模式运行 Fetchmail，防止在 fetchmail 命令后出现错误以外的任何消息。
- -v — 以详细输出模式运行 Fetchmail，显示 Fetchmail 与远程服务器之间的所有通信。
- -V — 显示详细的版本信息，列出其全局选项，并显示与每个用户的设置，包括邮件协议和身份验证方法。使用此选项的用户不会检索任何邮件。

