
GAIM 支持 Jabber，这是一种基于 XML 的开放 IM 协议，可用于建立企业 IM 服务器。Red Hat 未提供 Jabber，但你可以从 Jabber 主页 http://www.jabber.com/ 获取更多相关信息。你可以从 http://jabber.jabberstudio.org/ 获取 Jabber 服务器——Jabber。

KIT 是一个简单的 KDE IM 客户端。当你首次启动 KIT 时，它会提议去 AOL 创建新个人资料。在你选择用户名和密码并被接受后，你就退出了“注册”过程。你会收到一封邮件，必须回复该邮件以确认你的账户并完成注册。

# 第20章 新闻与其他协作通信

## 使用 GnomeMeeting 进行视频会议

GnomeMeeting 是一款互联网视频会议应用程序，它通过使用用于 IP 电话的 H.323 协议（也称为 IP 语音 VoIP））在互联网上提供双向语音和图像。它是随 Red Hat Linux 提供的。在充分利用 GnomeMeeting 的电话和视频会议功能之前，你必须配置全双工声卡和视频设备（参见第 26 章，“多媒体应用”）以及摄像头。

GnomeMeeting 位于菜单的“视频会议”中；点击图标即可启动它。当你第一次启动 GnomeMeeting 应用程序时，会看到四个配置屏幕中的第一个。你只需输入你的姓名、电子邮件地址和位置，并选择你的连接类型。音频和视频设备的设置会自动检测；你可以通过选择“编辑”菜单中的“偏好”项来查看它们。

20.9 GnomeMeeting 演示。要查看与服务器列出的当前在线用户列表，你可以点击左上标记为 ILS 的书本图标，随后会显示当前在线用户列表。

![](img/446debe023486a07fde575245cf7a3ff_719_0.png)

图 20.9 GnomeMeeting 友好的用户界面设计。

当你运行 GnomeMeeting 时，你必须在 http://ils.seconix.com/ 注册服务器以启用会议。GnomeMeeting 能够与 Microsoft NetMeeting 协作；你应该要求 NetMeeting 用户在 http://ils.seconix.com/ 注册，这样你就能看到他们，因为 NetMeeting 只能看到其他 NetMeeting 用户。你可以在 GnomeMeeting 主页 http://www.gnomemeeting.org/ 找到一个信息丰富的 FAQ。关于 VoIP 的极佳文章位于 http://freshmeat.net/articles/view/430。

> 注意
> 
> 如果你使用像 GnomeMeeting 这样的 VoIP 应用程序，你会厌于重复输入长 IP 地址来建立连接。为了避免这种麻烦，你可以使用“网门员”（gatekeeper），其目的类似于 DNS 服务器，能将名称翻译为 IP 地址。OpenH323 Gatekeeper 就是这样一种流行的网门员应用程序。它未随 Red Hat 8.0 提供，但你可以从 http://www.gnuk.org 获取。

## 使用 Mail 管理邮件列表

使用邮件列表是地理分散的个人进行协作的一种日益常见的方式。邮件列表是通过电子邮件进行的小组讨论。然而，你不需要向每位感兴趣的参与者发送单独的消息，而是向自动邮件列表服务器发送单条消息，由它向每个订阅用户发送消息。当你收到来自列表的邮件并回复某条消息时，该消息将发送到 Mailman 列表管理器，然后重新发送给列表上的所有人。Red Hat 维护许多邮件列表，并使用邮件列表管理器 Mailman 来实现。Red Hat 8.0 提供了 Mailman。

Mailman 跟踪谁订阅了列表，谁没有电子邮件地址。邮件列表管理器通过 Web 界面处理所有新的订阅和取消，甚至可以生成列表上所有消息的存档。

对于每个列表，都会指定一个人作为邮件列表管理员。管理员具有受密码保护的特殊 Web 权限。他或她可以手动从列表中添加和删除成员，并删除被判定为攻击性的邮件。还可以将列表配置为受审核模式，在这种情况下，审核员会在消息传递给 Mailman 分发给订阅者之前阅读所有消息。列表还可以配置为允许非成员发布内容，但该选项很少使用，因为大多数管理员希望让未经授权的帖子不要出现在列表中。

