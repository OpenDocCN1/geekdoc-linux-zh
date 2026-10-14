
此页面提供对邮件队列的访问。根据您的配置，您的队列可能转瞬即逝，也可能在定期或手动刷新之前一直填满。通常，如果您拥有全天候的网络访问和全天候的 DNS 服务器，您将使用后台模式发送邮件。在这种情况下，邮件在队列中只会停留几秒钟或几分钟，然后就会发送到接收服务器。但是，在发生临时投递失败（非永久性错误）的情况下，消息将保留在队列中，直到消息被丢弃（由于永久性错误）或成功发送为止。队列中的任何消息都可以通过点击消息 ID 来查看。此外，还可以从队列中删除消息。最后，可以手动刷新队列，Sendmail 将立即尝试投递队列中的所有邮件。

## User Mailboxes

Webmin Sendmail 模块的一个强大功能是能够通过 Web 界面读取邮件。虽然它不是一个功能齐全的邮件客户端（即使在基于 Web 的客户端中也是如此），但它是一种快速简便的方式来检查那些通常不会被用户检查的账户的消息。例如，在我的系统上，我每天都会从备份系统收到备份报告，因此我会定期通过 Webmin 界面检查它们以查找问题。

要检查 root 的邮件，只需点击名称即可。从那里您将看到该用户所有电子邮件的列表。点击邮件即可显示其内容。从用户邮件页面，您还可以删除邮件并撰写新邮件（图 11-2）。

## Editing the m4 Configuration File

您系统上的 Sendmail 可能已在默认的`sendmail.cf`中包含了相当不错的功能集。但正如所讨论的那样，一些功能通常被省略，例如`genericstable`。通常，这些功能不需要，但如果需要，您必须将它们添加到配置文件中。手动编辑`sendmail.cf`通常被认为不是像您和我这样的凡人可以考虑的选择（Sendmail 的创建者 Eric Allman 可能可以做到）。然而，最近版本的 Sendmail 提供了一种新颖的方法来向`sendmail.cf`添加功能，该方法使用名为`sendmail.mc`的宏文件和`m4`宏处理器。

![](img/d84604054810a13cacfdac212ebee2f7_231_0.png)

图 11-2：用户邮件

## Adding a Feature

与直接编辑`.cf`不同，使用`m4`宏文件添加功能实际上非常容易。

打开 M4 配置页面后，您会看到一个类似图 11-3 所示页面的文件。

除`dnl`注释行和`divert(-1)`行外，每一行都是`macro-type(value list)`的形式。在此示例中，您将添加一个名为`genericstable`的新功能。因此，您将在`FEATURE`列表中插入如下一行：

