
## 设置本地投递目标：/etc/mail/sendmail.cw

使用此文件指定 sendmail 服务器将接收电子邮件的主机和域名。该文件的一个示例如下：

niotec.com
ad-engine.com
classedrew.com

每一行指定一个由 sendmail 服务器处理服务的域名。

## 使用 /etc/mail/virtusertable 创建虚拟邮件服务器

要为多个域提供邮件支持，请使用 sendmail 设置虚拟邮件服务。例如，要为名为 yourclient.com 的域提供虚拟邮件服务，请执行以下操作：

- 1. 将域名（yourclient.com）添加到 /etc/mail/sendmail.cw 文件中，以便 sendmail 接受针对该主机的邮件。
- 2. 将域名（yourclient.com）添加到 /etc/mail/relay-domains 文件中，以便 sendmail 中继该域名的消息。

要将虚拟域用户映射到一个或多个本地账户，请如下使用 /etc/mail/virtusertable 文件：

```
virtual e-mail address    real e-mail address
```

以下是一些示例：

```
webmaster@yourclient.com    mike
mike@yourclient.com        mike
info@yourclient.com        jason
jason@yourclient.com       jason
```

在这些示例中，发往 webmaster@yourclient.com 和 mike@yourclient.com 等虚拟电子邮件地址的邮件将发送给本地用户 mike；类似地，发往 info@yourclient.com 和 jason@yourclient.com 的邮件将发送给另一个本地用户 jason。这为 yourclient.com 提供了一个它原本没有的邮件服务器。对于世界其他地方而言，yourclient.com 似乎拥有一个邮件服务器。如果你还为此域名提供 **yourclient.com** 域的 DNS 服务，你可以通过执行以下操作使整个过程看起来非常专业：

- 在 **yourclient.com** 域的 DNS 服务中添加一条 A 记录，指向你的 sendmail 服务器。例如，如果你的 sendmail 服务器主机的 IP 地址是 192.168.1.10，请在 **yourclient.com** 域的 DNS 配置文件中添加以下行：

```
mail.yourclient.com. IN A 192.168.1.10
```

- 在 **yourclient.com** 域的 SOA 记录中添加一条 MX 记录，指向 mail.yourclient.com。例如：

```
IN MX 5 mail.yourclient.com.
```

只要你的 sendmail 已根据前面讨论的虚拟配置设置好，这就会让世界上其他（毫不知情的）人认为 **yourclient.com** 拥有一个真实的邮件服务器。

支付 ISP 进行网站托管（**www.client-domain.com**）的个人或公司通常也要求提供虚拟邮件服务。在这种情况下，创建单一的 /etc/mail/virtusertable 文件通常难以管理。例如，如果你托管数百个域，每次你（或你的助理管理员）修改 /etc/mail/virtusertable 文件时，它都会成为大量人为错误的根源。在这种情况下，你可以创建一个更易于管理的解决方案。例如，要为两个名为 client-a.com 和 client-b.com 的客户端创建两个虚拟邮件服务，请执行以下操作：

- 为每个域创建单独的虚拟电子邮件映射文件。使用诸如 *domain.ftr* 的命名约定（*ftr* 是 fake-to-real 的缩写）。

- 创建一个 /etc/mail/client-a.ftr 文件，其中包含通常放入该域 /etc/mail/virtusertable 的内容。例如，该文件可能如下所示：

```
user1@client-1.com client1
webmaster@client-1.com unix@home-town-isp.com

@client-1.com client1
```

在此示例文件中，user1@client-1.com 地址映射到本地账户 client1；webmaster@client-1.com 映射到远程 ISP 账户；该域的所有其他可能的电子邮件地址都映射到本地账户。最后一条条目非常有用，并且经常被虚拟域所有者请求。它允许 **client-1.com** 域的所有者在网站或其他商业出版物和广告中使用任何他们想要的电子邮件地址，并且仍能在正确的地方接收邮件。例如，如果 **www.client-1.com** 发布了一个名为 **info@client-1.com** 的电子邮件地址，任何向该账户发送邮件的人都会得到 client1 用户的妥善服务。

- 3. 为第二个客户端创建 */etc/mail/client-b.ftr* 文件。该文件可能类似于上一个示例；但是，假设 **client-b.com** 的所有者希望所有电子邮件地址都自动映射到她在当地 ISP 邮件服务器中现有的账户。在这种情况下，该映射文件如下所示：

