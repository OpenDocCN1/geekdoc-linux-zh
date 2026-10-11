
很难跟踪一份能正常工作的应用程序列表。然而，大多数普通的互联网应用程序都得到支持，例如浏览互联网（Netscape、MSIE 等）、FTP（如 WSFTP）、Real Audio、Telnet、SSH、POP3（接收电子邮件——Pine、Outlook）、SMTP（发送电子邮件）等等。

涉及更复杂协议或特殊连接方式的应用程序，例如视频会议软件，需要特殊的辅助工具。

更多细节，请参阅 Lee Nevo 的 `http://dijon.nais.com/~nevo/masq/`，该页面介绍了通过 Linux IP 伪装工作的应用程序。

## 如何在 Red Hat、Debian、Slackware 等系统上运行 IP 伪装？

无论你使用哪种 Linux 发行版，本 HOWTO 中提到的设置 IP 伪装的步骤都应该适用。一些发行版可能有图形界面或特殊配置文件，使设置更容易。我们尽力将 HOWTO 写得尽可能通用。

## 我刚刚升级到 2.2.x 内核；为什么 IP 伪装不工作？

假设你的 Linux `ipmasq` 机器已经拥有到互联网和你局域网的正确连接，你应该检查以下几件事：

- 确保你已编译并加载了必要的功能和模块。详见前面章节。
- 检查 `/usr/src/linux/Documentation/Changes`，确保你安装了网络工具的最小要求。
- 确保你已启用 IP 转发。尝试运行 `echo 1 > /proc/sys/net/ipv4/ipforwarding`。
- 你应该使用 `ipchains` (`http://www.rustcorp.com/linux/ipchains/`) 来操作 `ipmasq` 和防火墙规则。
- 再次检查所有设置和配置步骤！很多时候只是你忽略的拼写错误或愚蠢的错误。

## 我刚刚升级到 2.0.30 或更高版本的内核；为什么 IP 伪装不工作？

假设你的 Linux `ipmasq` 机器已经拥有到互联网和你局域网的正确连接，你应该检查以下几件事：

- 确保你已编译并加载了必要的功能和模块。详见前面章节。
- 检查 `/usr/src/linux/Documentation/Changes`，确保你安装了网络工具的最小要求。
- 确保你已启用 IP 转发。尝试运行 `echo 1 > /proc/sys/net/ipv4/ipforward`。
- 你应该使用 `ipfwadm` (`http://www.xos.nl/`) 来操作 `ipmasq` 和防火墙规则。你需要修补 2.0.x 内核以使用 `ipchains`。
- 再次检查所有设置和配置步骤！很多时候只是你忽略的拼写错误或愚蠢的错误。

## 我无法让 IP 伪装工作！在 Windows 平台上我有什么选择？

放弃一个免费的、可靠的、高性能的且在最低配置硬件上即可运行的解决方案，转而支付巨额费用去使用需要更多硬件、性能更低且可靠性较差的东西？（是的，我在这方面有真实的经验。）

好吧，这是你的决定。搜索 MS Proxy Server、Wingate，或者查看 `www.winfiles.com`。不要告诉任何人是我推荐给你的。

## 我已经检查了所有配置，但仍然无法让 IP 伪装工作。我该怎么做？

- 保持冷静。给自己泡杯茶休息一下，然后尝试下面提到的建议。
- 查看 IP 伪装邮件列表存档 (`http://home.indyramp.com/lists/masq/`)；很可能你的答案在那里等着你。
- 将你的问题发布到 IP 伪装邮件列表；然后参见常见问题以获取详细信息。请只有在无法在邮件列表存档中找到答案时才尝试此操作。
- 将你的问题发布到相关的 Linux 网络新闻组。
- 发送电子邮件给 `ambrose@writeme.com` 和 `dranch@trinnet.net`。如果你给我们两人都发送，得到回复的机会更大。David 通常很善于回复，而我不想评论我的响应时间。
- 再次检查你的配置。

## 我如何加入 IP 伪装邮件列表？

通过向 `masq-subscribe@indyramp.com` 发送电子邮件来加入 Linux IP 伪装邮件列表。

消息的主题和正文会被忽略。这将让你收到列表发出的每条消息。如果你需要，可以使用此格式，但如果你能承受摘要（digest），请选择它。摘要对列表服务器的负载较小。注意，你只能从你订阅的账户/地址发布消息。