```
FEATURE(`genericstable', `hash -o /etc/mail/genericstable')
```

![](img/d84604054810a13cacfdac212ebee2f7_231_1.png)

图 11-3：M4 配置文件

要执行此操作，请从页面底部的下拉列表中选择 Feature，然后点击 Add new entry of type 按钮。接着，选择`genericstable`（Outgoing Addresses）。接下来在参数字段中指定表文件的类型和位置，`hash -o /etc/mail/genericstable`。单引号不是必需的，因为 Webmin 会为您插入它们。为了以后的方便，最好使用页面右侧的箭头按钮将新条目提升到文件中的其他`FEATURE`行下方。它不是严格必要的，但拥有整洁的配置文件是件好事，即使 Webmin 大多数时候都隐藏了它们。

保存更改后的文件后，您将生成新的`sendmail.cf`（如果您已设置 Sendmail，请不要忘记将旧文件备份到另一个文件）。要基于`.mc`文件创建新的`sendmail.cf`，请点击 Rebuild Sendmail Configuration 按钮。然后您将能够打开 Outgoing Domains 页面，并创建新的`genericstable`文件并正常编辑它。应用您所做的更改需要重新启动 Sendmail。

## Tutorial: Setting Up Sendmail

首次安装后，Sendmail 只需进行少量更改即可开始提供发送和接收邮件的服务。第一步是指定将接受邮件的对象，您将在 Local Domains 页面中指定，而第二步将是允许本地网络用户通过服务器发送或中继电子邮件，这将在 Spam Control 页面中指定。

NOTE 本教程假定您已为网络配置了 DNS 服务，包括域的 MX 记录。如果您尚未这样做，请参考 BIND 章节，并在尝试本教程中的步骤之前配置名称解析。

## Configuring Domains to Receive Mail For

默认情况下，Sendmail 未配置为接收除其运行的机器之外的任何主机或网络的邮件。因此，您必须首先配置 Sendmail 以允许任何人通过您的服务器发送邮件以交付到您的域。打开 Local Domains 页面，并输入您的服务器将接受邮件的域。在我的例子中，我会输入 swelltech.com。此处可以输入任意数量的域，也可以输入主机名，因此如果我期望邮件被交付到该地址，我也可以输入 www.swelltech.com。

点击 Save 按钮以更新`sendmail.cf`文件。这将添加新的`Cw`行以包含您指定的域。

## Permitting Local Users to Relay

实现一个简单的邮件服务器的下一步是允许您的本地用户通过您的服务器发送邮件。点击 Spam Control 图标，并创建一条或多条匹配您本地网络的规则。要创建新规则，首先选择 Mail source 为 Network，并指定您希望为其提供中继服务的网络 IP。例如，在使用私有 IP 地址的本地网络上，人们可能会输入 192.168.1 以指定 192.168.1.0/24 网络中的所有主机。然后，选择 Allow relaying，并点击 Create 以将新规则添加到`access`文件中。

最后，返回到主要的 Sendmail 页面，并点击 Start Sendmail 按钮。启动守护进程时通常很有用保持关注日志，以便问题能够立即显而易见。Sendmail 在大多数系统上记录到邮件日志中，该日志很可能位于`/var/log`目录中。您可以使用 Webmin System Logs 模块查看此日志。

## Tutorial: Virtual Hosting Email with Sendmail

虚拟主机是一个相当宽泛的术语，应用于许多网络服务，以指定相关服务器为两个或多个网络域提供服务并具有一定程度的分离。具体而言，在邮件服务器的情况下，这意味着邮件服务器将根据收到的电子邮件的收件人字段中的用户名和域名，将邮件投递到唯一的本地用户。例如，发送到 joe@swelltech.com 的电子邮件将与发送到 joe@notswelltech.com 的电子邮件不同对待，并投递到不同的邮箱。

与大多数开源软件一样，实现我们的目标有许多方法，但在这里您将学习 Sendmail 提供的最简单方法。配置 Sendmail 进行虚拟邮件托管是一个三步过程。首先，必须为每个被服务的域适当配置 DNS，包括 MX 记录，如本书 BIND 章节所述。其次，新域被添加到 Local Domains 表中。最后，一个或多个条目被添加到 Address Mapping 表中。由于 DNS 有自己的章节，并且在前面的教程中已经介绍了将条目添加到 Local Domains 表，您在这里只会学习最后一步。

### Adding Address Mapping Entries

点击 Address Mapping 图标，并根据您的环境创建新的映射。要创建新条目，请选择 Address 并在 Mail for 字段中填写邮件将被接收的地址。这将包括收件人的名称和域名，例如，我可能会在此字段中输入 joe@virtualhost.com。接下来，选择 Address 选项并在 Send to 字段中输入此用户的目标邮箱，该邮箱需要是一个已存在的用户。例如，我可能会在此处输入用户名 virtualhost-joe。用户名也必须在系统上创建，可以使用第 5 章中的 "Users and Groups" 部分完成。

点击 Create 按钮，并通过向您新创建的虚拟用户发送邮件来测试您的工作。

## 12 SQUID

![](img/d84604054810a13cacfdac212ebee2f7_234_0.png)

Squid 是一个功能丰富且极其灵活的 Web 缓存代理守护进程。大多数配置都是通过编辑一个名为`squid.conf`的简单配置文件来完成的，该文件通常位于`/usr/local/squid/etc/squid.conf`或在源自 Red Hat Linux 的系统上位于`/etc/squid/squid.conf`。每个行为都由一个指令后跟一个或多个选项来设置。Webmin 接口提供了访问可用于配置 Squid 的大多数指令。因为 Squid 是一个相当复杂的软件包，Webmin 接口打开时显示一系列图标来表示不同类型的配置选项。图 12-1 显示了 Squid 主页面。
