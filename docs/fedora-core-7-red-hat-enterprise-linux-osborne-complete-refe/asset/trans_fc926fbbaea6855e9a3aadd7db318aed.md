

## 配置 Sendmail 以支持简单网络环境

Fedora 初始将 Sendmail 配置为仅在其运行的系统上工作，即 **localhost**（本地主机）。若要使用 Sendmail 向本地网络上的其他主机发送消息，您需要修改并添加 `sendmail.mc` 和 `/etc/mail/access` 文件中的设置。在简单的网络配置中，Sendmail 将运行在每个主机上，处理该主机上用户之间以及与其他主机上用户之间的邮件收发。对于每个 Sendmail 服务器配置，您需要按照下文“简单本地网络配置”部分中描述的步骤进行修改。

对于网络上各主机之间发送的消息，您只需在每个主机上运行 Sendmail 服务器，并对其进行少量配置更改。您可以将其中一个主机上的 Sendmail 服务器配置为处理主机之间消息中继的任务。使用前面描述的网络示例，主机 **turtle**、**rabbit** 和 **lizard** 将各自运行其自身的 Sendmail 服务器。**turtle** 主机上的 Sendmail 服务器将被配置为中继所有主机（包括其自身）之间消息的服务器。

在网络上每个主机上，编辑 `/etc/mail/sendmail.mc` 文件并进行以下更改。在默认的 `sendmail.mc` 文件中，通过在 DAEMON_OPTIONS 行前添加 `dnl` 将其注释掉，如所示。移除此功能将允许您通过本地网络接收消息。此条目将 Sendmail 限制在 **localhost**（127.0.0.1）上：

```
dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=M')dnl
```

在您希望负责消息中继的那台主机的 `sendmail.mc` 文件中，您还需要添加以下行：

```
FEATURE(relay_entire_domain)dnl
```

运行 `m4` 操作以安装修改后的配置，然后如前所述使用 service 操作重启服务器。

现在，您可以通过网络从一个用户向另一个用户发送电子邮件。例如，**george@turtle.mytrek.com** 现在可以向 **larisa@rabbit.mytrek.com** 发送电子邮件。本地的 Sendmail 服务器将负责发送和投递邮件，无论是其主机内的用户还是位于其他网络主机上的用户。

## 配置 Sendmail 以支持集中式邮件服务器

或者，您可以设置一个集中式邮件服务器来处理网络上的所有邮件。各主机上的邮件客户端可以将消息发送到集中式邮件服务器，该服务器随后会将消息中继到更大的网络或互联网。邮件可以在集中式邮件服务器上接收，客户端之后可以从中检索邮件。设置集中式邮件服务器有几种方法。最简单的方法之一是在您的网关主机上运行集中式邮件服务器，然后在本地主机上运行 Sendmail 服务器的 null client（空客户端）版本。

从本地主机发送的任何邮件都会自动转发到集中式邮件服务器。接收的邮件只能投递到中央服务器，通常是投递到也运行在中央服务器主机上的 POP 或 IMAP 服务器。然后，用户可以访问 POP 服务器以检索其邮件。

对于集中式配置，将用户的网络域作为其地址（而不是网络中的单独主机）是有意义的。因此，rabbit.mytrek.com 上的用户 cce 将使用邮件地址 cce@mytrek.com，而不是 cce@rabbit.mytrek.com。用户可以与各自主机上的同名用户对应，但在网关主机上需要设置相应的用户以处理由 POP 或 IMAP 服务器管理的接收邮件。

一个有效且简单的邮件服务器将涉及以下几个组件：

- 运行在网关主机上的集中式邮件服务器
- 每个客户端将 Sendmail 作为 null client 运行
- 将所有邮件伪装（Masquerading）为仅使用域地址，而不使用主机地址
- 运行在网关主机上的 POP 或 IMAP 服务器以处理接收的邮件

## 配置具有直接 ISP 连接的工作站

