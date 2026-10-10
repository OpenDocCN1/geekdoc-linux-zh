
# 第 19 章：设置邮件服务器 799

## 第四部分：Fedora 和 RHEL 网络设置

### 配置 sendmail

要配置 sendmail，你需要编辑 `/etc/mail` 中的文件，这些文件会被 sendmail 启动脚本用于创建数据库文件。一旦 sendmail 配置完成，就可以开始创建账户。在本节中描述的步骤为：

- **获取域名** — 你需要一个分配给邮件服务器的唯一域名，可以在许多地方购买互联网域名，然后让 DNS 邮件交换 `MX` 记录指向该邮件服务器。
- **配置 sendmail 设置** — 在此步中，你编辑 `/etc/mail/sendmail.mc` 文件。该文件定义了其他以及日志文件的位置，并允许你配置 sendmail 守护的行为。
- **定义邮件访问** — 与您的邮件服务器相关的关键安全性是它接受转发到其他邮件服务器的消息。通过编辑 `/etc/mail/access` 文件，你可以指示哪些主机和用户可以接受本地交付或转发邮件。
- **配置虚拟服务器** — 默认情况下，sendmail 假设你正在为服务器所属的域名设置邮件服务器。要让单台计算机上的 sendmail 为多个域名（称为虚拟服务器）提供邮件服务，你需要在 `/etc/mail/virtual` 中定义每个域名。（你必须手动创建该文件，因为它不在 sendmail 软件包中）。
- **配置虚拟用户** — 使用 `/etc/mail/virtertable` 配置文件，你可以指示 sendmail 守护进程如何处理为其配置的用户和域名接收的消息。这提供了很大的灵活性，可以将发给特定信箱的邮件转发到不同的邮件地址，或以各种方式拒绝该邮件。要使用 virtertable 你必须手动创建该文件，因为它不在 sendmail 软件包中。
- **添加用户账户** — 你需要为邮件服务器上每个信箱的每个添加用户账户。
- **启动 sendmail 并生成数据库文件** — 启动 sendmail 服务会导致两个主要操作：运行 sendmail 服务器守护进程，并将你的配置文件编译成 sendmail 可使用的数据库文件。如果服务器是

# 第 19 章：设置邮件服务器 801

如果服务器已经在运行，你只需重新编译配置文件即可使任何新设置生效，而无需重启服务器。

以下子节将提供这些步骤的详细说明。

## 获取域名

为了让人们能够向你邮件服务器上的用户发送邮件，你必须拥有一个自己的域名。第 25 章描述了如何获取自己的域名以及设置 DNS 服务器。对于你的邮件服务器来说，关键问题是确保 DNS 服务器上你的域名 `MX` 记录指向你邮件服务器的地址。

> 注意：你的互联网服务提供商（ISP）可能不允许你在家庭网络账户上拥有私有邮件服务器。为了执行这一限制，ISP 可能会阻止发往 25 端口的数据包。你可能需要联系他们开放该端口，以便你可以在该连接上设置邮件服务器。由于许多发送垃圾邮件或其他恶意的（或至少控制不当的）邮件服务器隐藏在动态 IP 地址之后，许多服务器既不允许来自动态 IP 地址的邮件地址，也不会接受来自这些服务器发送的邮件。

## 配置基础 sendmail 设置 (`sendmail.mc`)

你邮件服务器的大部分配置来自 `/etc/mail/sendmail.mc` 文件中的信息。该文件设置了大多数情况下使用的 sendmail 默认值，你可能不需要对 `sendmail.mc` 进行任何操作。我建议你检查此节，以便了解你的邮件服务器是如何配置的。

你对 `sendmail.mc` 文件所做的更改不会立即生效。首先，你必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 sendmail 并生成数据库文件”部分描述了如何操作。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1800 行设置和注释，用于引导你的 sendmail 守护进程的行为。你在 `sendmail.mc` 文件中使用的 m4 宏与 `sendmail.cf` 文件中的设置不同。

> 注意：`m4` 工具用于处理符合 IEEE 标准 1003.1-2001 格式的包含宏的文本文件（第 12.2 节。工具语法指南）。它对你如何使用单引号反引号非常敏感，因此在编辑 `sendmail.mc` 时要小心。有关 m4 工具的详细信息，请输入 `info m4`。

