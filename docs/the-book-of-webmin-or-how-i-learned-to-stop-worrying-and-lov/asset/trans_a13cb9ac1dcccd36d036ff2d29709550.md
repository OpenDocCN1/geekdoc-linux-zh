

## Mail from

在此输入要重映射的用户的用户名或完整电子邮件地址。

## Change to

在此输入要将上述地址更改为的目标地址。

## Manually edit /etc/mail/genericstable

点击此项会提供一个简单的文本输入框，其中列出了所有 genericstable 映射。您可以在此处手动编辑它们。但请注意，手动编辑的条目不会由 Webmin 检查其语法正确性。

## Outgoing Domains

默认情况下，Sendmail 仅对本地用户（与 Sendmail 服务器相同域中的用户）的发件地址进行翻译。任何需要重映射的外部域都必须在此输入。

## Domain Mapping

此功能允许您将某个域的所有收件人和发件人地址重映射到另一个域。例如，如果您的公司更改名称，您希望将所有邮件从 mailuser@oldname.com 更改为 mailuser@newname.com 时，此功能很有用。此更改将影响所有交付到、经由或从您的服务器发出的邮件。使用此功能应仅限于您的域。

## Spam Control

在此页面，您可以配置任意数量的规则，以防止垃圾邮件发送者利用您的系统和网络资源进行其邪恶目的。虽然这只是最新版本 Sendmail 提供的垃圾邮件控制功能中的冰山一角，但它确实为您提供了防止网络垃圾邮件的非常好的手段。首要且主要的目标是防止网络外部的任何人将您的服务器用作垃圾邮件中继。幸运的是，在最近版本的 Sendmail 中，默认情况下会拒绝从本地网络以外的任何主机进行中继。这让您的工作变得轻松一些，因为您只需允许来自受信任的主机和域的邮件中继即可。在这里，您还可以添加规则，明确禁止来自某些已知垃圾邮件发送者的邮件。例如，如果您的用户开始收到来自 bigdumbspammers.com（截至本文撰写时并非真实域名）的成批未经请求的商业电子邮件（UCE，亲切地称为垃圾邮件），并且该域的管理员要么不在乎，要么积极参与垃圾邮件发送，您就可以简单地阻止他们向我们的任何客户发送邮件。您只需输入域名并选择 Reject 或通过使用 Error code 提供错误消息即可。