如果您正在运行一个不属于网络但通过 ISP（互联网服务提供商）直接连接互联网的 Linux 系统，您可以简单地使用 ISP 的邮件服务器来发送和接收邮件。通常，您会有一个用于发送邮件的 SMTP 邮件服务器和一个用于接收邮件的 POP 服务器。但是，您也可以配置 Sendmail 以与您的 ISP 进行交互。

请务必首先按照前面章节中所示的方式注释掉 DAEMON_OPTIONS 选项。

通常，您的 ISP 将提供一个为其主机处理邮件的邮件服务器。为了利用 ISP 的邮件服务器，您可以使用 SMART_HOST 选项来定义它。邮件将通过 ISP 的邮件服务器发送。SMART_HOST 的格式为 type:hostname，其中 type 是使用的邮件服务器类型，通常是 SMTP。默认值是 relay。定义 SMART_HOST 选项以使用您的 ISP 发送和接收邮件：

```
define(`SMART_HOST', `smtp:mail.my-isp.com') dnl
```

SMART_HOST 选项用于指示您希望处理网络消息中继的特定远程邮件服务器。它可以是 ISP 的邮件服务器，也可以是更大网络中的任何邮件服务器。

对于通过调制解调器的拨号连接，您可以使用各种配置选项来控制连接。confMESSAGE_TIMEOUT 选项允许您控制邮件在输出队列中保留多长时间，从而让您可以在准备好拨号并发送时保留邮件。将 confDELIVERY_MODE 选项设置为 queueonly 可让您仅在准备好时才发送邮件。

## 邮件器表（Mailer Table）

邮件器表允许您将地址为指定主机或域的消息路由到特定的邮件服务器。您可以使用邮件器表将地址为虚拟域的邮件路由到您网络的邮件服务器。若要引用整个域，请在域名前加一个句点。邮件路由到的主机前缀由使用的邮件器标识，对于 Sendmail 通常是 **smtp**。以下条目将地址为 **.mybeach.com** 的邮件路由到邮件服务器 **turtle.mytrek.com**：

```
.mybeach.com    smtp:turtle.mytrek.com
```

条目放置在 */etc/mail/mailertable* 文件中。完成条目后，使用 **make** 命令生成 *mailertable.db* 数据库文件：

```
make mailertable
```

## 虚拟域：virthsersutable

如您将在第 36 章中看到的，您可以为网络定义虚拟域。这些虚拟域由您的 DNS 服务器映射到一个或多个实际域。但是，您可以接收具有虚拟域用户邮件地址的消息。在这种情况下，您需要将这些地址映射到实际域上的用户，以便将邮件投递到现有位置。此映射由称为 */etc/mail/virthsersutable* 的虚拟用户表完成。虚拟用户表允许您将虚拟域的邮件地址映射到实际域上的用户。完成条目后，使用 **make** 命令生成 *virthsersutable.db* 数据库文件：

```
make virthsersutable
```

## 安全性

出于安全考虑，Sendmail 允许您筛选特定消息，并为 Sendmail 传输提供身份验证和加密。在 8.11 版本中，Sendmail 集成了对安全套接字层（SSL）和简单身份验证和安全层（SASL）的支持。SSL 支持通过 Sendmail 命令 **STARTTLS** 实现，即“启动传输层安全”。SSL 为 Sendmail 操作提供身份验证、加密和完整性检查（参见第 19 章）。必须先安装 OpenSSL 才能使用 SSL 加密和身份验证方法。

SASL 通过 **AUTH** 命令实现，称为 SMTP AUTH。SASL 为邮件用户和服务器提供身份验证。它可以利用已安装的 Kerberos 服务来提供身份验证。

Sendmail 还提供了筛选来自特定域、主机、IP 和用户地址的消息的能力。执行此类筛选的规则保存在 */etc/mail/access* 文件中。您可以编辑此文件并添加自己的规则。规则由地址和要采取的操作组成。（支持的操作列在表 25.4 中。）例如，要删除来自 **myannoyingad.com** 域的所有消息，您将输入：

```
myannoyingad.com  DISCARD
```

下一个示例拒绝来自 **larisa@turtle.mycar.com** 的任何消息，并发送拒绝通知：

```
larisa@turtle.mycar.com  REJECT
```