某些列表被称为“高流量”列表，每天发布的消息很多。其他被称为“低流量”的列表，每天发布的消息很少，甚至根本没有。一种配置选项是将所有消息合并成一份摘要（digest），这样在 Mailman 接收到预设数量的消息后，只发送一条消息。还可以建立最大消息大小，并禁止消息附件。

> Red Hat 8.0 的部分测试和开发是在一个邮件列表进行的。如果你好奇，可以在 https://listman.redhat.com/pipermail/limbo-list/ 查看存档。

使用 Mailman 管理邮件列表之前，你必须先安装并配置 Sendmail（参见第 19 章，“处理电子邮件”）。

在安装 RPM 后（使用包管理器或手动使用 `# rpm -ivh`），你可以查看 `/usr/share/doc/mailman-2.0.13` 中的已安装文档，特别注意 `README.REDHAT` 中的简单安装说明。

以下是安装和配置 Mailman 的一些建议：

- 设置一个不容易被猜到但又复杂至于会被忘记的密码。

- 文件 `/etc/sysconfig/sendmail` 中找到默认值可以保持不变，因为它们不需要更改。

- 你必须使用文本编辑器手动将 `conf/httpd-mailman.conf` 添加到文件 `/etc/httpd/conf/httpd.conf` 中。考虑到 Red Hat 在设置 Mailman 方面所付出的努力，这种遗漏是令人惊讶的。该行代码本应由 RPM 安装程序自动添加。文件中已经有一行以 `Include` 开头的代码了，你需要找到该行并在其下方添加新行，然后保存文件。

完成文本添加后，你可以重启 httpd：

```bash
service httpd restart
```

如果你在 Mailman 的安装和设置过程中遇到任何问题，可以在 Mailman `INSTALL`、`README.SENDMAIL` 和 `README.EXIM` 文件中查找额外的配置和故障排除提示。这些文件为使用 Postfix 或 Exim 程序代替 Sendmail 的用户提供了配置信息。

所有的 Mailman 命令都保存在 `/var/mailman` 中。尽管它们的所有者是 root，但它们属于 mailman 组。

要手动运行 Mailman 命令，你需要切换目录到 `/var/mailman/bin` 并在那里运行它们。你需要在所有 Mailman 命令前加上 `./`，因为它们不在你的路径中（出于安全考虑），这样做是告诉 shell 在当前目录而非默认路径查找命令。

要创建一个新的邮件列表，使用 `newlist` 命令，如下：

```bash
./newlist
```

运行命令后，系统会提示你输入新邮件列表的名称、列表管理员的电子邮件地址以及密码；随后 `newlist` 命令会向管理员发送一封电子邮件，告知管理员列表已激活。该邮件还提供了管理列表的 URL 和密码。虽然如果你是 root 用户，可以从 `/var/mailman` 目录手动管理邮件列表，但最简单且最推荐的方法是通过 Web 界面管理列表。

如果你是列表管理员且没有看到那条通知消息，可以将浏览器指向 `http://localhost/mailman/admin`，选择相应的列表并输入密码。你将被重定向到该列表的选项页面（如图 20.10 所示）。向下滚动到此屏幕即可修改选项。每个可以修改的项目描述旁边都有一个链接名称（Details）；点击该链接将显示一个上下文相关的帮助屏幕。

![](img/446debe023486a07fde575245cf7a3ff_722_0.png)

图 20.10 名名为 Rhl8.0 的邮件列表的 Mailman 管理页面。

图 20.11 所示的配置选项和其他管理活动是可以点击的链接，允许访问 Mail 提供的全范围管理选项。

任何想要订阅列表的人都可以访问 `http://localhost.localdomain/mailman/` 显示的页面，填写其姓名和电子邮件地址，然后选择密码。在获得批准后，该人员将收到一封成员邮件通知。

> 注意：Christopher Kolar 为管理邮件列表汇编了“用户文档”、“快速参考指南”和“管理员指南”；这些指南可以在 http://staff.isa/~ckolar/mailman/ 免费获取。这些指南编写得非常专业，是不可或缺的资源。“站点管理员文档”可以在 http://www.list.org/admins.html 处找到。在这里你可以了解如何使用 `/var/mailman/bin` 中的脚本，这些脚本在你编写用于自动化许多管理任务的脚本时非常有用；它是另一个不可或的资源。

## 相关的 Red Hat Linux 命令