要找到设置 `sendmail.cf` 文件需要哪些宏，请参考 `/usr/share/doc/sendmail*/README.cf` 文件。如果你对 `sendmail.cf` 文件的内容感兴趣，我已经在 Fedora 10 和 Red Hat Enterprise Linux Bible 网站（http://www.wiley.com/go/fedora10bible）的下载文件中包含了 `sendmail.cf` 的详尽描述。

## 第四部分：Fedora RHEL 网络和服务器设置

> 警告：由于 Fedora 中 sendmail 的配置方式，你不应该直接修改 `sendmail.cf` 文件。当 `sendmail.mc` 发生变化时，sendmail 重启会自动重新生成 `sendmail.cf` 文件。因此，任何直接对 sendmail.cf 进行的修改将会丢失。

以下代码示例来自 Fedora 版本 sendmail 附的 `/etc/mail/sendmail.mc` 文件。

> 注意：`sendmail.mc` 文件中以 `dnl`（删除到换行）开头的行是内容。在大多数情况下，我在示例中省略了它们。此外，注意 sendmail 使用反引号作为起始引号，使用直引号作为引号。

```
divert(-dnl)

include(/usr/share/sendmail-cf/m4/cf.m4)*dnl

VERSIONID setup for Linux)*dnl

OSTYPE(linux)*dnl
```

`sendmail.cf` 的前几行进行清理工作。`divert` 行在生成配置文件时移除了额外的输出。`include` 行导致 sendmail 设置的规则生效。`VERSIONID` 标识配置文件用于 Linux 系统的，或者是 Fedora 的（尽管没有检查此设置，所以可以设置为你喜欢的任何内容）。然而，`OSTYPE` 必须设置为 linux，以获取 sendmail 所需的行的正确位置。

```
dnl define(confSMTP_LOGIN_MSG, `Sendmail: Sb')dnl

def('SMART_HOST', `smtp.your.provider`)*dnl
```

这里有两行你可以考虑取消注释（删除 `dnl` 字符串）。`confSMTP_LOGIN_MSG` 的定义可以用于伪装你正在使用的 sendmail 服务器（将 sendmail 更改为任何内容）。但是，对于第二行，默认情况下，sendmail 守护进程会尝试将你的出站邮件直接发送到邮件服务器；如果你想让所有邮件中继到特定的邮件服务器，你可以删除上方 `SMART_HOST` 行开头的 `dnl`（代表“删除到换行”），在末尾留一个。然后将 `smtp.your.provider` 更改为你想要使用的邮件服务器的全限定域名。当然，你需要确保你定义的 `SMART HOST` 接受来自你邮件服务器的中继。

```
define(confDEF_USER_ID, `8:12`)*dnl
```

根据之前设置的 `dnl` 行，守护进程不再以 root 身份运行，而是以用户（UID 8）和组（GID 12）身份运行。这是一个很好的策略，因为它可以防止任何可能通过 `confDEF_USER_ID` 损害你邮件服务器的人获取对你机器的 root 权限。

```
dnl define(confAUTO_REBUILD)*dnl

define(conf_CONNECT, `lm`)*dnl
```

# 第 19 章：设置邮件服务器 803

如果你删除了初始的 `dnl`，`confAUTO_REBUILD` 行将告诉 sendmail 自动重建别名数据库。`CONF_CONNECT` 行设置了 sendmail 将等待初始连接一分钟（1m）。

```
define(CONTRY_NULL_MX_LIST, `True`)dnl

define(CONFDONT_PROBE_INTERFACES, `True`)dnl
```

当 `CONFTRY_NULL_MX_LIST` 为真时，如果接收服务器是主机的最佳交换（MX），sendmail 将尝试直接连接到该主机。如果 `CONF_PROBE_INTERFACES` 为真，sendmail 将不会将本地接口插入地址列表中。

```
define(`PROMAIL_MAILER_PATH`, `/usr/bin/procmail1`)dnl

define(`ALIAS_FILE`, `/etc/aliases`)dnl

dnl define(`STATUS_FILE`, `/var/log/mail/statistics`)dnl
```
