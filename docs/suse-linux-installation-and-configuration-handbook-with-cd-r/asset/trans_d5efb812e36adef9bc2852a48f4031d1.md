

GIMP（GNU 图像处理程序）在很多方面都类似于 Adobe Photoshop。你可以用它来修图、创建新图像等等。它是一款非常成熟的软件，被认为是开源社区开发的最佳应用程序之一。绝对值得一看。

- **Electric Eyes**—这是一个图像查看器。它支持查看多种图像格式。
- **PostScript 文件查看器**—此程序显示 PostScript 文件。它非常强大且完整，在你需要查看 PostScript 文件时非常有用。

## Internet

此子菜单包含所有 Internet 专用的应用程序：

- **XSitecopy**—你可以用此程序将你的网站发布到远程服务器。
- **Balsa**—这是 GNOME 邮件客户端。
- **PPP 拨号实用程序**—这是 GNOME 拨号连接拨号器。你可以用它来配置系统使用调制解调器拨号到任何 ISP。
- **Talk**—这是 GNOME 版本的著名控制台 talk 命令。你可以用它与系统上的其他用户或另一系统上的用户打开聊天会话。

## Multimedia Submenu

此子菜单包含所有多媒体专用应用程序，具体如下：

- **Audio Mixer**—你可以用此应用程序控制你拥有的各种多媒体设备的音量。
- **CD Player**—你可以用此应用程序在 GNOME 中播放你的音频 CD。
- **ESD Volume Meter**—你可以用它查看 ESD、声音守护进程的频谱分析仪。

## System Submenu

此子菜单包含所有以下系统专用应用程序：

- **GnoRPM**—这是 GNOME 对 RPM 命令的前端。
- **Shut Down or Reboot**—这将关闭或重新启动机器。你必须以 root 身份使用此命令。

## Settings Submenu

此子菜单包含你在 GNOME 控制中心中的所有首选项小程序的快捷方式。你可以直接从这里启动它们，而无需使用控制中心。

## Utilities Submenu

此子菜单包含以下实用程序应用程序：

- **Eterm**—这是一个功能强大的 X 终端变体。
- **GNOME Terminal**—这是 X 终端的 GNOME 版本。它高度可配置。
- **System log monitor**—此程序只有在你以 root 身份运行它时才有用。它显示所有系统日志文件。
- **Simple calculator**—这是 GNOME 计算器，一个你会觉得有用的简单计算器。
- **Color Browser**—这个小应用程序显示你当前 X 显示屏支持的所有颜色。
- **GNOME DiskFree**—此应用程序显示仪表，显示你在所有硬盘上拥有的可用空间量。
- **Font Selector**—你可以用此应用程序浏览当前已安装的字体。
- **GNOME Search Tool**—你可以用此应用程序在硬盘上搜索文件。
- **System Info**—此应用程序显示有关你当前系统的信息。

## GNOME Tips

使用 GNOME 是使用 SuSE Linux 可以做的最有趣的事情之一。整个桌面环境设计为使用起来很有趣。随着你使用 GNOME 越多，你会发现它可以多么强大。为了让你的体验更好，我们将给你一些 GNOME 技巧。

GNOME 大量使用拖放技术。例如，如果你从任何应用程序打开了颜色选择器，你可以将颜色从中拖到面板上以更改面板的颜色。同样适用于 GNOME 终端——拖动颜色到其上会将其背景更改为该颜色。拖动颜色到终端中的任何文本上也会更改文本颜色。

当你使用背景小程序设置背景时，你仍然可以使用拖放。例如，你可以打开 GNOME 文件管理器并将图像文件拖到背景小程序上以将其用作背景。同样，当你将图像拖到面板上时，它将被用作面板的背景。

大多数符合 GNOME 的应用程序都接受拖放。你可以将文件从文件管理器拖到任何 GNOME 应用程序上以使其打开它。例如，将电子表格文件拖到 Gnumeric 上会打开它。这种拖放与 Motif 兼容，这意味着你可以将链接拖到 Netscape 上，它会打开它们。它也适用于大多数 Motif 应用程序。

你甚至可以在两个正在运行的 GNOME 文件管理器实例之间使用拖放。只需将文件或文件夹从一个拖到另一个即可执行复制操作。

你也可以拖放目录。你可以将目录从 GNOME 文件管理器拖出并放在面板上。这将创建一个新菜单，让你轻松访问该目录中的文件。

如果你使用 X 多媒体系统（xmms），你可以将文件和目录从文件管理器拖到它上面以将它们添加到播放列表中。

