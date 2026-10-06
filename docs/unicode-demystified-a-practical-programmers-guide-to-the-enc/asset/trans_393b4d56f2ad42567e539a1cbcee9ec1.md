

## 杂杂

本节涵盖了使用 K 菜单编辑器、Desktop 文件、在运行 KDE 时自动启动应用程序、报告 Bug 以及使用 KDE 功能的内容。

## kmenuedit：编辑 K 菜单

K 菜单编辑器（图 8-30）允许您通过添加/删除/修改子菜单和单个菜单来更改 K 菜单（第 274 页）。右键点击 K 菜单图标（或红帽子）并选择菜单编辑器以显示编辑 K 菜单窗口。根据需要展开树形视图（左侧），点击您想要更改、删除、移动或复制的部分，或者点击下方想要插入新选择的区域。根据您的意愿更改右侧的子窗口，或点击工具栏上相应的图标。创建子菜单后，您需要在该子菜单内创建一个新项目。

子窗口（右侧）描述了您希望菜单选择执行的程序。您必须填充的唯一字段是“Command”（命令）文本框，它包含了在从 K 菜单选择该项时要执行的命令行。“Name”（名称）是 K 菜单中选择的名称。“Comment”（注释）是注释。“Type”（类型）描述程序类型，几乎总是“Application”（应用程序），由 K 菜单编辑器填充。当您想分配图标或更改现有图标时，点击“Work Path”（工作路径）文本框右侧的图标。“Work Path”是启动程序时目录的绝对路径。

![](img/aa8214d49e1cf50152c432845129fb3b_393_0.png)

当您指定基于字符的程序时，必须在终端模拟器中运行它；在下一个框中勾选“Run in terminal”（在终端运行），并在“Terminal Options”（终端选项）中指定任何命令行选项。如果您有权限，可以以不同的用户运行程序。“Current”（当前）键行指定执行命令的快捷键。点击此帧右侧的键映射来更改执行命令的按键。有关如何更改键，请参考第 302 页的“shortcuts”。

## Desktop 文件

Desktop 文件具有 .desktop 文件扩展名，存储有关其如何显示的信息以及指定指向位置的 URL。URL 可以是本地文件或目录、Internet URL 或 FTP 地址。以下简写文件名 home.desktop 位于 $KDEHOME/share/apps/konqsidebart/entries，在 Konqueror 导航面板工具栏中显示为房屋图标，并链接到主目录：

```
$cat home.desktop
[Desktop Entry]
Encoding=UTF-8
Type=Link
URL=file:$HOME
Icon=folder_home
Name=Home gets
Name[af]-huis gets
Comment=This file contains your personal files
Comment[af]-hierdie cabinet bevat jou persoonlike 1ªers
Open=False
X-KDE-TreeModule=directory
X-KDE-KonqSidebarModule=konqsidebar_tree
```

查看同一目录下的其他 Desktop 文件以了解完整的 Desktop 文件长什么样。另请参见第 306 页的“Navigation Panel”和第 297 页的“Show Navigation Panel”。

## 指定窗口管理器

在 /usr/bin/startkde 文件的末尾有一行可以指定 KDE 使用的窗口管理器。由于它没有指定窗口管理器，KDE 默认使用 kwin：9

```
kwrapper ksmserver--restore || \
```

9. 随其后的行是该行的延续：确保反斜杠是您新行的最后一个字符。

## 第8章 KDE 桌面环境

要指定 Sawfish 窗口管理器，请以 root 身份操作，将前面的行改为 kwrapper ksmserver --restore --windowmanager sawfish || \

当您启动 KDE 时，它会自动启动全局自启动目录（$KDEDIR/share/autostart，当变量未设置时，$KDEDIR 的值默认为 /usr）中的程序，然后是 Autostart 目录（$KDE_HOME/Autostart）中的程序。虽然 KDE 可以使用会话管理功能（第 185 页）在关闭 KDE 时重启符合标准的正在运行的程序并在重启 KDE 时重新启动它们，但您必须将非符合标准的程序放在 Autostart 目录中以便它们自动重启。拖并复制或链接想要自动启动的非符合标准的程序到 Autostart 目录。

## 自动启动

## 报告 Bug

选择 K 菜单：Extras⇒Bug Report Tool 打开 Bug Buddy 窗口，该窗口便于向 KDE 组发送 Bug 报告。按照窗口中的指示提交 Bug 报告。

## 音频

声音通过 K 菜单：Control Center⇒Sound 控制。默认情况下，KDE 在后台运行 aRT（模拟实时合成器，www.arts-project.org）声音服务器。如果没有声音服务器，需要播放声音的程序在继续之前会请求系统获取音频设备（声卡）的控制权。aRT 为音频设备提供了一个层，允许程序输出声音而无需等待设备变为可用。aRT 会混合声音。如果您正在播放音乐（例如，使用 KDE 的媒体播放器 noatum），而另一个应用程序正在播放声音，aRT 会将此声音与音乐混合在一起，而不会中断音乐。

aRT 服务器是一个专业的音频服务器；它提供了专业音乐创作软件所需的高级功能。由于 GNU/Linux 设计时没有考虑到专业（实时）需求，您必须在 (1) 使用大量资源的高质量声音和 (2) 使用较少周期的低质量之间之间选择。为了提高性能，当您选择 K 菜单：Control Center⇒Sound 的实时优先级时

## 章节总结

KDE 桌面环境提供了丰富的工具，包括多个帮助系统；一个灵活的文件管理器和浏览器；一个包含文字处理、演示文、图表和电子邮件的办公套件；以及可以通过多种方式配置的众多面板和菜单。

帮助系统包括“这是什么?”（What's This?）、KDE 帮助和帮助菜单。K 菜单应用程序启动器、主面板使 KDE 易于驱动。您可以通过多种方式自定义工具以适应任何环境。

Konqueror 作为 KDE 的文件管理器和浏览器，自身的功能很少。它依赖其他程序来完成工作。Konqueror 在自己的窗口内打开这些程序，给人一种它非常强大的印象。它是程序无缝集成的良好范例。