```
@client-b.com $1@home-town-isp.com
```

- 4. 现在既然有了两个虚拟用户映射文件，使用以下命令创建最终的 */etc/mail/virtusertable* 文件：

```
touch /etc/mail/virtusertable
cat *.ftr >> /etc/mail/virtusertable
```

第一条命令创建 */etc/mail/virtusertable* 文件（如果尚不存在）。第二条命令将所有 FTR 文件连接到 */etc/mail/virtusertable*。这有效地创建了最终的 */etc/mail/virtusertable* 文件。

- 5. 运行 **makemap** 程序创建该文件的数据库版本，如下所示：

```
makemap hash /etc/mail/virtusertable < /etc/mail/virtusertable
```

正如本例所示，创建多个虚拟用户映射文件可以帮助你轻松跟踪各个域。任何时候你想更改特定域的映射，只需修改该域的 FTR 文件，并使用刚才讨论的技术创建最终的 */etc/mail/virtusertable* 文件。

由于大多数邮件客户端程序允许单个用户将出站 **From:** 行设置为任何他们希望的内容，你可能不需要对虚拟站点的出站流量进行任何映射。然而，如果你希望确保虚拟邮件站点用户的出站邮件转换为其虚拟域名，请使用 /etc/mail/genericstable 文件。

例如，假设你有一个名为 classifiedworks.com 的虚拟邮件站点，你有一个 FTR 文件，如 /etc/mail/classifiedworks.ftr，其中包含以下行：

```
sales@classifiedworks.com sheila
```

sales@classifiedworks.com 地址映射到名为 sheila 的本地用户。当 Sheila 使用 sendmail 服务器发送邮件时，你希望她的邮件显示为 sheila@classifiedworks.com，而不是 sheila@yourdomain.com。在这种情况下，创建一个 /etc/mail/genericstable 文件，并包含以下行：

```
sheila sales@classifiedworks.com
```

这反转了 virtusertable 文件的内容。本着保持特定域信息分离的精神，你可能希望为每个域创建单独的逆映射文件。假设该文件将使用 .rtf 扩展名（real-to-fake）。在为每个使用虚拟邮件服务的域创建此类文件后，按如下方式创建合并的 /etc/mail/genericstable 文件：

```
touch /etc/mail/genericstable
cat *.rtf >> /etc/mail/genericstable
```

运行 makemap 程序创建该文件的数据库版本：

```
makemap hash /etc/mail/genericstable < /etc/mail/genericstable
```

总之，对于每个虚拟邮件域，创建一个 FTR 文件将虚假电子邮件地址映射为真实地址，并创建另一个文件将真实地址映射为虚假电子邮件地址。创建这些文件后，将它们合并以创建 /etc/mail/virtusertable 文件（针对 *.ftr）和 /etc/mail/genericstable 文件（针对 *.rtf）。然后，运行 makemap 创建这些文件的数据库版本。只要你在 /etc/mail/sendmail.cw 和 /etc/mail/relay-domains 文件中列出了每个虚拟域，流程就完成了。

sendmail 配置很复杂，因此通常有必要尝试各种配置更改以实现你想要的效果。作为一般规则，请始终执行以下操作：

- 在进行任何更改之前备份你的配置。
- 每次更改 sendmail 配置时，在深入推进之前先进行测试。

本节介绍了一些测试典型配置问题的示例。

## 测试 sendmail 配置

### 测试 sendmail 地址重写规则

要测试 sendmail 规则的行为，请如下运行 **sendmail**：

```
sendmail -bt
```

这将使 sendmail 以地址模式运行，并给你一个提示符与之交互。在提示符下，输入测试命令，例如：

```
<ruleset> <address>
```

例如，要查看 sendmail 的重写规则 0 如何处理 **kabir@nitec.com**，请运行以下命令：

```
0 kabir@nitec.com
```

在我的 sendmail 系统上，输出显示如下：

```
ADDRESS TEST MODE (rule set 3 NOT automatically invoked)

Enter <ruleset> <address>

> 0 kabir@nitec.com

rewrite: rule set 0 input: kabir@nitec.com

rewrite: rule set 199 input: kabir@nitec.com

rewrite: rule set 199 returns: kabir@nitec.com

rewrite: rule set 90 input: kabir@nitec.com

rewrite: rule set 90 returns: kabir@nitec.com

rewrite: rule set 198 input: kabir@nitec.com
```
