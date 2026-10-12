

![](img/2045828cf45e5632bf056f9ca99d6755_264_0.png)

**图 8.15** 一个 Usenet 文章显示示例，展示了一条关于互联网邮件 FAQ 的已发布消息。

![](img/2045828cf45e5632bf056f9ca99d6755_264_1.png)

**图 8.16** Pan 图形新闻阅读器是 Linux 上可用的最出色的阅读器之一，此处展示了它正在显示附在新闻文章中的图像。

首次运行 Pan 时，会出现一个配置向导，提示你输入姓名、SMTP 服务器名称、NNTP 服务器名称，以及你希望用于标识连接的名称（在图 8.17 所示的示例中，我们使用了 Cavtel）。向导完成后，系统将提示你下载服务器提供的新闻组列表；这可能需要一些时间。如果需要更改新闻服务器或添加额外服务器，你可以通过 Edit 菜单下的 Preferences 项访问服务器列表。在那里，你突出显示相应的服务器并点击 Edit 进行修改，或者直接点击 New 按钮添加新的新闻服务器。

![](img/2045828cf45e5632bf056f9ca99d6755_265_0.png)

**图 8.17** Pan 新闻服务器配置窗口。

## KNode 新闻客户端

KNode 程序是 kdenetwork RPM 软件包的一部分——即 Fedora Core 中包含的 KDE 网络软件包；如果你在安装 Fedora Core 时选择了 KDE 窗口管理器选项，通常默认会安装 KNode。

KNode 程序是一个优秀的图形化程序（类似于 MS Outlook Express），允许你连接到新闻服务器（本地或远程服务器），并选择你可以阅读和发布文章的新闻组。不过，在开始之前，你必须在 KNode 中配置新闻服务器的地址。你可以通过主 KNode 窗口上的 Settings 菜单项来完成此操作；选择 Configure KNode 项，KNode 配置窗口将出现。在 Accounts 项下，选择 News 项。窗口中将显示已配置的新闻服务器列表。要添加新的新闻服务器，点击 New 按钮。图 8.18 显示了 KNode 新账户窗口，你可以在此输入新的新闻服务器信息。

![](img/2045828cf45e5632bf056f9ca99d6755_266_0.png)

**图 8.18** KNode 新闻阅读器；设置快速且简单。它是纯文本新闻组的极佳阅读工具。

## Mozilla 新闻客户端

Mozilla 网页浏览器支持图形化的 Usenet 新闻阅读以及网页浏览。在 Fedora Core 系统上安装多个新闻阅读客户端为用户提供丰富的选择和培养喜好的机会。然而在某些情况下，这可能会使管理员跟踪和修复客户端安全漏洞的任务变得复杂。使用 Mozilla 可以通过提供集网页浏览、电子邮件、文件传输和新闻阅读功能于一体的一体化客户端来简化此任务。出于这些原因，你可能会选择使用 Mozilla 作为浏览器、电子邮件客户端和新闻客户端。Mozilla 是 Fedora Core 的默认浏览器。

要开始使用 Mozilla 阅读新闻，启动 Mozilla 并选择 Window, Mail and Newsgroups；将显示图 8.19 所示的窗口。菜单 Edit, Mail & Newsgroups Account Settings 是配置 Mozilla 的新闻和邮件服务器设置的地方。许多人更喜欢使用 Mozilla 进行所有网页浏览、邮件、新闻和 IRC 活动。

要添加账户，在 Edit, Mail & Newsgroups Account Settings 下，点击 Add Account 按钮，然后选择要添加的邮件或新闻账户。账户设置对话框如图 8.20 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_267_0.png)

**图 8.19** Mozilla 是一个便捷的综合性集成互联网客户端。

![](img/2045828cf45e5632bf056f9ca99d6755_267_1.png)

**图 8.20** 这里是访问配置信息的地方。请注意，我们必须特意取消勾选 Compose Messages in HTML Format 选项，以修复一个不理想的默认设置。

完成输入此信息后，点击 OK，你将进入新闻阅读器窗口。点击左侧窗格中的新闻服务器名称，然后在右侧窗格中选择 Subscribe to Newsgroups，开始从你的新闻服务器下载新闻组列表。随时，你都可以通过点击该窗口中的 Refresh 按钮来更新新闻组列表。

