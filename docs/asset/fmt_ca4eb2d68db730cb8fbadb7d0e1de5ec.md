
```bash
HACK(check_mail3,'hash -a@UUNK /etc/mail/deny' )
HACK(use_id, '/etc/mail/ip_allow')
HACK(use_names, /etc/mail/name_allow')
HACK(use_relayto, '/etc/mail/relay_allow')
HACK(check_rtcp4)
HACK(check_RELAY3)
```

从 `sendmail` 的 V8.9 系列开始，默认情况下拒绝外部主机中继。这是为了防止其他主机将您的邮件服务器用作分发垃圾邮件（spam）或其他用途的中继点。这些 `HACK` 允许您指定哪些主机被允许将您的邮件服务器用作中继点，以及互联网上哪些机器永远不接受其邮件。如果您和您的用户不断从相同的主机收到垃圾邮件，这会特别有用。请阅读 `/usr/lib/sendmail.cf/README.check` 文件，其中描述了所有可用的 `HACK` 及其使用方法。

### 提示

假设您的用户收到大量电子邮件广告（或 SPAM）并向您投诉。假设所有 SPAM 都来自相同的主机。您可以做的就是阻止该主机向您的站点发送任何电子邮件。这是通过编辑文件 `/etc/mail/deny` 并添加一条目来实现的，例如 "`192.168.1.2 We do not accept mail from spammers.`"。然后输入命令 `# makemap hash /etc/mail/deny.db < /etc/mail/deny` 创建供 `sendmail` 使用的数据库。

您需要使用 `nslookup` 查找垃圾邮件主机的 IP 地址，并将其放入 `deny` 文件中。当对应于 IP 地址 `192.168.1.2` 的主机试图与您的 `sendmail` 进程通信时，它将收到一个错误代码以及连接被拒绝的可配置文本原因。

如你所见，提供的 `redhat.mc` 文件为你的 `mc` 文件提供了一个相当不错的模板。你已将它复制到 `gonzo.mc` 中。现在你所需要做的就是添加另外两个条目，然后你就可以创建 `cf` 文件，供 `sendmail` 使用。在 `FEATURES` 列表之后添加以下内容：

```text
FEATURE(masquerade_envelope)
MASQUERADE_AS(gonzo.gov)
```

这些行假定你的 `Gonzo` 邮件主机名为 `mail.gonzo.gov`。如果没有这些行，从你的邮件主机发出的所有邮件，其信封和消息体中的 `From:` 地址都会类似于 `joe@mail.gonzo.gov`。将发送源主机隐藏起来，让接收方看到的 `From:` 地址类似于 `joe@gonzo.gov` 会好得多。这正是 `MASQUERADE_AS` 行的作用。`masquerade_envelope` 功能会使消息信封的 `From:` 标头进行类似的伪装。

现在你需要做的就是构建 `sendmail` 配置文件：

```bash
[root@gondor cf]# make gonzo.cf
rm -f gondor.cf
m4 ..../m4/cf.m4 gondor.mc > gonzo.cf
chmod 444 gonzo.cf
```

如果你使用的是 `GNU Make`（如果你在运行 `Red Hat`，几乎可以肯定就是这样），在输入 `make` 命令后你会遇到错误。请尝试使用 `make Makefile.dist` `gonzo.cf`。如果 `make` 成功，一个 `gonzo.cf` 文件将出现在你的 `cf` 目录中。恭喜你，你创建了你第一个 `sendmail.cf` 文件！

## 经过这一切之后，还有一种更简单的方法

Perl 社区中常见的评论是“实现目标不止一种方法。”这再次体现了 Perl 的根源，因此我在此提供最后一种配置 `sendmail` 的方法，感谢爱尔兰 Linux 用户组的 Donncha Ó Caoimh 所做的艰苦工作（<http://www.linux.ie>）。他的 `install-sendmail` 脚本可在 <http://cork.linux.ie/projects/install-sendmail/> 获取，其工作原理是询问用户一系列问题（在更新 `system` 文件时会提示输入 `root` 密码，但请勿以 `root` 身份运行它），以便根据其需求配置系统。脚本包含信息丰富的 `README` 和 `INSTALL` 文件，使用前应仔细阅读它们。以下是 2000 年 3 月 13 日版本的示例会话：

