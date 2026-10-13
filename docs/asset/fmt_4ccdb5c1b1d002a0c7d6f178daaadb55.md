
```
divert(-1)
This is the macro config file used to generate
the /etc/mail/sendmail.cf file. If you modify the file, you will have to regenerate /etc/mail/sendmail.cf by running the m4 macro config through preprocessor
divert(0)
```

为了让 Sendmail 能够正常工作，只需要定义 `OSTYPE` 和 `MAILERS` 宏，以及任何所需的特性和选项即可。这里展示了一个非常简单的 Sendmail 文件。

`mysendmail.mc`

```
dnl My sendmail.mc file
OSTYPE('linux')
define('PROCMAIL_MAILER_PATH','/usr/bin/procmail')
FEATURE(redirect)
MAILER(procmail)
MAILER(smtp)
```

`sendmail.mc` 文件通常包含更多条目，特别是用于参数和特性。请检查您的 Red Hat 系统上的 `/etc/mail/sendmail.mc` 文件，以查看 Sendmail 的标准默认条目。

## Sendmail 伪装（Masquerading）

对于将本地主机的消息中继到 Internet 的邮件服务器，您可能希望伪装消息的来源。在拥有连接到 Internet 的自有邮件服务器的大型网络中，Sendmail 伪装可以使本地主机发送的消息看起来像是由邮件服务器发送的。它们的主机地址将被邮件服务器的地址替换。退回的邮件可以发送到邮件服务器，并保存在 POP 或 IMAP 服务器邮箱中，以便稍后由本地主机上的用户访问。此外，服务器虚拟用户表中的条目可以将邮件转发到本地主机上对应的用户。

伪装通常用于用域名来掩盖本地主机。任何子域名也可以被伪装。这种方法可以应用于 ISP 或网络管理员为您的网络分配了独立域名的情况。您可以将所有邮件消息掩盖为来自您的域名，而不是来自特定主机或您可能拥有的任何子域名。例如，如果一个网络的官方域名是 `mytrek.com`，那么 `mytrek.com` 网络中主机（如 `rabbit.mytrek.com` 和 `turtle.mytrek.com`）的所有消息都可以被伪装为仅来自 `mytrek.com`。如果 `mytrek.com` 网络有一个域名为 `mybeach.com` 的子网络，那么来自 `mybeach.com` 的任何消息也可以被伪装为来自 `mytrek.com`。

通过 `MASQUERADE_AS` 命令开启伪装。它接受您希望伪装邮件来源的名称作为参数。通常，使用的名称仅是域名，不包含邮件主机。在以下示例中，邮件被伪装为简单的 `mytrek.com`。从 `turtle.mytrek.com` 这样的本地主机发送的邮件将看起来像是仅由 `mytrek.com` 发送的：

```
MASQUERADE_AS('mytrek.com')dnl
```

您还必须指定本地网络中您的 Sendmail 服务器应进行伪装的主机和域。如果您决定伪装本地网络中的所有主机，只需设置 `masquerade_entire_domain` 特性，如下所示：

```
FEATURE('masquerade_entire_domain')dnl
```

相反，如果您希望伪装特定主机，或者您的域有多个需要伪装的子域名，请在 `MASQUERADE_DOMAIN` 条目中列出它们。您可以列出特定主机或整个域。例如，给定一个本地网络，其中本地主机为 `turtle.mytrek.com` 和 `rabbit.mytrek.com`，您可以通过 `MASQUERADE_DOMAIN` 列出它们以进行伪装。它们被伪装成的域名在 `MASQUERADE_AS` 条目中指定。

```
MASQUERADE_DOMAIN('turtle.mytrek.com rabbit.mytrek.com')dnl
```

如果您希望伪装本地网络中的所有主机，只需列出本地网络的域名。如果您的本地网络还支持多个子域名，也可以列出它们以进行伪装。例如，要伪装 `mybeach.com` 域中的所有主机，请使用以下条目：

```
MASQUERADE_DOMAIN('mytrek.com mybeach.com')dnl
```

如果您有一长串域名或主机列表，或者希望能够轻松更改应被伪装的对象，可以将它们放在一个文件中供 Sendmail 读取。使用 `MASQUERADE_DOMAIN_FILE` 命令指定该文件： `MASQUERADE_DOMAIN_FILE('mydomains')dnl`

