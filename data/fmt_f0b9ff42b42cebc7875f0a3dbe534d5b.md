
确保 Exchange 正常运行的最有效方法是在 Windows XP 系统上安装 Outlook 2003。Outlook 是 Office 2003 的一部分。如果你没有授权版本，可以从 `www.microsoft.com/office/trial/default` 下载 Office 2003 标准版（包含 Outlook）的试用版

![](img/1bd448c8019d74f469e5d7e3f033d752_339_0.png)

在 Windows XP 系统上安装 Outlook 2003 是确保 Exchange 正常运行的最有效方法。`img/1bd448c8019d74f469e5d7e3f033d752_339_0.png`

在 `windc1.ad.corp.com` 上加载 Exchange，下载 Office 2003 标准版（包含 Outlook）的试用版。

确保 Exchange 正常运行的最有效方法。

![](img/1bd448c8019d74f469e5d7e3f033d752_339_0.png)

在 `windc1.ad.corp.com` 上加载 Exchange，下载 Office 2003 标准版（包含 Outlook）的试用版。

确保 Exchange 正常运行的最有效方法。

![](img/1bd448c8019d74f469e5d7e3f033d752_339_0.png)

在 `windc1.ad.corp.com` 上加载 Exchange，下载 Office 2003 标准版（包含 Outlook）的试用版。

确保 Exchange 正常运行的最有效方法。

![](img/1bd448c8019d74f469e5d7e3f033d752_339_0.png)

在 `windc1.ad.corp.com` 上加载 Exchange，下载 Office 2003 标准版（包含 Outlook）的试用版。

确保 Exchange 正常运行的最有效方法。

![](img/1bd448c8019d74f469e5d7e3f033d752_339_0.png)

## 第 6 章. 实用的 Windows Exchange 与 Linux Postfix 邮件集成

是的。但我们需要一种方法，将来自外部的入邮件路由到实际上具有特定 `@corp.com` 用户正确邮箱箱的后端服务器。我们还需要能够将来自 Exchange 用户的邮件路由到 Linux 用户，反之亦然。

我们将使用四个主要组件来实现这一目标：

- Postfix 邮件服务器：我们已经介绍过这个软件了。在这种情况下，我们将使用 Postfix 作为早期路由器和清理器，而不是直接将消息投递到邮箱服务器。
- SpamAssassin 垃圾邮件过滤器：根据 `http://spamassin.apache.org` 上的 SpamAssassin 主页，SpamAssassin 是一种“通过对邮件头和正文内容使用广泛的启发式方法来识别垃圾邮件”的邮件过滤器。
- ClamAV 病毒过滤器：ClamAV 是一个由开源社区支持的检测和删除工具。你可以从 `www.clamav.net` 的 ClamAV 主页了解更多关于 ClamAV 的信息。
- MailScanner 桥接了 Postfix、SpamAssassin 和 ClamAV 之间的差异。SpamAssassin 和 ClamAV 包含了它们与 Postfix 集成的简单方法，但你将不会使用这些方法。MailScanner 提供了将任意数量的扫描程序与 Postfix 集成的能力。为了保险起见，它本身也有一些垃圾邮件和病毒检测功能。更多信息，请访问 `www.mailscanner.info` 的 MailScanner 主页。

以上所有内容都是免费的开源软件包。

然而，我们仍然有一个障碍需要跨越。我们需要一种方法让 `mail.corp.com` “知道”哪些用户在 Exchange 上有邮箱箱，哪些用户在 Linux 服务器上有邮箱箱。我们需要一种方法让 `mail.corp.com` 恰当地路由到我们的后端服务器。为此，自定义编写一个 Perl 脚本来确定任何接收者的正确后端服务器。该脚本可用于路由路由到 Exchange 和 Postfix 后端的任何组合，而不仅仅是本章所示特定配置。

![](img/1bd448c8019d74f469e5d7e3f033d752_343_0.png)

