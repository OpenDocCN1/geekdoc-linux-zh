
该发行版最初使用一个大小写混合的名称：SuSE。不过现在，该发行版的名称全部用大写字母书写：SUSE。最终，SUSE 作为缩写的起源很可能会被遗忘，它将被视为一个不代表任何含义的名称。

## 如何找到我的 SUSE Linux 问题的答案？

你可以在许多在线资源中找到有关 SUSE Linux 的有用信息。从 www.suse.com 开始。从该网页的菜单中选择“支持→知识库”。然后选择 SUSE 作为产品，输入一个或多个关键字，并单击“立即搜索”。

如果你在 www.suse.com 上没有找到答案，请尝试通过 Google Groups 上的“高级群组搜索”搜索新闻组：

```
http://groups.google.com/advanced_group_search?hl=en
```

输入你喜欢的搜索词。你甚至可以设置要搜索的文章的日期范围。

如果新闻组搜索没有给你答案，请访问 Google 的 Linux 搜索页面进行 Linux 搜索，地址为：

```
http://www.google.com/linux
```

输入搜索词并按 Enter，或单击“Google 搜索”。要获得 SUSE 相关的答案，请在搜索词之外再输入 **SUSE**。

如果你还想搜索 SUSE 邮件列表，请访问 www.google.com，输入 **lists:suse:lists.suse.com**，后面再加上搜索词。例如，要搜索 DVD movie player，你应在搜索框中输入 **lists:suse:lists.suse.com DVD movie player**。

这些在线搜索之一应该能让你找到问题的答案。如果没有，你可以在第 22 章列出的某个论坛（如 www.suseforums.com）上发布问题。

## 下一个 SUSE Linux 版本何时发布？

每个人都想知道这个问题的答案，包括我自己！当然，正确的答案是：“无论 Novell 何时决定发布它。”不过，根据过去的历史，新的 SUSE 版本似乎大约每六个月发布一次。现在 SUSE 是通过 Novell 赞助的 openSUSE 项目开发的，你可以在 www.opensuse.org/index.php/Roadmap 找到 SUSE 的最新里程碑。

## 我可以从互联网上获取 SUSE Linux 的 ISO 文件吗？

在 10.0 版本之前，你必须在 SUSE Linux 新版本发布后等待数周，Novell 才会免费提供该版本的 ISO 镜像文件。随着 Novell 于 2005 年 8 月赞助并建立了 openSUSE 项目，最新版 SUSE Linux 的 ISO 文件始终可以从 www.opensuse.org/index.php/Download 和互联网上的许多镜像站点获取。

## 如何执行 SUSE Linux 的 FTP 安装？

假设你手头有这本书，但更新的 SUSE Linux 版本现在已经可以通过 FTP 安装。你可以轻松地执行 FTP 安装，而不是安装随书附带的 CD 或 DVD 上的版本。

要从众多镜像最新 SUSE 发行版的 FTP 服务器之一安装 SUSE Linux，你必须执行以下主要步骤：

- 1. 从 FTP 服务器下载 SUSE 启动镜像，并用该镜像刻录一张 CD。
- 2. 记下 FTP 服务器的 IP 地址以及 SUSE 发行版文件所在的目录。
- 3. 用启动 CD 启动 PC，然后在启动提示符下输入一条命令，从你通过其 IP 地址指定的 FTP 服务器开始进行 FTP 安装。

如果你有一台运行 Windows 且具有高速 Internet 连接的 PC，你可以用那台 PC 下载启动镜像并刻录启动 CD。你也可以用那台 PC 查找 FTP 服务器的 IP 地址。

你还需要知道 PC 中安装的网卡名称，因为在启动 SUSE FTP 安装之前，你必须手动加载驱动程序。当你下载 SUSE 安装程序的启动镜像时，可以找到 FTP 服务器的 IP 地址。我将在本节中解释这些步骤。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_331_0.png)

通过典型的宽带 DSL 或电缆调制解调器连接 Internet，从 FTP 服务器安装 SUSE 可能需要两个小时或更长时间。请按照以下步骤，通过 Internet 从 FTP 服务器执行 FTP 安装。

