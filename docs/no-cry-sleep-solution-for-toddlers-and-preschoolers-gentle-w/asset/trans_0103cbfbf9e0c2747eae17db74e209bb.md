

KDE 控制中心包含用于配置声音和 kickerrc 的面板。从控制中心，你还可以访问一组专门的 KDE 系统配置工具。目前这些包括登录管理器和字体管理器。

## .kde 和桌面用户目录

你的 .kde 目录保存用于维护你的 KDE 桌面的文件和目录。Desktop 目录保存 KDE 桌面文件，其图标显示在桌面上。配置文件位于 .kde/share/config 目录中。在这里你可以找到不同组件的通用配置文件。kwinrc 保存窗口管理器的配置命令，kmailrc 用于邮件，kickerrc 用于你的面板。kdeglobals 保存键盘快捷键以及其他全局定义。你可以直接在这些文件中的任何一个中放置配置指令；.kde/share/mimelnk 保存用户添加的菜单项的桌面文件。.kde/share/apps 目录包含用于配置 KDE 应用程序的文件和目录。

## MIME 类型和关联应用程序

随着你安装新的程序类型，它们可能会使用某种类型的文件。在这种情况下，你需要将该类型注册到 KDE，以便它可以与某个应用程序或一组应用程序关联。例如，GIF 图像的 MIME 类型是 image/gif，它与图像查看程序关联。你使用 KDE 控制中心来设置新的 MIME 类型或更改 MIME 类型与应用程序的关联。选择 KDE 组件下的文件关联条目。这将列出已知的 MIME 类型及其关联的文件名扩展名。选择一个条目进行编辑，在那里你可以更改与其关联的应用程序。KDE 将其 MIME 类型信息保存在 KDE 配置目录中的一个名为 mimelnk 的单独文件中。

要更改特定文件的关联应用程序，你使用文件管理器找到该应用程序，然后右键单击它并选择编辑文件类型。这会显示一个包含两个面板的窗口：常规和嵌入。在常规菜单中，你可以通过单击添加并输入文件类型的扩展名来添加扩展名，使用 * 来匹配前缀。例如，*.gif 将匹配任何以 .gif 结尾的文件。在应用程序首选项顺序部分，使用添加按钮选择你希望与文件关联的应用程序。你可以为单个文件设置多个应用程序，并按你希望的方式更改它们的首选项顺序。单击应用以保存你的更改。

## KDE 目录和文件

当 KDE 安装在你的系统上时，其系统范围的应用程序、配置和支持文件可能安装在与其它 GUI 和用户应用程序相同的系统目录中。在 Red Hat 上，KDE 安装在标准系统目录中，并有一些变化，例如 /usr/bin 用于 KDE 程序文件，/usr/lib/kde3 保存 KDE 库，而 /usr/include/kde 包含在应用程序开发中使用的 KDE 头文件。由 KDE 应用程序设置的文件和目录。/usr/share/mimelnk 保存 MIME 类型定义。/usr/share/config 包含特定 KDE 应用程序的配置文件。这些是系统范围的默认值，可以被用户自己的 .kde/share/config 目录中的个人配置覆盖。/usr/share/icons 保存用于你的 KDE 桌面和 KDE 应用程序以及 Bluecurve 界面的默认图标。如前所述，在用户的主目录中，.kde 目录保存用户自己的桌面及其应用程序的 KDE 配置。

每个用户都有一个 Desktop 目录，其中保存用户桌面上所有图标和文件夹的 KDE 链接文件（参见表 7-3）。这些包括回收站文件夹以及 CD-ROM 和主目录链接。

表 7-3 KDE 安装目录

| System KDE Directories | Description |
| --- | --- |
| /usr/bin | KDE programs |
| /usr/lib/kde3 | KDE libraries |
| /usr/include/kde | Header files for use in compiling and developing KDE applications |
| /usr/share/config | KDE desktop and application configuration files |
| /usr/share/mimelnk | Desktop files used to build the main menu |
| /usr/share/apps | Files used by KDE applications |
| /usr/share/icons | Icons used in KDE desktop and applications |
| /usr/share/doc | KDE Help system |
| User KDE Directories |  |
| .kde/AutoStart | Applications automatically started up with KDE |
| .kde/share/config | User KDE desktop and application configuration files for user-specified features |
| .kde/share/mimelnk | Desktop files used to build the user’s menu entries on the KDE main menu |
| .kde/share/apps | Directories and files used by KDE applications |
| Desktop | Desktop files for icons and folders displayed on the user’s KDE desktop |
| Desktop/Trash | Trash folder for files marked for deletion |

