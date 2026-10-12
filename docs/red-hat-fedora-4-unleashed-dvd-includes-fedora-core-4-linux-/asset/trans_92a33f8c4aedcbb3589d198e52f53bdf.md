
- 使用 Procmail 根据发件人、主题或许多其他变量自动对收到的邮件进行分类。
- 使用 Spamassassin 在你阅读之前消除不需要的消息。

## 基本的 Sendmail 配置和操作

由于 Sendmail 是 Fedora 的默认客户端（也是使用最广泛的客户端），以下章节将简要说明如何配置和操作你的邮件系统并提供示例。然而，如前所述，Sendmail 是一个极其复杂的程序，其配置非常繁琐。因此，本章仅涵盖一些基础知识。如需了解有关 Sendmail 以及其他 MTA（邮件传输代理）的更多信息，请参阅本章末尾的“参考”部分。

Sendmail 的配置由 /etc/mail 目录中的文件处理，其中大部分配置由 sendmail.cf 文件处理。配置文件 sendmail.cf 的实际语法晦涩难懂（见以下示例）。为了简化 Sendmail 的配置，创建了 sendmail.mc 文件。然而，以下示例表明这一目标并未完全实现。sendmail.mc 文件必须通过 m4 宏处理器进行处理以创建 sendmail.cf 文件；该处理器的需求导致了该文件不寻常的语法。你稍后会学习如何使用它，我们将查看一个自动简化整个过程的 Perl 脚本。首先，让我们检查一下你可能想对 Sendmail 进行的一些基本配置。

