

当你输入密码时，它不会显示在屏幕上。这是为了防止他人看到你的密码。如果你输入用户名或密码有误，系统会以错误信息“Login incorrect”作出回应，并要求你重新输入用户名，重新开始登录过程。然后你可以重新输入用户名和密码。

一旦你正确输入用户名和密码，你就登录到系统了。你的命令行提示符会显示出来，等待你输入命令。注意命令行提示符是一个美元符号（$），而不是井号（#）。$ 是普通用户的提示符，而 # 仅用于 root 用户。在这个版本的 Linux 中，你的提示符前面加上主机名和你所在的目录。两者都用一组方括号括起来。

```
[turtle /home/richlp]$
```

要结束你的会话，请执行 logout 或 exit 命令。这会将你返回到登录提示符，Linux 等待另一位用户登录。

```
[turtle /home/richlp]$ logout
```

## 关闭 Linux

如果你想关闭计算机，必须先关闭 Linux。如果不关闭 Linux，你可能需要在下次启动时要求 Linux 执行冗长的系统检查。你可以通过两种方式关闭系统。首先，登录到一个账户然后输入 halt 命令。该命令会注销你并关闭系统。

```
$ halt
```

另外，你也可以使用带 -h 选项的 shutdown 命令。使用 -r 选项，它会关闭系统然后重新启动它。在下一个示例中，系统在五分钟后关闭。要立即关闭系统，可以使用 +0 或单词 now（有关更多详细信息，请参阅第 28 章）。

```
# shutdown -h now
```

> Tip 关闭涉及一系列重要操作，例如卸载文件系统和关闭任何服务器。切勿简单地关闭计算机。

你也可以在登录提示符处强制系统重新启动，按住 CTRL 和 ALT 键然后按下 DEL 键（CTRL-ALT-DEL）。系统将经过标准的关闭程序然后重新启动计算机。

## 从命令行启动 GUI

登录系统后，你可以选择启动 X Window System GUI，例如 GNOME 或 KDE，并使用它与你的 Linux 系统交互。在 Linux 中，命令 startx 启动 X Window System 以及一个 GUI，然后你就可以使用窗口、菜单和图标与系统交互。startx 命令默认启动 GUI 桌面。一旦你关闭 GUI 界面，你将返回到命令行界面，仍然保持登录状态。在 Red Hat 上，你可以在桌面中使用 Desktop Switcher 在 GNOME 或 KDE 之间切换。Desktop Switcher 可从 Extra System Settings 菜单中的 Desktop Switching Tool 访问，或使用 switchdesk 命令。你做出选择然后退出桌面以返回到命令行界面。当你再次启动 GUI 时，所选的桌面将被使用。

## Bluecurve：GNOME 和 KDE 桌面

两种可选的桌面 GUI 界面可以安装在 Red Hat Linux 上：GNOME 和 KDE。两者各有自己的风格和外观。为了提供更一致的图形界面，Red Hat 为 GNOME 和 KDE 开发了统一的外观和感觉的默认设置，称为 Bluecurve。有了 Bluecurve，GNOME 和 KDE 看起来几乎相同，具有相同的菜单、面板项目和窗口样式。默认情况下，Red Hat 安装 GNOME，不过你也可以选择同时安装 KDE。GNOME 和 KDE 应用程序都可以通过 Bluecurve GNOME 或 KDE 菜单访问。Red Hat 在其主菜单中提供了一套标准应用程序，例如 OpenOffice，以及在 More 菜单中的其他对应应用程序，例如 GNOME 的 AbiWord 和 KDE 的 KOffice 在 More Office Applications 下。Bluecurve 本质上是一个主题，你可以使用 GNOME 或 KDE 配置工具进行更改。本节描述了 GNOME 和 KDE 桌面的 Bluecurve 界面。

需要注意的是，虽然 GNOME 和 KDE Bluecurve 界面看起来相同，但它们实际上是两个非常不同的桌面界面，具有各自用于选择首选项的工具。GNOME 和 KDE 上的 Preferences 菜单显示了非常不同的桌面配置工具选择。这些内容在第 6 章和第 7 章中讨论。

## GNOME

如图 3-1 所示的 Bluecurve GNOME 桌面显示，最初在屏幕底部显示一个面板，以及 Red Hat 最初设置的任何文件夹和网页图标。你会看到几个网页图标和一个指向你主目录的文件夹。屏幕底部的面板包含用于启动应用程序的图标，例如 Mozilla（Mouse and World 标志）、Evolution 邮件实用程序以及几个 OpenOffice 应用程序。你可以使用主菜单启动应用程序，通过点击面板左侧的 Red Hat 图标（Red Hat fedora 的图像）来显示该菜单。

当你点击桌面上的主目录文件夹时，会打开一个文件管理器窗口显示你的主目录。你可以显示主目录中的文件并使用上箭头按钮移动到父目录。Back 和 Forward 按钮可在先前显示的目录之间移动。在位置窗口中，你可以输入目录的路径名直接移动到它。在 GNOME 上，文件管理器也是 Internet 感知的。你可以使用它来显示网页和访问远程 FTP 目录以及显示或下载其文件。

要移动窗口，请左键单击并拖动其标题栏或右键单击其其他边框。每个窗口都支持 Maximize、Minimize 和 Close 按钮。双击标题栏会“着色”窗口，将其缩小为仅标题栏。你可以通过再次双击重新显示窗口。桌面支持完整的拖放功能。你可以将文件夹、图标和应用程序拖到桌面或其他打开到其他文件夹的文件管理器窗口。移动操作是默认的拖动操作（你也可以在拖动时按住 SHIFT 键）。要复制文件，请按住 CTRL 键然后单击并拖动然后释放

