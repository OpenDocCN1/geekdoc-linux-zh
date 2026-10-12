

![](img/774d40fd20903495c5cd00e2efad3f33_262_0.png)

**图 8.18** KNode 新闻阅读器；设置快速且简单。它非常适合纯文本新闻组。

## Mozilla 新闻客户端

Mozilla 网页浏览器支持图形化的 Usenet 新闻阅读以及网页浏览。在 Fedora Core 系统上安装众多新闻阅读客户端可为用户提供丰富的选择以及培养偏好的机会。然而在某些情况下，这会使管理员追踪和修复客户端安全漏洞的任务变得复杂。使用 Mozilla 可以通过提供一个集网页浏览、电子邮件、文件传输和新闻阅读功能于一体的客户端来简化这一任务。基于这些原因，你可能选择使用 Mozilla 作为浏览器、电子邮件客户端和新闻客户端。Mozilla 是 Fedora Core 的默认浏览器。

要开始使用 Mozilla 阅读新闻，启动 Mozilla 并选择 Window（窗口）, Mail and Newsgroups（邮件和新闻组）；将显示如图 8.19 所示的窗口。菜单 Edit（编辑）, Mail & Newsgroups Account Settings（邮件和新闻组账户设置）是配置 Mozilla 的新闻和邮件服务器设置的地方。许多人喜欢使用 Mozilla 进行所有的网页浏览、邮件、新闻和 IRC。

要添加账户，在 Edit（编辑）, Mail & Newsgroups Account Settings（邮件和新闻组账户设置）下，点击“添加账户”按钮，并选择要添加的邮件或新闻账户。账户设置对话框如图 8.20 所示。

完成此信息输入后，点击 OK（确定），您将到达新闻客户端窗口。点击左侧窗格中的新闻服务器名称，然后在右侧窗格中选择“订阅新闻组”以开始从新闻服务器下载新闻组列表。随时可以通过点击该窗口中的“刷新”按钮来更新新闻组列表。

![](img/774d40fd20903495c5cd00e2efad3f33_263_0.png)

![](img/774d40fd20903495c5cd00e2efad3f33_263_1.png)

## Thunderbird 新闻客户端

与 Firefox 一样，Thunderbird 邮件和新闻客户端是 Mozilla 套件的直接后代。Thunderbird 设计得轻量级且界面简洁，它可以执行 Mozilla 新闻客户端能做的许多功能，但它是一个独立于 Firefox 的应用程序。

要在 Thunderbird 中添加新账户，点击 Tools（工具）, Account Settings（账户设置）并选择“添加账户”。选择新闻账户并按照提示提供 Thunderbird 所需的所有信息。

在您向 Thunderbird 提供完所有相关信息后，点击 OK（确定），您将到达 Thunderbird 的默认视图。在左侧窗格中，您将看到新的新闻服务器账户。点击它，然后选择“管理新闻组订阅”。

## 使用 TWiki 进行协作

