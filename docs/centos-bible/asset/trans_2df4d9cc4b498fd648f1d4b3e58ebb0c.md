
# 第四部分 网络

确保你运行的不是存在漏洞的 sendmail 守护进程。此外，`expn` 和 `vrfy` 命令（可以通过配置选项禁用）可能会泄露比你愿意分发的更多信息。

```
May 16 13:03:27 dale sendmail[699]: NOQUEUE: "wiz" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:29 dale sendmail[699]: NOQUEUE: "debug" command from localhost [127.0.0.1] (127.0.0.1)
May 16 13:03:37 dale sendmail[701]: NOQUEUE: localhost [127.0.0.1]: expn oracle
May 16 13:03:43 dale sendmail[702]: NOQUEUE: localhost [127.0.0.1]: vrfy oracle
```

## 配置 Sendmail

为了配置 Sendmail 功能，你需要编辑 `/etc/mail/` 和 `/etc/` 中的配置文件，这些文件随后会被 Sendmail 启动脚本用于生成数据库文件。这些数据库文件反过来又被 sendmail 守护进程使用，以控制你的 Sendmail 服务器的行为。一旦 Sendmail 配置完成，你就可以开始添加用户账户以在你的服务器上创建邮箱。本章节描述配置 Sendmail 的一般步骤如下：

- 1. **获取域名** — 你需要为你的邮件服务器分配一个唯一的互联网域名。你可以从许多不同的地方购买互联网域名，然后让你的域名的 DNS 邮件交换（MX）记录指向你要创建的邮件服务器。

- 2. **配置基本 Sendmail 设置** — 在这一步中，你编辑 `/etc/mail/sendmail.mc` 文件。该文件定义了其他配置文件和日志文件的位置，并允许你配置 sendmail 守护进程的某些行为。

- 3. **定义出站邮件访问** — 与你的邮件服务器相关的最关键的安全问题是它接受哪些邮件消息并中继到其他邮件服务器。通过编辑 `/etc/mail/access` 文件，你可以指定你的服务器将从哪些主机和用户接受用于本地投递或中继的邮件。

- 4. **配置虚拟服务器** — 默认情况下，Sendmail 假设你正在为服务器所属的域名设置邮件服务器。要让单台计算机上的 Sendmail 成为多个域名（称为*虚拟服务器*）的邮件服务器，你需要在 `/etc/mail/local-host-names` 文件中定义每个域名。（你必须手动创建 local-host-names，因为它不在 sendmail 软件包中。）

- 5. **配置虚拟用户** — 使用 `/etc/mail/virtual/ustable` 配置文件，你可以指示 sendmail 守护进程如何处理它收到的、针对其配置要处理的用户和域名的邮件。这个文件给你很大的灵活性，可以将发送给特定用户的邮件指向特定的邮箱，转发到不同的邮件地址，或者以各种方式拒绝该邮件。要使用 virtual/ustable，你必须手动创建该文件，因为它不在 sendmail 软件包中。

- 6. **添加用户账户** — 你需要为每个在你的邮件服务器上拥有邮箱的用户添加一个用户账户。

- 7. **启动 Sendmail 并生成数据库文件** — 启动 Sendmail 服务会引发两个主要操作。它运行 `sendmail` 服务器守护进程，并将你的配置文件编译成 Sendmail 可使用的数据库文件。如果服务器已经在运行，你可以简单地编译配置文件，使任何新设置生效，而无需重启服务器。

以下小节将详细介绍这些步骤中的每一个。

### 获取域名

为了让人们能够向你的邮件服务器上的用户发送邮件，你必须拥有自己的域名。第 24 章描述了如何获取自己的域名并设置 DNS 服务器。对于你的邮件服务器而言，关键问题是确保 DNS 服务器上你域名的 MX 记录指向你邮件服务器的地址。

> **注意**：你的 ISP 可能不允许你在家庭互联网账户上拥有私有邮件服务器。为了强制实施这一点，ISP 可能会阻止发往端口 25 的数据包。在你能在该连接上设置邮件服务器之前，可能需要联系他们开放该端口。由于许多垃圾邮件发送者以及其他不良（至少是控制不佳的）电子邮件服务器试图隐藏在动态 IP 地址之后，许多 ISP 既不允许使用动态 IP 地址的电子邮件地址，也不接受从这些服务器发送的电子邮件。