```bash
[kevin@moo kevin]$ wget http://cork.linux.ie/projects/install-sendmail/install-sendmail-5.3.1.tar.gz
-21- 12.2k ---> http://cork.linux.ie:80/projects/install-sendmail/install-sendmail-5.3.1.tar.gz
=> 'install-sendmail-5.3.1.tar.gz'
Connecting to cork.linux.ie:80... connected!
HTTP request sent, awaiting response... 200 OK
Length: 39,807 (application/x-tar)

OK -> ... [100%]

21:18:30 (7.78 KB/s) - 'install-sendmail-5.3.1.tar.gz' saved [39807/39807]
[kevin@mo kevin]$ cp /kevin/install-sendmail-5.3.1.tar.gz .
[kevin@mo kevin]$ tar zxf install-sendmail-5.3.1.tar.gz
[kevin@mo kevin]$ cd install-sendmail-5.3.1
[kevin@mo install-sendmail-5.3.1]$ ./install-sendmail -c
```

随后它会问以下问题：

你想使用哪种语言？English(1)

1.1 你希望该机器发出的所有电子邮件使用什么地址？gonzo.gov

1.2 所有发往 gonzo.gov 的邮件都会到达这台机器吗？n

2.1 你希望出站邮件通过外部邮件服务器发送吗？

如果你使用调制解调器拨号连接，这里最好回答 Y。y

2.1.1 你将邮件发送到哪里？（出站 smtp 服务器，通常是你的 ISP

[smtp.isp.com]）？mail.gonzo.gov

2.2. 使用远程邮件？如果你有拨号连接，可以在离线时撰写邮件，

然后在你连接时将其'排队'发送。

（不过，你必须运行 '`usr/bin/sendmail -q`' 来发送邮件。）

本地邮件（发往登录你机器的人的邮件）仍将正常投递。

如果对此问题回答 "no"，所有邮件将立即投递，而不是排队。这可能会导致你的机器在高峰时段

拨号连接。

你希望远程邮件排队吗？y

3.1 你想为本地网络提供邮件服务吗？n

4. 虚拟域支持

4.1 你需要此功能吗？我还会提供

输入别名映射的方法。n

5. 通用表支持

5.1 你想将本地电子邮件地址映射为新地址吗？y

5.1.1 输入你想映射的本地用户名。

完成后输入 "none"。

[bob]? kevin

5.1.1 当 kevin 写电子邮件时，人们应该看到什么地址？

[den@fsomeplace.org]? csainhs@gonzo.gov

5.1.2 输入你想映射的本地用户名。

完成后输入 "none"。

[?] none

6. 传入邮件服务器

6.1 你需要 Fetchmail 支持吗？y

6. 传入邮件服务器

6.1.1 输入你用于轮询邮件的 pop 服务器。完成后输入 "none"。

[pop.isp.com]? pop.gonzo.gov

6.1.2 你使用什么用户名登录 pop.gonzo.gov？

[alan]? caomh

6.1.3 你使用什么密码登录 pop.gonzo.gov？

[password]? moo

6.1.4 哪个用户应接收 caomh 的邮件？

[bob]? kevin

6.1.5 pop.gonzo.gov 使用什么协议？(POP3, IMAP, AUTO)

[pop3]? imap

6.1.6 输入你用于轮询邮件的 pop 服务器。完成后输入 `none`。

[pop.telebot.com]? none

在此时它会要求提供 root 密码以安装文件。之后你应该使用以下命令重启 sendmail：

```bash
/etc/init.d/sendmail restart
```

对于初次在家用系统上使用 sendmail 的用户来说，这是一个优秀的工具。前面的章节介绍了企业大学系统管理员应使用的方法。

# 测试 sendmail 和 sendmail.cf

在安装新的或修改过的 `sendmail.cf` 之前，你必须对其进行彻底测试。即使是微小的、看似无害的更改也可能导致灾难，当邮件系统出现问题时，人们会非常愤怒。