## Thunderbird 新闻客户端

与 Firefox 一起，Thunderbird 邮件和新闻客户端是 Mozilla 套件的直接继承者。Thunderbird 设计轻巧，界面简洁，它可以执行 Mozilla 新闻客户端所做的大多数事情，但它是独立于 Firefox 的应用程序。

要在 Thunderbird 中添加新账户，点击 Tools, Account Settings 并选择 Add Account。选择新闻账户并按照提示提供 Thunderbird 所需的所有信息。

当你向 Thunderbird 提供完所有相关信息后，点击 OK，你将进入 Thunderbird 的默认视图。在左侧窗格中，你将看到新的新闻服务器账户。点击它，然后选择 Manage Newsgroup Subscriptions。

## 使用 TWiki 协作

虽然 Usenet 是一个有用的交互和协作工具，但在某些情况下，基于 Web 的工具更适合你的需求。TWiki (http://TWiki.org/) 是一个基于 Web 的交互式协作工具，也可用作公告板、知识库、错误跟踪器和软件存档。

![](img/2045828cf45e5632bf056f9ca99d6755_268_0.png)

TWiki 在 Fedora 中不可用，你必须在完成简短注册后从 TWiki 网站下载它。然后你会收到电子邮件说明，解释如何从该站点下载 .zip 文件。（你使用 unzip 解压缩文件。）该程序在 GPL 许可下授权。

你可能希望首先阅读位于 http://TWiki.org/cgi-bin/view/TWiki/TWikiDocumentation 的安装说明。文档在过去一年里得到了改进，现在包括了作为非 root 用户安装 TWiki 的步骤。其中提供了关于文件所有权和文件权限的许多细节。还有一个自动安装程序——O’Wiki Installer，参考网址为 http://TWiki.org/cgi-bin/view/Code/TWikiUnixInstaller。如果你擅长 Apache 配置，这可能是一个好的方法，但安装脚本未如后文所述为 Fedora 设置适当的文件所有权和权限。

以下是关于在 Fedora 系统上顺利走过安装过程的一些简短建议（此列表假设你作为 root 用户执行安装，并且正在从 TWiki 网站阅读 TWiki 安装说明）：

- 你需要创建目录 `/home/httpd/twiki`；将 `unzip TWiki` 解压到此目录。
- 安装说明提到了文件 `/etc/httpd/httpd.conf`。在 Fedora 中，该文件位于 `/etc/httpd/conf/httpd.conf`。你只需复制并粘贴下载说明中提供的示例所示的条目。
- Fedora 中 Perl 的路径是 `/usr/bin/perl`。
- Fedora Core 以用户 `apache` 身份运行 CGI 脚本，而不是默认 TWiki 安装中假设的用户 `nobody`。你可以浏览到 `http://localhost/twiki/bin/testenv` 并阅读屏幕上显示的警告。这是一个在你的本地机器上运行的特殊脚本，帮助你诊断安装中的任何问题。消息应具体针对你的安装，任何警告都应附有如何解决问题的建议。

TWiki 安装指南建议设置权限并更改所有权。对于 Fedora，权限设置是正确的，但所有权是错误的。要更改所有权，请执行以下步骤（在每一步之后，你应该重新加载 `http://localhost/twiki/bin/testenv` 页面以检查进度）：

1. 将所有内容的组所有权更改为 `apache`，但将 `/httpd/twiki/templates` 的组所有权改回 `root`：
   ```bash
   # chgrp -r apache /home/httpd
   # chgrp -r root /home/httpd/twiki/templates
   ```
2. 记得编辑 `/home/httpd/twiki/lib/TWiki.cfg` 以反映你自己的域名，而不是 `http://your.domain.com`。
3. 将 RCS 仓库文件的所有权更改为用户 `apache`：
   ```bash
   # cd /home/httpd/twiki/data
   # perl -pi -o 's/nobody/apache:/' *.v
   ```

完成安装后，你应该拥有一个“原始”的 TWiki 安装，可以在 `http://localhost/twiki/bin/view` 查看。与任何应用程序一样，你需要进一步配置此文件以适合你的需求。TWiki 文档解释了许多可供你使用的配置选项和过程。此文档包含在你刚刚完成的 TWiki 安装中。