虽然 Usenet 是有用的交互和协作工具，但在某些情况下，基于网页的工具更适合您的需求。TWiki ([http://TWiki.org/](http://TWiki.org/)) 是一个基于网页的交互协作工具，也可以用作公告板、知识库、缺陷跟踪器和软件归档。

**提示**

您可以在公司主页上查看 TWiki 成功案例，以获取探索 TWiki 的鼓励。您还可以探索这个与 Linux 相关的公共 TWiki 站点 ([http://TWiki.org/cgi-bin/view/WikiLearn/WebHome/](http://TWiki.org/cgi-bin/view/WikiLearn/WebHome/))。

Fedora 不提供 TWiki，您必须在完成简短注册后从 TWiki 网站下载它。然后您会收到电子邮件说明，解释如何从该站点下载 .zip 文件。（您使用 `unzip` 来提取文件。）该程序根据 GPL 协议授权。

您可能希望首先阅读位于 [http://TWiki.org/cgi-bin/view/TWiki/TWikiDocumentation](http://TWiki.org/cgi-bin/view/TWiki/TWikiDocumentation) 的安装说明。文档在过去一年中有所改进，现在包括作为非 root 用户安装 TWiki 的步骤。它提供了关于文件所有权和文件权限的许多细节。还有一个自动安装程序——O'Wiki Installer——在 [http://TWiki.org/cgi-bin/view/Code/TWikiUnixInstaller](http://TWiki.org/cgi-bin/view/Code/TWikiUnixInstaller) 中提及。如果您擅长 Apache 配置，这可能是一个好的方法，但安装脚本没有为 Fedora 设置适当的文件所有权和权限，正如后文所述。

以下是在 Fedora 系统上顺利完成安装过程的简短建议列表（此列表假设您以 root 用户身份执行安装，并正在从 TWiki 网站阅读 TWiki 安装说明）：

- 您需要创建目录 `/home/httpd/twiki`；将 TWiki 解压到此目录中。
- 安装说明提到了文件 `/etc/httpd/httpd.conf`。对于 Fedora，该文件位于 `/etc/httpd/conf/httpd.conf`。您只需复制并粘贴下载说明中提供的示例中显示的条目。
- Fedora 中 Perl 的路径是 `/usr/bin/perl`。
- Fedora Core 以用户 apache 运行 CGI 脚本，而不是默认 TWiki 安装中假设的用户 nobody。您可以浏览到 [http://localhost/twiki/bin/testenv](http://localhost/twiki/bin/testenv) 并阅读屏幕上显示的警告。这是一个在您本地机器上运行的特殊脚本，有助于诊断安装中的任何问题。消息应针对您的安装情况，任何警告都应附带关于如何修复问题的建议。

TWiki 安装说明建议设置权限和更改所有权。对于 Fedora，权限设置正确，但所有权错误。要更改所有权，请实施以下步骤（每个步骤之后，您应该重新加载 [http://localhost/twiki/bin/testenv](http://localhost/twiki/bin/testenv) 页面以检查您的进度）：

1. 将 everything 的组所有权更改为 apache，但将 /httpd/twiki/templates 的组所有权改回 root：
   ```
   # chgrp -r apache /home/httpd
   # chgrp -r root /home/httpd/twiki/templates
   ```
2. 记得编辑 /home/httpd/twiki/lib/TWiki.cfg 以反映您自己的域名，而不是 http://your.domain.com。
3. 将 RCS 仓库文件的所有权更改为用户 apache：
   ```
   # cd /home/httpd/twiki/data
   # perl -pi -e 's/nobody/apache/' */*,v
   ```

完成安装后，您应该拥有一个“virgin”（未使用的/原始的）TWiki 安装，可以在 [http://localhost/twiki/bin/view](http://localhost/twiki/bin/view) 查看。与任何应用程序一样，您需要进一步配置此文件以适合您的需求。TWiki 文档解释了许多可供您使用的配置选项和过程。此文档包含在刚刚完成的 TWiki 安装中。

## 互联网中继聊天

如 RFC 2812 和 RFC 2813 所述，IRC 协议用于文本会议。与邮件和新闻一样，IRC 使用客户端/服务器模型。虽然个人建立 IRC 服务器很罕见，但可以做到。大多数人使用公共 IRC 服务器并使用 IRC 客户端访问它们。

Fedora Core 提供许多图形 IRC 客户端，包括 X-Chat、licq-kde 和 Mozilla-chat，但 Fedora Core 没有默认的聊天客户端。Fedora Core Linux 还为那些回避 X 的人提供控制台客户端 epic 和 licq。如果您还没有最喜欢的，您应该尝试它们所有。

**注意**

当您作为 root 用户时，您永远不应使用 IRC 客户端。由于潜在的安全问题，最好专门为 IRC 创建一个特殊用户。要以这种方式使用 X-Chat，您打开一个终端窗口，使用 su 切换到您的 IRC 用户，并启动 xchat 客户端。

X-Chat 是一个流行的 IRC 客户端，也是本章示例中使用的客户端。X-Chat 的 HTML 文档位于 `/usr/share/docs/xchat`。在开始之前阅读它们是个好主意，因为它们包括介绍并涵盖一些 IRC 基础知识。要启动 X-Chat 客户端，从 Extras（附加）菜单下的 Internet（互联网）菜单中选择“IRC 客户端”项，或者您可以从命令行启动它，如下所示：

```
$ xchat &
```

X-Chat 应用程序允许您为自己分配最多三个昵称。您还可以指定您的真实姓名和用户名。由于许多人选择不使用真实姓名进行 IRC 聊天，您可以自由地在提供的任何空格中输入您想要的任何姓名。您可以选择多个昵称；您可能因一个名字被禁止进入 IRC 频道，然后可以使用另一个名字重新加入。如果这看起来对您来说略显幼稚，您开始了解许多 IRC 频道上的行为类型。

当打开主 X-Chat 屏幕时，会出现一个 IRC 服务器列表，如图 8.21 所示。通过双击选择一个服务器后，您可以通过选择 Window（窗口）, List Window（列表窗口）来查看该服务器上可用的频道列表。X-Chat 频道列表窗口将出现。在该窗口中，您可以选择加入以感兴趣主题为特色的频道。要加入频道，请双击它。

![](img/774d40fd20903495c5cd00e2efad3f33_266_0.png)

**图 8.21** 主 X-Chat 屏幕显示一个可用的公共服务器列表供选择。