有关 Sendmail 中垃圾邮件控制主题的更多信息，允许在 Sendmail 中受控 SMTP 中继 [http://www.sendmail.org/tips/relaying.html] 页面提供了有关防止垃圾邮件的多个新 Sendmail 功能的更多文档，例如使用实时黑洞列表 [http://mail-abuse.org/rbl/]，它提供了一个已知垃圾邮件发送者和开放中继的黑名单。此外，访问邮件滥用预防系统 [http://mail-abuse.org/] 以了解更多打击垃圾邮件的方法也可能是值得的。

## Relay Domains

您希望允许中继到的任何本地域都应在此列出。任何既不是本地用户也不是这些列出域的传入邮件都将被 Sendmail 拒绝。如果您的 Sendmail 以虚拟主机的方式为多个域提供邮件服务，这些域也应在此列出。

## Mail Queue

此页面提供对邮件队列的访问。根据您的配置，您的队列可能转瞬即逝，也可能在定期或手动刷新之前一直填满。通常，如果您拥有全天候的网络访问和全天候的 DNS 服务器，您将使用后台模式发送邮件。在这种情况下，邮件在队列中只会停留几秒钟或几分钟，然后就会发送到接收服务器。但是，在发生临时投递失败（非永久性错误）的情况下，消息将保留在队列中，直到消息被丢弃（由于永久性错误）或成功发送为止。队列中的任何消息都可以通过点击消息 ID 来查看。此外，还可以从队列中删除消息。最后，可以手动刷新队列，Sendmail 将立即尝试投递队列中的所有邮件。

## User Mailboxes

Webmin Sendmail 模块的一个强大功能是能够通过 Web 界面读取邮件。虽然它不是一个功能齐全的邮件客户端（即使在基于 Web 的客户端中也是如此），但它是一种快速简便的方式来检查那些通常不会被用户检查的账户的消息。例如，在我的系统上，我每天都会从备份系统收到备份报告，因此我会定期通过 Webmin 界面检查它们以查找问题。

要检查 root 的邮件，只需点击名称即可。从那里您将看到该用户所有电子邮件的列表。点击邮件即可显示其内容。从用户邮件页面，您还可以删除邮件并撰写新邮件（图 11-2）。

## Editing the m4 Configuration File

您系统上的 Sendmail 可能已在默认的 sendmail.cf 中包含了相当不错的功能集。但正如所讨论的那样，一些功能通常被省略，例如 genericstable。通常，这些功能不需要，但如果需要，您必须将它们添加到配置文件中。手动编辑 sendmail.cf 通常被认为不是像您和我这样的凡人可以考虑的选择（Sendmail 的创建者 Eric Allman 可能可以做到）。然而，最近版本的 Sendmail 提供了一种新颖的方法来向 sendmail.cf 添加功能，该方法使用名为 sendmail.mc 的宏文件和 m4 宏处理器。

![](img/d84604054810a13cacfdac212ebee2f7_231_0.png)

图 11-2：用户邮件

## Adding a Feature

与直接编辑 .cf 不同，使用 m4 宏文件添加功能实际上非常容易。

打开 M4 配置页面后，您会看到一个类似图 11-3 所示页面的文件。

除 dnl 注释行和 divert(-1) 行外，每一行都是 macro-type(value list) 的形式。在此示例中，您将添加一个名为 genericstable 的新功能。因此，您将在 FEATURE 列表中插入如下一行：

```
FEATURE(`genericstable', `hash -o /etc/mail/genericstable')
```

![](img/d84604054810a13cacfdac212ebee2f7_231_1.png)

图 11-3：M4 配置文件

要执行此操作，请从页面底部的下拉列表中选择 Feature，然后点击 Add new entry of type 按钮。接着，选择 genericstable（Outgoing Addresses）。接下来在参数字段中指定表文件的类型和位置，hash -o /etc/mail/genericstable。单引号不是必需的，因为 Webmin 会为您插入它们。为了以后的方便，最好使用页面右侧的箭头按钮将新条目提升到文件中的其他 FEATURE 行下方。它不是严格必要的，但拥有整洁的配置文件是件好事，即使 Webmin 大多数时候都隐藏了它们。

保存更改后的文件后，您将生成新的 sendmail.cf（如果您已设置 Sendmail，请不要忘记将旧文件备份到另一个文件）。要基于 .mc 文件创建新的 sendmail.cf，请点击 Rebuild Sendmail Configuration 按钮。然后您将能够打开 Outgoing Domains 页面，并创建新的 genericstable 文件并正常编辑它。应用您所做的更改需要重新启动 Sendmail。

## Tutorial: Setting Up Sendmail

首次安装后，Sendmail 只需进行少量更改即可开始提供发送和接收邮件的服务。第一步是指定将接受邮件的对象，您将在 Local Domains 页面中指定，而第二步将是允许本地网络用户通过服务器发送或中继电子邮件，这将在 Spam Control 页面中指定。

NOTE 本教程假定您已为网络配置了 DNS 服务，包括域的 MX 记录。如果您尚未这样做，请参考 BIND 章节，并在尝试本教程中的步骤之前配置名称解析。

## Configuring Domains to Receive Mail For

默认情况下，Sendmail 未配置为接收除其运行的机器之外的任何主机或网络的邮件。因此，您必须首先配置 Sendmail 以允许任何人通过您的服务器发送邮件以交付到您的域。打开 Local Domains 页面，并输入您的服务器将接受邮件的域。在我的例子中，我会输入 swelltech.com。此处可以输入任意数量的域，也可以输入主机名，因此如果我期望邮件被交付到该地址，我也可以输入 www.swelltech.com。

点击 Save 按钮以更新 sendmail.cf 文件。这将添加新的 Cw 行以包含您指定的域。

## Permitting Local Users to Relay

实现一个简单的邮件服务器的下一步是允许您的本地用户通过您的服务器发送邮件。点击 Spam Control 图标，并创建一条或多条匹配您本地网络的规则。要创建新规则，首先选择 Mail source 为 Network，并指定您希望为其提供中继服务的网络 IP。例如，在使用私有 IP 地址的本地网络上，人们可能会输入 192.168.1 以指定 192.168.1.0/24 网络中的所有主机。然后，选择 Allow relaying，并点击 Create 以将新规则添加到 access 文件中。