更多命令，请向 `masq-help@tori.indyramp.com` 发送电子邮件。

## 我想参与 IP 伪装开发。我能做什么？

通过向 `masq-dev-subscribe@tori.indyramp.com` 发送电子邮件加入 Linux IP 伪装开发者（DEVELOPERS）列表，并询问那里优秀的开发者（或者使用摘要格式，请发送至 `masq-dev-digest-subscribe@tori.indyramp.com`）。

请勿在该列表中询问与 IP 伪装开发无关的问题。

## 我在哪里可以找到更多有关 IP 伪装的信息？

你可以在由 David 和我共同维护的 Linux IP 伪装资源库中找到更多有关 IP 伪装的信息。参见 6.2 节了解可用性。

你也可以在由 Indyramp Consulting 维护的“半原创 Linux IP 伪装”网站 (`http://www.indyramp.com/masq/`) 上找到更多信息，该网站也提供 `ipmasq` 邮件列表。

## 我想将此 HOWTO 翻译成另一种语言。我该怎么做？

确保你想翻译的语言没有被其他人覆盖。可用的 HOWTO 翻译列表可以在 Linux IP 伪装资源库 (`http://ipmasq.cjb.net/`) 上找到。

向 `ambrose@writeme.com` 发送电子邮件，我将发送最新版 HOWTO 的 SGML 源文件给你。

## 这个 HOWTO 似乎过时了。你仍在维护它吗？

是的，这个 HOWTO 仍在维护中。我因为忙于两份工作而内疚，没有太多时间处理这个；我很抱歉。不过，随着 David Ranch 加入作为 HOWTO 的主要维护者，情况应该会改善。

如果你想到可以包含在 HOWTO 中的主题，请给 David 和我发送电子邮件。如果你能提供该信息会更好。如果合适，David 和我将把信息包含在 HOWTO 中。非常感谢你的贡献。

我们有很多新的想法和计划来改进 HOWTO，例如涵盖涉及 IP 伪装的不同网络配置的案例研究、更多安全性内容、`ipchains` 的使用、`ipfwadm`/`ipchains` 规则集示例，

更多的常见问题解答，更多关于协议和端口转发工具（如 masqadmin）的覆盖范围，等等。如果您认为您能提供帮助，请尽管参与。谢谢。

## 我已经让 IP 伪装（IP Masquerade）运行起来了，太棒了！我想感谢你们。我可以做些什么？

感谢开发人员，并珍惜他们为此付出的时间和精力。给我们发一封电子邮件，告诉我们您有多开心。向其他人介绍 Linux，并在他们遇到问题时帮助他们。

## 杂项

本节包含一个有用资源的列表，关于 IP 伪装资源页面的信息，以及致谢。

### 有用资源

- IP 伪装资源页面（IP Masquerade Resource page）应包含足够的信息来设置 IP 伪装：`http://ipmasq.cjb.net/`。
- IP 伪装邮件列表存档（IP masquerade mailing list archive）包含发送给邮件列表的一些最近消息：`http://www.indyramp.com/masq/list/`。
- 适用于内核 2.2.x 和 2.0.x 的 Linux IP 伪装迷你 HOWTO（Linux IP Masquerade mini-HOWTO）：`http://ipmasq.cjb.net/ipmasq-HOWTO.html`。
- 如果您使用的是较旧的内核，请参阅适用于内核 1.2.x 的 IP 伪装 HOWTO（IP Masquerade HOWTO）：`http://ipmasq.cjb.net/ipmasq-HOWTO-1.2.x.txt`。
- IP 伪装常见问题解答（IP masquerade FAQ）包含一些通用信息：`http://www.indyramp.com/masq/ip_masquerade.txt`。
- Linux IPCHAINS HOWTO（参见第 14 章）以及 `http://www.rustcorp.com/linux/ipchains/` 提供了大量关于 ipchains 使用的信息，以及 ipchains 的源代码和二进制文件。
- X/OS Ipfwadm 页面包含关于 ipfwadm 包的源代码、二进制文件、文档和其他信息：`http://www.xos.nl/linux/ipfwadm/`。
- Lee Nevo 撰写的关于通过 Linux IP 伪装（Linux IP masquerading）运行的应用程序的页面提供了有关使应用程序与 IP 伪装配合使用的提示和技巧：`http://dijon.nais.com/~nevo/masq/`