> 注意
> sendmail.cf 具有奇怪的语法，这是由 m4 宏处理器的要求造成的。你不需要在这里了解 m4 的细节，但请注意引用系统。起始引号是反引号 (`)，而结束引号只是一个单引号 (')。此外，`dn1` 序列意味着“删除直到换行”，并导致输出中该序列到包括换行符在内的内容被删除。

以下是 sendmail.cf 文件片段的摘录：

```
C# "Smart" relay host (may be null)
DS
# operators that cannot be in local usernames (i.e., network indicators)
CO @ % !
# a class with just dot (for identifying canonical names)
C..
# a class with just a left bracket (for identifying domain literals)
C[[
# access_db acceptance class
C{Accept}OK RELAY
C{ResOk}OKR
# Hosts for which relaying is permitted ($=R)
FR-o /etc/mail/relay-domains
```

这是 sendmail.mc 文件中的引用，供对比参考：

```
define(`SMART_HOST',`smtp.your.provider')
define(`confDEF_USER_ID',`8:12')
undefine(`UUCP_RELAY')
undefine(`BITNET_RELAY')
define(`confAUTO_REBUILD')
define(`confTO_CONNECT', `1m')
define(`confTRY_NULL_MX_LIST',true)
```

> 你可以明白为什么该文件被描述为“晦涩难懂”。

而不是让你深入理解手动编辑一个众所周知最难成功编辑的文件的过程，我们将查看 Donncha O'Caoimh 开发的一个 Perl 脚本。该脚本通过提示你输入信息并自行修改 Sendmail 配置文件来自动化 Sendmail 的配置。该脚本在运行 Fedora 的家用计算机上设置网络邮件服务器。要使用该脚本，你需要知道你的电子邮件地址、所有邮件用户的登录名和密码、你的邮件服务器地址以及网络的 IP 地址。完成后，Sendmail 和 Fetchmail 将被配置。运行该脚本不仅会提示你输入所有必要的信息，而且在过程中还会提供一些问题解释和帮助。

在开始之前，你应该已经在系统中安装了 Sendmail 和 Fetchmail。该脚本可以在 http://cork.linux.ie/projects/install-sendmail/ 下载。只需解压归档文件：

```
$ tar -zxvf install-sendmail-5.5.tar.gz
```

现在使用 cd 命令切换到新创建的目录。

你可以阅读之前提到的网站上的 README、FAQ 和 INSTALL 文件中对该脚本及其用法的绝佳描述。在继续安装之前，你应该阅读这些文件；它们写得很好，并将回答你所有的问题。如果你对使用 Perl 编程的强大功能感兴趣，请参阅第 29 章，“使用 Perl”。

当然，你也可以手动配置 Sendmail，尤其是当你需要任何高级选项时。以下五个部分介绍了一些常用的高级选项。

## 配置伪装（Masquerading）

有时你可能希望 Sendmail 伪装成除系统实际主机名以外的其他主机。这种情况可能发生在你有拨号连接到互联网且你的 ISP（互联网服务提供商）为你处理所有邮件时。在这种情况下，你希望 Sendmail 伪装为你 ISP 的域名。例如，

```
MASQUERADE_AS(`sample1.net.org')
```

### 使用智能主机（Smart Hosts）

如果你没有全天候连接到互联网，你可能希望 Sendmail 将消息发送到你的 ISP 的邮件服务器并让它为你处理投递。如果没有全天候的互联网连接，你可能会发现向某些位置（如世界上一些电子邮件服务不可靠且间歇性服务的落后地区）投递消息非常困难。在这种情况下，你可以配置 Sendmail 作为智能主机，将电子邮件转交给另一个发送者，而不是尝试直接投递电子邮件。你可以在 sendmail.mc 文件中可以使用如下一行来启用智能主机：

```
define(`SMART_HOST', `smtp.samplenet.org')
```

这一行使 Sendmail 将其接收的任何邮件传递给服务器 smtp.samplenet.org，而不是尝试直接投递。如果你的 ISP（像许多其他 ISP 一样）阻止任何邮件中继，那么智能主机对你将不起作用。一些 ISP 阻止中继，因为它经常被用于传播垃圾邮件。

### 设置消息投递间隔

如前所述，Sendmail 通常尝试在收到消息时尽快投递，并在此后按固定间隔再次尝试。如果你只有定期连接到互联网，例如通过拨号连接，你很可能希望 Sendmail 将所有消息保留在队列中，并在特定的时间间隔或你的提示下进行投递尝试。你可以通过向 sendmail.mc 添加以下行来配置 Sendmail 执行此操作：

```
define(`confDELIVERY_MODE', `d')
```

这一行将使 Sendmail 仅在定期安排的队列处理间隔（默认情况下，介于 20 到 30 分钟之间）尝试邮件投递。

但是，如果你离线时间较长，这个延迟时间可能不够。在这种情况下，你可以调用没有队列处理时间的 Sendmail。例如，默认情况下，Sendmail 可能会以如下命令启动：

```
# sendmail -bd -q30m
```

这告诉 Sendmail 它应该每 30 分钟处理一次邮件队列（并尝试消息投递）。你可以将 30 更改为其他任何数字来更改投递间隔。如果你想让 Sendmail 等待特定提示后再处理队列，你可以像这样调用没有队列时间的 Sendmail：

```
# sendmail -bd -q
```

此命令告诉 Sendmail 在启动时处理一次队列，并且只有当你手动指示时才再次处理。要手动告诉 Sendmail 处理队列，你可以使用如下命令：

```
# sendmail -q
```

![](img/774d40fd20903495c5cd00e2efad3f33_702_0.png)

如果你使用调制解调器进行联网，有一个用于 `pppd` 的配置文件名为 `ppp.linkup`，位于 `/etc/ppp` 中。该文件中的任何命令都将在每次启动 PPP 守护进程时自动运行。你可以将 `sendmail -q` 行添加到该文件中，以便每次拨号连接到互联网时自动处理你的邮件队列。

## 构建 sendmail.cf 文件

书籍可供深入探索 Sendmail 配置的深度，但 Sendmail 安装和操作指南是权威参考。通过 Google 搜索也可以找到配置指南；许多人在许多不同的配置中使用 Sendmail。幸运的是，Fedora 提供了默认的 Sendmail 配置，只要你的网络配置正确且不需要类似 ISP 的 Sendmail 配置，它将“开箱即用”地适用于家庭用户。

在你完成对 `sendmail.mc` 的所有更改后，你需要重新构建 sendmail.cf 文件。首先，备份你的旧文件：

```
# cp /etc/mail/sendmail.cf /etc/mail/sendmail.cf.old
```

你必须通过 `m4` 宏处理器运行 `sendmail.mc` 以生成可用的配置文件。使用如下命令来执行此操作：

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

此命令从 /usr/share/sendmail-cf/m4/cf.m4 加载 `cf.m4` 宏文件，然后使用它处理 `sendmail.mc` 文件。输出通常发送到 STDOUT，然后重定向到文件 `sendmail.cf`，你的新配置文件就准备好了。在更改生效之前，你需要重启 Sendmail。

![](img/774d40fd20903495c5cd00e2efad3f33_702_1.png)

Fedora 还提供了使用 `awk` 重新构建 Sendmail 配置的替代方案。作为 root，执行

```
# make -C /etc/mail
```

## 邮件中继（Relaying）

默认情况下，Sendmail 不会中继并非源自本地域的邮件。这意味着，如果在 lion.org 运行的 Sendmail 安装接收到旨在发送给 cheetah.org 的邮件，且该邮件并非源自 lion.org，该邮件将被拒绝且不会被中继。如果你想允许特定位置通过你中继，请将域名的条目添加到文件 `/etc/mail/relay-domains`。如果文件不存在，只需在你的首选文本编辑器中创建它，并添加一行包含你希望允许通过你中继的域名。此更改需要重启 Sendmail 才能生效。