如果您只想伪装本地域中的所有主机，请使用 `masquerade_entire_domain` 特性： `FEATURE(masquerade_entire_domain)dnl`

本地网络的常见配置会在 `MASQUERADE_AS` 条目和 `MASQUERADE_DOMAIN` 条目中指定域名。以域名 `myisp.com` 为例，条目将如下所示： `MASQUERADE_AS('mytrek.com')dnl` `FEATURE(masquerade_entire_domain)dnl`

如果您希望伪装成 ISP 的邮件域，请在 `MASQUERADE_AS` 条目中使用 ISP 的域名，如下所示： `MASQUERADE_AS('myisp.com')dnl` `MASQUERADE_DOMAIN('mytrek.com')dnl`

当从外部接收仅带有 `mytrek.com` 地址的邮件时，您的网络需要知道将其发送到哪个主机。这是指定为 `mytrek.com` 网络邮件服务器的主机。这些信息由 DNS 配置中的邮件交换记录（MX）提供，该记录将指定邮件发送到 `mytrek.com` 的邮件将由邮件服务器处理——在本例中为 `turtle.mytrek.com`：

```
mytrek.com. IN MX 0 turtle.mytrek.com.
```

你还必须确保通过 `relay_based_on_MX` 功能启用了 MX 中继：

```
FEATURE(relay_based_on_MX)dnl
```

所有邮件都将显示源自邮件服务器的主机。例如，如果你的 Sendmail 邮件服务器运行在 `turtle.mytrek.com` 上，从名为 `rabbit.mytrek.com` 的本地主机发送的邮件将显示为来自 `turtle.mytrek.com`。

你还可以伪装收件人地址，使发往本地主机用户的邮件改发到伪装后的地址。使用 `allmasquerade` 功能来启用收件人伪装：

```
FEATURE(allmasquerade)dnl
```

## 配置邮件服务器和邮件客户端

Sendmail 可用作邮件服务器，为网络上的各个主机处理邮件，也可作为邮件客户端，管理特定主机上本地用户的邮件。在简单的网络配置中，你会让每台主机以客户端配置运行 Sendmail，并有一台主机作为邮件服务器运行，负责网络主机的邮件中继。对于连接互联网的本地网络，你的本地主机将以客户端配置运行 Sendmail，而网关则以服务器配置运行 Sendmail（尽管邮件服务器不一定非要在网关上运行）。邮件服务器会将来自本地网络主机的消息中继到互联网。邮件服务器还可用于阻止来自外部主机的 unwanted 访问，例如发送垃圾邮件的主机。基本的客户端或服务器 Sendmail 配置仅涉及 `/etc/mail/sendmail.mc` 文件中的几个功能。系统上安装的默认 Red Hat 配置允许在单台主机上使用，管理该主机上用户之间的消息。要启用客户端和服务器使用，你需要对 `/etc/mail/sendmail.mc` 文件进行更改。

## 为简单网络配置 Sendmail

Red Hat 最初将 Sendmail 配置为仅在运行它的系统上工作，即 `localhost`。要使用 Sendmail 向本地网络上的其他主机发送消息，你需要在 `sendmail.mc` 和 `/etc/mail/access` 文件中更改并添加设置。简单的网络配置会在每台主机上运行 Sendmail，既处理该主机上用户之间发送的邮件，也处理与其它主机用户之间的邮件往来。对于每个 Sendmail 服务器配置，你需要进行以下关于简单本地网络配置部分中描述的更改。

对于在网络上主机之间发送的消息，你只需在每台主机上运行 Sendmail 服务器，对其 Sendmail 配置做少量更改。你可以将其中一台主机的 Sendmail 服务器配置为处理主机之间消息中继的任务。以前面描述的网络示例为例，主机 `turtle`、`rabbit` 和 `lizard` 将各自运行自己的 Sendmail 服务器。`turtle` 主机上的 Sendmail 服务器将被配置为在所有主机之间中继消息，包括其自身。

在网络上的每台主机上，编辑 `/etc/mail/sendmail.mc` 文件并进行以下更改。在 Red Hat 系统上，通过在前面放置 `dnl` 词来注释掉默认 `sendmail.mc` 文件中的 `DAEMON_OPTIONS` 行，如下所示。移除此功能将允许你通过本地网络接收消息。此条目将 Sendmail 限制在 `localhost`（`127.0.0.1`）：