- 1. **使用 Web 浏览器打开位于 www.suse.com/us/private/download/ftp/intl_mirrors.html 的 FTP 服务器列表，找到一个离你最近且标记为“complete”的 FTP 服务器（表示该服务器拥有完整的 SUSE 发行版和所有更新）。**

    服务器列表按国家/地区组织，包含 FTP 和 HTTP（Web）服务器。前往离你最近的国家/地区，并选择离你最近且标记为“complete”的服务器。

    ![](img/b7e91b81e0d84c8a5261ee14a48991b2_332_0.png)

    在终端窗口中，输入 **ping**，后面跟上 FTP 服务器的名称（例如，**mirror.mcs.anl.gov**）。接下来，你会在下一行看到该 FTP 服务器的 IP 地址（例如，140.221.37.130）。记下该 IP 地址以备后用。如果你是在 Microsoft Windows 中执行此步骤，同样使用 ping 命令，但要在“命令提示符”窗口中输入该命令（选择“开始→运行”，输入 **cmd**，然后按 Enter）。

- 2. **单击你的 FTP 服务器链接，找到包含 boot.iso 文件的目录——这就是 SUSE 安装程序的启动镜像。**

    目录取决于 SUSE 的版本。例如，对于 10.0 版本，**boot.iso** 文件位于 FTP 服务器的 **pub/suse/i386/10.0/boot/** 目录中。该文件有几十兆字节大小。

- 3. **下载 boot.iso 文件并保存。**

- 4. **将 boot.iso 镜像刻录到 CD 上。**

    使用 PC 的 CD 刻录应用程序刻录名为 **boot.iso** 的 ISO 镜像。

- 5. **前往你想要执行 SUSE FTP 安装的 PC，插入启动 CD，然后重新启动 PC。**

    如果你的 PC 未设置为从 CD/DVD 驱动器启动，你必须进入 SETUP（在 PC 启动时按 F2 等按键）并更改启动设备的顺序。

    PC 重新启动，片刻后，一个文本屏幕会显示带有多个选项的屏幕。使用箭头键在列表项和屏幕上的按钮之间移动。

- 6. **使用箭头键选择“安装”选项并按 Enter。**

    此步骤加载 Linux 内核并运行安装程序。在检测并初始化硬件后，安装程序显示一条消息，说明它无法找到 SUSE Linux 安装源，正在激活手动设置程序。这是正常现象，你应按 Enter 继续。安装程序会显示一个语言列表。

- 7. **选择语言并按 Enter。**

    安装程序显示键盘映射列表——即键盘的依赖于语言的布局。

- 8. **选择键盘语言并按 Enter。**

    安装程序显示主菜单。

- 9. **使用箭头键选择“开始安装/系统”并按 Enter。在下一个屏幕上，选择“开始安装/更新”并按 Enter。**

    安装程序显示源介质列表——你可以在此处指定安装程序从哪里找到执行安装所需的文件。

- 10. **选择“网络”作为源介质并按 Enter。**

    安装程序提示你选择网络协议。

- 11. **选择“FTP”作为网络协议并按 Enter。**

    一个对话框提示你确定是否使用动态主机配置协议（DHCP）自动配置网络。如果你的网络和大多数网络一样使用 DHCP，请选择“是”并按 Enter。否则，你必须在此步骤中输入 IP 地址和名称服务器的 IP 地址。然后安装程序会提示输入 FTP 服务器的 IP 地址。

- 12. **输入你在步骤 1 中查到的 FTP 服务器的 IP 地址（例如，为 FTP 服务器 mirror.mcs.anl.gov 输入 140.221.37.130）。**

    安装程序会询问你是否要使用用户名和密码连接到 FTP 服务器。由于 FTP 服务器支持匿名 FTP——这意味着任何人都可以使用用户名 anonymous 登录——请选择“否”并按 Enter。安装程序还会询问你是否要使用 HTTP 代理。除非你的 PC 位于代理服务器之后（在某些组织中可能如此），否则请选择“否”并按 Enter。然后安装程序会提示输入 SUSE 文件所在目录的名称。

- 13. **输入 FTP 服务器上 SUSE Linux 文件所在目录的名称并按 Enter。**

    目录名称应是你在步骤 1 中找到 `boot.iso` 文件的位置的父目录。例如，如果 `boot.iso` 文件位于 `/pub/suse/i386/10.0/boot/`，你应输入 **pub/suse/i386/10.0/** 并按 Enter。

    安装程序会显示一条消息，通知你正在将数据加载到 ramdisk（ramdisk 是指充当硬盘驱动器的内存区域）。当安装程序完成数据下载后，YaST（即 SUSE 安装程序的名称）安装程序将启动并显示其初始 GUI 屏幕。

