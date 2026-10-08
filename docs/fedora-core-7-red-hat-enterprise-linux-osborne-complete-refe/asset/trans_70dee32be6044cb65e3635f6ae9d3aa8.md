

Xine 是一款适用于 Linux/Unix 系统多用途视频播放器，能够播放视频、DVD 和音频光盘。更多信息请访问 xinehq.de。Xine 提供源代码形式，你需要自行编译和安装，不过你也可以从 freshrpms.net 下载 RPM 二进制文件。

Totem 随 Fedora 一起安装，是一个基于 Xine 并使用 GStreamer 的 GNOME 电影播放器。为了扩展 Totem 的功能，你需要安装额外的 GStreamer 插件。

PowerDVD 提供 Linux 版本的商业 DVD 播放器（www.cyberlink.com）。

如需 DVD 转码和 DivX 支持，请查看 DVD::rip 项目。www.exit1.org/dvdrip。

kdtv KDE 电视观看器

tvtime 电视观看器

额外的编解码器支持由 ffmpeg 和 x264 提供。x264 编解码器是 Videolan 开发的高清 H.264 编解码器的开源版本。

托管于 SourceForge 上的开源软件均不对商业 DVD 进行 CSS 解密。不过，你可以下载并安装 libdvdcsc 库，该库通过将 DVD 视为块设备来规避 CSS 解密，使你能够使用任意 DVD 播放器播放商业 DVD。它还提供了无区域限制的访问。请记住，在要求 DVD 播放器拥有 CSS 许可证的某些国家，这样做可能并不合法。

> 注意 要在 Red Hat 和 Fedora 上播放 DivX 媒体，请使用位于 labs.divx.com/DivXLinuxCodec 的 Divx for Linux 编解码器。

最初，这些播放器中的许多并不支持 DVD 菜单。借助 libdvdnav 和 libdvbplay 库，这些播放器现在具备完整的 DVD 菜单支持。libdvbread 库提供基本的 DVD 接口支持，例如读取 IFO 文件。你可以从 freshrpms.net 下载这些软件的 RPM 二进制文件。

## 电视播放器

linuxtv.org 网站提供了关于 DVD、数字视频广播（DVB）和多播的详细说明。该网站还提供许多 Linux 视频应用程序的下载。Fedora 的主要电视播放器是 tvtime，它兼容许多常见的视频采集卡，依赖于为这些卡上的电视调谐器芯片（如 Conexant 芯片）开发的驱动程序。它仅能显示电视图像。它没有录制或文件播放功能。请查看 tvtime.sourceforge.net 获取更多信息。对于 KDE，有几个视频应用程序可用或正在开发中，包括 kdetr。请查看 www.kde-apps.org 下载。对于基于 Gnome 的播放器，请查看 www.gnomefiles.org。

## Linux 上的 DivX 和 Xvid

DivX 是一种商业视频压缩技术（个人使用免费），用于以相对较小的文件大小提供 DVD 质量的视频。你可以将 60 分钟的 DVD 视频压缩到约 400 MB，同时保持非常高质量。DivX 基于 MPEG-4 压缩格式，而 DVD 是 MPEG-2。你可以从 labs.divx.com/DivXLinuxCodec 免费下载 DivX 的 Linux 版本。你需要手动安装包。如果你使用 Firefox 下载，可以选择直接解包该存档文件。

与其试图让 DivX 正常工作，你只需使用 DivX 的开源版本，即 Xvid 即可。大多数 DivX 文件可以使用 Xvid 运行。Xvid 是一个完全独立的开源项目，但与 DivX 文件兼容。Fedora 的二进制 RPM 版本可从 rpm.livna.org 和 freshrpms.net 获取。如果你已经配置了这些仓库以供系统中的 Yum 使用，你可以直接使用 Pirut 或 yum 命令安装 xvid 包。

```
yum install xvid
```

你也可以从 www.xvid.org 下载 Xvid 源代码。如果你使用 Firefox 下载，将自动获得下载原始压缩 .tar.bz 文件或打开 File Roller 并立即解压缩文件的选项。解压后，你可以编译源代码并安装编解码器。Linux 版本在 build/generic 子目录中构建，使用 ./configure、make 和 make install 命令（参见第 4 章）。打开终端窗口，使用 cd 命令切换到该目录，然后运行这些命令。

# 第 13 章
# 邮件和新闻客户端

你的 Linux 系统支持广泛的电子邮件和新闻客户端。邮件客户端使你能够与系统上或其他通过网络访问的其他用户发送和接收消息。新闻客户端允许你阅读发布在新闻组中的文章和消息，这些新闻组对所有用户开放访问。本章回顾了随 Fedora Linux 安装的邮件和新闻客户端。

## 邮件客户端