你应该更频繁地使用 GNOME 终端，因为它非常强大。如果终端中有任何文本包含 URL，当你将鼠标指针移到其上时，它们将被下划线标出。如果你按下键盘上的 Ctrl 按钮并单击 URL，Netscape 将被启动以打开此 URL。

如果你的 GNOME 会话无法正常启动，只需在登录 GNOME 时按下 Ctrl+Shift。GNOME 然后会询问你是否要使用默认程序启动或删除所有用户设置。使用默认程序启动将以干净的会话启动你，但仍保留你的设置。如果你选择删除所有用户设置，GNOME 将恢复为默认状态，你将丢失所有配置。

## Troubleshooting GNOME

### I can't find my panel.

确保它没有被隐藏。寻找屏幕边缘的小箭头。如果你找到任何，点击一个以恢复面板。如果你找不到任何，那么面板可能已崩溃；只需打开一个终端并输入以下命令：

```
$ nohup panel&
```

这将再次启动面板并使其在你关闭终端后仍保持运行。

### I can't change the GNOME menu using the menu editor.

可以，你只是不能更改默认菜单，因为你没有权限这样做。你可以添加到用户菜单部分，而不是系统菜单。要添加到系统菜单，你必须以 root 身份运行 GNOME。更改将反映在所有用户上。

### How can I stop GNOME from reloading my session?

如果你的 GNOME 会话无法正常启动，只需在登录 GNOME 时按下 Ctrl+Shift。GNOME 然后会询问你是否要使用默认程序启动或删除所有用户设置。使用默认程序启动将以干净的会话启动你，但仍保留你的设置。如果你选择删除所有用户设置，GNOME 将恢复为默认状态，你将丢失所有配置。

## Installing and Configuring StarOffice

### In this chapter

- StarDivision and Sun Microsystems—History and License 502
- StarOffice Features 502
- Installing StarOffice 505
- Installing New Printers 508
- Installing New Fonts 510
- Setting Up StarOffice as a Web Browser 511
- Setting Up StarOffice as an Email Client 516
- Setting Up StarOffice as a News Reader 517
- StarOffice General Configuration 518
- Troubleshooting 519

## StarDivision and Sun Microsystems--History and License

StarOffice 是一个功能齐全的办公套件应用程序。它包括常见的办公应用程序，如文字处理器、电子表格、演示制作器、图形设计实用程序、数据库、电子邮件客户端、新闻客户端和调度程序。StarOffice 最令人印象深刻的事情之一是它有多个平台的版本。你可以找到适用于 MS Windows、IBM OS/2、Solaris、Linux 和 Java 的版本。StarOffice 由一家名为 StarDivision 的德国公司开发。该公司为个人使用免费提供 StarOffice；如果套件用于商业用途，则必须购买商业许可证。

最近 Sun Microsystems 收购了 StarDivision 并免费赠送 StarOffice 给所有平台和所有类型的用途，商业或个人。你可以直接从 Sun 下载它，也可以让他们以少量费用通过 CD 连同手册一起寄给你。SuSE Linux 6.3（完整版）附带最新版本的 StarOffice，版本 5.1a。StarOffice 真的是一款很棒的软件，而且它包含在 SuSE 中使其物超所值。

在收购 StarOffice 后不久，Sun Microsystems 启动了 StarOffice NOW 计划。这是一个面向合作伙伴和其他有兴趣向其订阅者、客户或学生提供 StarOffice 的第三方计划。你可以从 Sun Microsystems 网页 http://www.sun.com/products/staroffice/staroffice now/ 访问此计划。

## StarOffice Features

StarOffice 不仅作为办公套件，而且作为集成桌面环境。通过使用 StarOffice，你可以完成日常业务工作，而无需使用任何其他应用程序或文件管理器。这是因为 StarOffice 本身就可以作为文件管理器，同时它具有满足大多数家庭和商业用户需求的能力。

通过使用 StarOffice，你可以轻松编辑和管理你的文档。随 SuSE Linux 提供的完整套件包含 StarOffice 的所有模块。模块是文件管理器、文字处理器、电子表格编辑器、演示设计器等等。

### StarOffice Modules

StarOffice 是一个非常完整的办公套件。它建立在“在一个地方完成所有事情”的理念之上。其背后的想法是，与其为文字处理有一个单独的应用程序，为电子表格编辑有另一个应用程序，你可以将它们全部放在一个环境下，即 StarOffice。

