
程序。Microsoft Office 套件中几乎任何实用程序在 StarOffice 的 Linux 移植版中也可用。最近发布的 StarOffice 5.2 允许用户像使用 Microsoft Access 一样创建数据库。

StarOffice 通过精简部分功能来减小软件包体积。整个套件经过 tar 打包和压缩后，可从互联网下载。与最新 Microsoft Office 套件完整安装所需的 500 多兆字节数据相比，StarOffice 完全压缩后仅略多于 90 兆字节，安装后占用空间不到 200 兆字节。它也是自包含的，意味着它不会更改任何配置文件，而是在其自身目录内运行。StarOffice 加载自己的一组库和配置文件，以在所有平台（无论是 Windows 还是 Linux）上保持一致的外观和感受。这导致了我在使用最新发布的 StarOffice 时发现的少数缺点之一：速度并非其最大优势。如果你在一台配备 500 兆赫兹 Athlon 处理器和 128 兆字节内存的计算机上新重启后启动程序，StarOffice 需要 30 到 45 秒才能完全就绪。但该程序提供的功能——将办公管理带到 Linux 平台——其重要性远超速度问题。

## 下载和安装 StarOffice

你可以从 Sun 网站的一个子目录获取 StarOffice：http://www.sun.com/staroffice/。Sun 要求你在下载前注册，但作为回报，他们会向你通知升级信息和额外的 Sun 程序。注册后，你可以选择下载整个程序（即使对于带宽充裕的高速机器来说也是一项不小的工作量），或者购买该程序的 CD 副本。我建议使用几美元（大约低于 10.00 美元）让 Sun 给你邮寄一份。这样你只需拥有单一副本，即可安装在任意多台机器上。此外，你也不必使用 FTP 将大的 tar 包文件传输到不同的服务器。

安装 StarOffice 的最佳方法是首先创建你希望安装程序的默认目录。确保你或运行程序的人拥有该目录的所有权，以免安装例程遇到重大的权限问题并中止安装。我选择在一个较大的分区中创建一个目录：

```
# mkdir /usr/local/office52
# chown -R <username> /usr/local/office52
# chgrp -R <username> /usr/local/office52
```

接下来，将下载的文件解压到临时目录，例如 /tmp，或另一个你拥有正确权限的目录。StarOffice 应该会创建一个名为 so52inst 的额外安装目录。查找一个名为 setup 的文件：

```
# cd /tmp/so52inst/
# ./setup
```

以你自己或相应用户的身份运行此命令会启动图形安装窗口。系统将提示你填写几个表单，其中包含有关你个人信息的以及你的互联网连接配置的信息。完成所有字段后，StarOffice 开始安装例程，根据计算机速度的不同，此任务只需几分钟。你无需对系统进行进一步调整。

如果你将 StarOffice 的目录路径添加到全局 /etc/profile 文件或每个用户的单独 .bash_profile 中，你就可以从命令行的单一入口点启动 StarOffice：

```
PATH="${PATH}:/usr/X11R6/bin:/usr/local/Office5.2"
```

运行命令 *source* /etc/profile 以启用设置。StarOffice 通过简单命令 *soffice* 启动。为了使你的系统在互联网上完全正常工作，StarOffice 会提示你填写一些关于你的 POP3 服务器、用户名以及你经常访问以获取连接的服务器名称的表单。考虑到 StarOffice 在与 Microsoft 系统及其他以 Microsoft 为中心的用户进行界面交互和信息交换方面所赋予的便捷性和自由度，填写这些表单仍是一项相对较小的任务。

图 12.6 展示了一个常规文本文档的外观以及用于选择附加选项的各种菜单。StarOffice 高度模拟 Microsoft 的功能，以至于它和开始按钮一样，允许你将整个 Linux 桌面集成到 StarOffice 显示中。这创建了一个类似 Windows 的显示界面。你实际上可以通过指向和点击来浏览 StarOffice 集成桌面下的程序和目录。此外，如果系统上已安装 KDE，StarOffice 会检测到该窗口管理器，并在 KDE 桌面上放置一个链接，同时也将 *Fav* 或将其所有 KDE 程序纳入其自身的开始按钮中。这两个系统的平滑集成部分归功于 StarOffice 自身作为一家德国公司的背景，这与 KDE 的历史及德国开发人员的情况类似。

![](img/a0884097af3186d9b4f616aaa3f065b0_453_0.png)

图 12.6

*在 Linux 下运行的 StarOffice 程序。*

## 完善 Linux 版 WordPerfect

安装 WordPerfect 用于 Linux 操作系统的过程比 StarOffice 略显复杂，这仅仅是因为 WordPerfect 的 tar 压缩文件不像普通的 Linux 文件。尽管其体积不到 25 兆字节有助于提高其下载的吸引力，但虽然名为 GUILG00.GZ，它不仅经过 gzip 压缩，还经过了 tar 打包。

### 注意

> WordPerfect Office 2000 for Linux 的用户个人版可免费下载。应提及的是，WordPerfect Office 2000 的商业版本也适用于 Linux。它具有与 Windows 版本发布的所有相同功能和应用程序。由于其成本以及大多数 Linux 用户对免费软件的偏好，我将重点关注可从互联网下载的 WordPerfect 个人版。

在执行标准安装之前，请将该文件放在其自己的目录中，然后运行标准命令：

```
# gunzip -c GUI\LG00.GZ \|tar xvf -
```

一旦所有文件解压完毕，只需执行 Runme 文件如下：

```
# ./Runme
```

请确保你也处于 X Window 环境中，因为 Runme 文件随后将启动图形安装菜单。一旦 WordPerfect 程序完全安装，你可以通过输入命令 $HOME/wpbin/xwp 来启动它，其中 $HOME 是你安装 WordPerfect 的位置。

### 注意

> 在 Corel 宣布支持 Linux 并将 WordPerfect 放置在互联网上供下载后不久，头 24 小时内收到了数千条对该程序的请求。截至目前，Linux 版 WordPerfect 的下载量已超过一百万次。

WordPerfect 的界面与 Windows 版本非常相似。尽管其显示依赖于较旧的 Motif 库（因此具有独特的外观以及使用不同的单选按钮和下拉菜单项），但它仍然具有许多在商业版中发现的相同选项。图 12.7 展示了 WordPerfect 显示默认文本文档的情形。请注意程序窗口和文本窗口的分离。

Linux 版 WordPerfect 个人版，即可供下载的版本，缺少一些项目，包括模板和额外的宏，这些仅能在商业版中获得。因此，购买完整版可能是值得的。最新的 Corel Linux 办公套件显示出巨大的潜力，不仅为 Linux 用户提供完整的 WordPerfect，还提供 Presentations 和 QuattroPro。

WordPerfect 为你的系统中的多个用户提供附加功能。虽然你可以在个人版中实现相同效果，但商业版允许多个用户从 *dumb terminals*（哑终端）或硬盘空间极少甚至没有、依赖网络获取程序的机器登录。在联网的 Linux 机器或哑终端上，WordPerfect 可以在 Linux 的所有版本上运行，每个版本在其自己的会话下运行。如果你希望在联网系统（如大型公司办公室或教育环境）中保留一定的标准化，功能齐全的 WordPerfect Office 200 Suite 是推荐的程序。