### 配置基本 Sendmail 设置 (sendmail.mc)

你的 Sendmail 服务器的大部分配置来自 `/etc/mail/sendmail.mc` 文件中的信息。由于该文件设置了 Sendmail 的默认值，这些值在大多数情况下都可以使用，因此你可能不需要对 `sendmail.mc` 做太多修改。然而，我建议逐步浏览本节，以便你理解你的邮件服务器是如何配置的。

你对 `sendmail.mc` 文件所做的更改不会立即生效。首先，你必须编译 `sendmail.mc` 设置以生成 `/etc/mail/sendmail.cf` 文件。我在“启动 Sendmail 并生成数据库文件”一节中描述了如何执行此操作。

生成的 `/etc/mail/sendmail.cf` 文件包含超过 1,800 行用于指导你的 `sendmail` 守护进程行为的设置和注释。你在 `sendmail.mc` 文件中使用的 `m4` 宏与 `sendmail.cf` 文件中的最终设置不同。

> **注意**：m4 实用程序可用于处理包含 IEEE 标准 1003.1-2001 格式宏的文本文件（第 12.2 节，“实用程序语法指南”）。该编译器对你是使用单引号还是反引号非常敏感，因此在编辑 `sendmail.mc` 时要小心。有关 m4 实用程序的详细信息，请输入 `info m4`。

要查找在 `sendmail.cf` 文件中找到的设置应使用哪些宏，请参阅 `/usr/share/doc/sendmail*/README.cf` 文件。

> **警告**：由于 CentOS 中 *Sendmail* 的配置方式，你不应该直接修改 *sendmail.cf* 文件。当 *Sendmail* 重启或 *sendmail.mc* 发生变更时，*sendmail.cf* 文件会自动重新生成。因此，任何直接对 *sendmail.cf* 所做的修改都将丢失。

以下代码示例来自随 CentOS 版本 *Sendmail* 附带的 */etc/mail/sendmail.mc* 文件。

> **注意**：在 *sendmail.mc* 文件中以 *dnl*（“delete to new line”，即删除至行尾）开头的行是注释行。在大多数情况下，我在示例中省略了它们。此外，请注意 *Sendmail* 使用反引号作为开引号，使用直引号作为闭引号。

```
divert(-1)dnl
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
VERSIONID(`setup for linux')dnl
OSTYPE(`linux')dnl
```

*sendmail.mc* 文件的前几行做一些事务性工作。`divert` 行在生成配置文件时移除了多余的输出。`include` 行引入了 `Sendmail` 所需的规则集。`VERSIONID` 行标识该配置文件是用于 Linux 系统的（如 `CentOS`）（尽管此设置不受检查，因此可以是任何你喜欢的值）。然而，`OSTYPE` 必须设置为 `linux` 才能获取 `Sendmail` 所需文件的正确位置。

```
dnl define(`confSMTP_LOGIN_MSG', '$j Sendmail; $b')dnl
dnl define(`SMART_HOST', `smtp.your.provider')
```

这里有两行你可以考虑取消注释（移除 `dnl` 字符串）。`confSMTP_LOGIN_MSG` 定义可用于隐藏你正在使用的邮件服务器（将 `Sendmail` 更改为任何你喜欢的内容）。至于第二行，默认情况下，`sendmail` 守护进程会尝试将你的出站电子邮件直接发送到其地址所属的邮件服务器。如果你希望所有电子邮件都通过特定的邮件服务器中继，你可以移除 `SMART_HOST` 行开头的注释（`dnl`，意为“delete to new line”）（保留行末尾的那个）。然后，将 `smtp.your.provider` 更改为你想要使用的邮件服务器的完全限定域名。当然，你需要确保你定义的 `SMART_HOST` 会接受来自你邮件服务器的中继。

```
define(`confDEF_USER_ID', `8:12')dnl
```

守护进程不以 `root` 用户身份运行，而是以 `mail` 用户（UID 8）和 `mail` 组（GID 12）身份运行，这是基于之前设置的 `confDEF_USER_ID` 行。这是一项良好的策略，因为它可以防止可能入侵你邮件服务器的人获得你机器的 root 访问权限。

```
dnl define(`confAUTO_REBUILD')dnl
define(`confIO_CONNECT', `1m')dnl
```
