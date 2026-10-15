

和社交问题。每个新闻组都以更高级别主题的子集命名。例如，新闻组 comp 涉及所有计算机主题。新闻组 comp.laptops 涉及笔记本电脑问题。通常层级会深入好几层。例如，新闻组 comp.databases.oracle.server 涉及 Oracle 服务器数据库问题。

## NOTE

新闻组文章的格式遵循互联网标准文档请求评论（RFC）1036 中定义的严格指南。每篇文章必须包含两个不同的部分：标题行和消息正文。

标题行标识有关文章何时以及由谁发布的信息。消息正文应仅包含标准 ASCII 文本字符。新闻文章中不应发布二进制字符或文件。为规避此限制，二进制文件会通过使用标准的 Unix uuencode 程序或更新的多用途互联网邮件扩展（MIME）协议转换为文本数据。然后将生成的文本文件发布到新闻组。新闻组阅读器随后可以将发布的文本文件解码回其原始二进制形式。

针对共同主题发布的文章集合称为线程。线程可以包含许多文章，因为用户会针对其他已发布消息发布消息。一些新闻组程序允许用户根据它们所属的线程来跟踪文章。这有助于简化新闻组中文章的组织。

## TIP

免费新闻服务器 news.gmane.org 通过各种组提供 Red Hat 和 Ubuntu 邮件列表。Beta 列表可作为 gmane.linux.redhat.rhl.beta 获取。这是一种方便阅读线程讨论的方式，比使用 Ubuntu 邮件列表存档更容易。

用于将新闻组文章从一台主机传输到另一台主机的协议是网络新闻传输协议（NNTP），定义在 RFC 977 中。 （您可以在 ftp://metalab.unc.edu/pub/docs/rfc/ 上搜索 RFC；查看文件 rfc-nn at.txt。）NNTP 被设计为简单的客户端/服务器协议，使两台主机能够以高效的方式交换新闻组文章。

## The Pan News Client Newsreader

无论您的 Ubuntu 服务器是否设置为主新闻服务器，您都可以使用新闻阅读器程序来阅读新闻组文章。新闻阅读器程序只需要连接到新闻服务器即可。新闻服务器是在同一台机器上还是在世界另一端的远程新闻服务器并不重要。

有多个程序可用于 Unix 系统以连接到新闻服务器来阅读和发布新闻组中的文章。在这里我们将讨论 Pan 新闻客户端。

Pan 是一款与 GNOME 配合使用的图形新闻阅读器客户端，是 Ubuntu 的默认新闻阅读器。如果您已安装 GNOME 库（通常默认安装），您也可以在 K 桌面环境（KDE）中使用 Pan。Pan 具有下载并显示所有新闻组以及显示已发布新闻文章的功能。您可以通过使用 GNOME 或 KDE 桌面面板或从 X 终端窗口的命令行使用命令 pan & 来启动它。Pan 支持组合多部分消息以及 yenc 编码/解码协议。图 5.17 显示了 Pan 显示的示例。

![](img/8f9e74e2b343ff525bebfb720a3d8441_158_0.png)

FIGURE 5.17 The Pan graphical newsreader is one of the nicest available for Linux, shown here displaying an image attached to a news article.

首次运行 Pan 时，会出现配置向导，提示您输入新闻服务器名称（也称为 NNTP 名称）、连接端口详细信息，以及该服务器的可选用户名和密码。您还可以设置过期选项并优先考虑一个服务器而不是其他服务器。向导完成后，会提示您下载服务器提供的新闻组列表：这可能需要一段时间。如果您需要更改新闻服务器或添加额外的服务器，您可以访问 Edit 菜单下的 Preferences 项目以调出服务器列表，如图 5.18 所示。然后您突出显示适当的服务器并单击 Edit 以更改它，或直接单击 New 按钮添加新的新闻服务器。

![](img/8f9e74e2b343ff525bebfb720a3d8441_159_0.png)

FIGURE 5.18 The Pan news server configuration window.

## Videoconferencing with Ekiga

Ekiga 是一款互联网视频会议应用程序，通过使用 H.323 协议进行 IP 电话（也称为语音 over IP，VoIP）提供双向语音和图像传输。它是一个类似于 Microsoft NetMeeting 的应用程序，并作为 Ubuntu 的默认视频会议客户端提供。

在您充分利用 Ekiga 的电话和视频会议功能之前，您必须配置全双工功能的声卡和视频设备（请参阅第 7 章，“多媒体应用程序”）以及摄像头。

Ekiga 在 Internet 菜单中作为 Videoconferencing 找到；您单击图标即可启动它。首次启动 Ekiga 应用程序时，会运行配置向导，您会看到四个配置屏幕中的第一个。您只需输入您的姓名、电子邮件地址和位置并选择您的连接类型。您的音频和视频设备的设置会自动检测；您可以通过从 Edit 菜单中选择 Preferences 项目来查看它们。图 5.19 显示了 Ekiga 的运行情况，准备拨号给另一用户。