如果你在 `l1nserv1.corp.com` 上使用基于 LDAP 的账户，该脚本将运行得很好。否则，`mail.corp.com` 没有办法发现哪些地址属于 Linux 后端 MTA。LDAP 是服务器之间共享信息的关键。如果你在第 2 章中没有设置基于 LDAP 的身份验证，现在是回去设置的时候了。具体来说，查看第 2 章中“在 Linux 上设置 OpenLDAP 服务器”的部分。

这里有一个很大的警告：你必须完成本节中的所有步骤，直到本章结束。这些指南是作为一个整体为你提供的，不应该分批执行。在这些步骤期间，在在你完成之前，邮件将停止正常路由，因为我们正告诉 Postfix 部门人员和 Exchange 服务器将邮件路由到 `mail.corp.com`——在它甚至存在之前。

## 统一 Linux 与 Exchange 投递（带反垃圾邮件和反病毒）323

### Exchange 重新配置任务

为了实现上述目标，我们需要与出厂设置略有不同地重新配置 Exchange。以下是我们要做的操作：

- 让 Exchange 服务器像 `ad.corp` 一样发送和接收邮件：目前，Exchange 上的所有用户都有类似 `salesperson1@corp.com` 的电子邮件地址。我们需要训练 Exchange 允许用户拥有仅显示 `@corp.com` 的电子邮件地址。
- 强制 Exchange 将所有邮件发送到我们的 `mail.corp` 服务器：我们可以允许 Exchange 直接向互联网发送出站邮件。但通过将这些消息转发到 `mail.corp` 前端 MTA，我们获得了扫描出站邮件的优势。如果本地网络内发生邮件病毒，很高兴它不会传播到其他公司和客户。扫描出站邮件是有好处的！
- 让 Exchange 将 `corp.com` 中无法识别的地址发送到 `mail.corp` 服务器：当一个 Exchange 用户（例如 `salesperson1`）发送邮件时，目标可能是 Linux Postfix 邮件服务器（例如 `n1`）。`mail.corp` 服务器将配置为自动区分 Exchange 用户和 Linux 用户。如果没有此更改，Exchange 将假设自己是 `corp.com` 的唯一仲裁，并丢弃非 Exchange 用户的消息。

### 让 Exchange 伪装 Corp.com

目前，Exchange 认为它正在作为 `ad.corp` 发送和接收邮件，但当 `salesperson1` 处理邮件时，它说是 `salesperson1@corp.com`。因此，我们需要教 Exchange 像它负责 `corp.com` 那样发送和接收邮件。要配置此项，你将使用的工具是 Exchange 系统管理器。让 Exchange 以 `corp.com` 发送和接收邮件：

1. 选择 Start ► Programs ► Microsoft Exchange 并选择 System Manager。
2. 钻取 Corp (Exchange) ► Recipients ► Policies 并在右侧找到 Default Policy。
3. 右键点击 Default Policy 并选择“Properties”。
4. 点击“E-mail Addresses (Policy)”选项卡并点击“New”。
5. 在“New E-mail Addresses”对话框中选择“SMTP Address”并点击“OK”。
6. 在“SMTP Address Properties”对话框中，在“Address”字段输入 `@corp.com`，选择“This Exchange is responsible for all mail delivery to”，并点击“OK”。
7. 回到“E-Mail Addresses (Policy)”选项卡，点击你刚刚创建的 `@corp.com` 并设置“Set as Primary”。`@corp.com` 将加粗，如图 6.9 所示。点击“OK”继续。
8. 将被询问是否更新当前批用户的电子邮件地址。你应该选择“Yes”，因为你已经为 `salesperson1` 和 `salesperson2` 分配了电子邮件地址。注意这并不总是立即生效。请耐心。几分钟后，新地址将出现在 Active Directory 中。

### 让 Exchange 服务器使用智能主机

在我们的世界中，我们希望确保 Exchange 发送和接收的所有邮件都通过 `mail.corp` 前端 MTA。为了实现这一点，我们将告诉 Exchange 仅通过智能主机发送。

配置 Exchange 通过智能主机发送：

1. 选择 Start ► Programs ► Microsoft Exchange 并选择 System Manager。