你可以通过多种方式发送和接收电子邮件消息，具体取决于你使用的邮件客户端类型。尽管所有电子邮件工具执行相同的接收和发送消息的基本任务，但它们往往具有不同的界面。一些邮件客户端在桌面环境中运行，如 KDE 或 GNOME。其他则在任何 X 窗口系统管理器上运行。几种流行的邮件客户端被设计为使用基于屏幕的界面，并且只能从命令行启动。其他传统邮件客户端专为命令行界面开发，这要求你在单行命令线中输入命令。此处描述的大多数邮件客户端都包含在标准 Linux 发行版中，并以标准 RPM 包的形式提供，便于安装。对于基于 Web 的 Internet 邮件服务，如 Hotmail、Google 和 Yahoo，你使用 Web 浏览器而不是邮件客户端来访问这些服务提供的邮件账户。表 13-1 列出了几种流行的 Linux 邮件客户端。邮件通过邮件传输代理在目的地之间传输。Sendmail、Exim 和 Smail 从 Internet 或网络上其他站点的目的地发送和接收邮件（参见第 25 章）。为了通过 Internet 发送邮件，它们使用简单邮件传输协议（SMTP）。大多数 Linux 发行版，包括 Fedora，会自动为你安装并本地配置 Sendmail。在启动系统并配置好网络连接后，你可以通过 Internet 发送和接收消息。

你可以使用相同的标准签名信息（例如你的姓名、Internet 地址或多个地址、或告别语）为你的电子邮件消息签名。自动将你的签名信息添加到消息中是有帮助的。为此，你需要在家庭目录中创建一个签名文件并在其中输入你的签名信息。签名文件是一个标准文本文件，你可以使用任何文本编辑器进行编辑。像 KMail 这样的邮件客户端允许你指定一个文件作为你的签名文件。其他如 Mail 这样的客户端则期望签名文件命名为 .signature。

| 邮件客户端 | 描述 |
| :--- | :--- |
| Kontact (KMail, KAddressbook, KOrganizer) | 包含 K Desktop 邮件客户端 KMail；集成的邮件、地址簿和日程表 |
| Evolution | 电子邮件客户端 |
| Balsa | GNOME 邮件客户端 |
| Thunderbird | Mozilla 组独立邮件客户端和新闻阅读器 |
| Netscape | 基于 Web 浏览器的邮件客户端 |
| GNU Emacs 和 X Emacs | Emacs 邮件客户端 |
| Mutt | 基于屏幕的邮件客户端 |
| Sylpheed | Gtk 邮件和新闻客户端 |
| Mail | 原始 Unix 基于命令行的邮件客户端 |
| SquirrelMail | 基于 Web 的邮件客户端 |

表 13-1 Linux 邮件客户端

## MIME

MIME（该术语代表 Multipurpose Internet Mail Extensions，即多用途 Internet 邮件扩展）用于使邮件客户端能够发送和接收多媒体文件以及使用不同字符集（如不同语言的字符集）的文件。多媒体文件可以是图像、声音片段甚至视频。支持 MIME 的邮件客户端可以自动将二进制文件作为附件发送到消息中。支持 MIME 的邮件客户端维护一个名为 mailcap 的文件，该文件将不同类型的 MIME 消息映射到系统中可以查看或显示它们的程序。例如，图像文件将映射到可以显示图像的应用程序。然后你的邮件客户端可以运行该程序来显示图像消息。声音文件将映射到可以在你的扬声器上播放声音文件的应用程序。大多数邮件客户端内置 MIME 功能并使用它们自己版本的 mailcap 文件。其他则使用名为 metainfo 的程序来添加 MIME 支持。MIME 不仅用于邮件客户端。如第 6 章和第 7 章所述，KDE 和 GNOME 文件管理器都使用 MIME 将文件映射到特定应用程序，以便你可以直接从文件启动该应用程序。

## mime.types 文件

应用程序通过 mailcap 和 mime.types 文件与二进制文件关联。mime.types 文件定义不同的 MIME 类型，将 MIME 类型与特定应用程序关联。然后 mailcap 文件将每个 MIME 类型与特定应用程序关联。你的系统维护自己的 MIME 类型文件，通常是 /etc/mime.types。

MIME 类型文件中的条目将应用程序的 MIME 类型和可能的子类型与用于在给定类型应用程序上运行的文件的一组可能文件扩展名关联起来。MIME 类型通常由子类型进一步限定，子类型与主要类型之间用斜杠分隔。例如，MIME 类型 image 可以有几个子类型，如 jpeg、gif 或 tiff。下面展示了一个定义 JPEG 文件 MIME 类型的示例 MIME 类型条目。MIME 类型是 image/jpeg，可能的文件扩展名列表是 "jpeg jpg jpe"：

image/jpeg jpeg jpg jpe

