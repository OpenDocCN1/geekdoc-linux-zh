
| `-onewp` | 告诉 WordPerfect 在现有的 WordPerfect 实例中打开新文件，如果已打开。 |
| `-printer "name"` | 将默认打印机设置为指定的名称。如果打印机名称包含空格，则需要引号。 |
| `-recover` | 尝试修复无法工作的文档，特别是当问题与表格有关。 |
| `-restore` | 删除您的 `~/.wprc/.wp8x.set` 文件，将其还原为默认值。 |
| `-setup path` | 设置 WordPerfect 读取 `.wp8x.set` 文件的目录。 |
| `-temp path` | 设置 WordPerfect 存储临时目录。 |

- 若要了解如何安装打印机和字体，请查看“字体与打印”，第 739 页
- 若要了解如何设置默认值，请参阅“自定义偏”，第 767 页
- 若要了解更多关于 WordPerfect 的语言，请查看“语言”，第 141 页
- 若要了解更多关于宏，请查看“让计算机工作”，第 483 页
- 若要了解如何选择打印机，请查看“选择打印机”，第 151 页

- 如果您想配置系统让所有 KDE 用户都能访问 WordPerfect，请执行以下操作：

1. 以 root 身份登录或使用 `sudo` 获取系统访问权限。
2. 通过编辑 `/etc/group` 或您的发行版提供的任何用户管理工具为 WordPerfect 创建新组。确保将所有希望访问 WordPerfect 的用户加入组。
3. 更改 WordPerfect 文件的组。例如，`chgrp --recursive wp /opt/wp8` 将 `/opt/wp8` 中的所有文件更改为 `wp` 组。
4. 移除读取和执行权限。例如，`chmod o-rx /opt/wp8` 移除这些权限。

现在，只有 `wp` 组的用户可以运行 WordPerfect 或访问目录下的文件。

3. 将 KDE 图标或其他您想要用于 WordPerfect 的图标拷贝到 `share/icons` 目录。例如，执行 `cp /opt/wp8/wplib/dt/appconfig/icons/c/wpBApp.m.pm /opt/kde/share/icons/wp.xpm` 可以使该图标全局可访问。

**注意** CD 上的 KDE 配置文件假设 WordPerfect 已在您的搜索路径中，您需要按照本章前面的说明设置一个 shell 脚本，以便从路径中的位置启动 WordPerfect。或者，您也可以编辑 `x-wp.kdelink` 和 `xWp.kdelink` 文件，为它们提供 WordPerfect 可执行文件的完整路径。

您可以为 WordPerfect 自定义 KDE 配置文件。例如，CD 上的文件可以将扩展名为 `.wpd`、`.wp8`、`.wp7` 和 `.wp6`（这些扩展名的大写版本）的文件识别 WordPerfect 文件。您可以添加其他文档类型，例如，每当您点击 Microsoft Word `.doc` 文件时，KDE 都会启动 WordPerfect。您还可以编辑 `share/mimeinfo/magic` 文件，让 KDE 即使在文件具有奇特的扩展名时也能检测到文件。如果您喜欢，可以为 KDE 文件管理器的 KDE 菜单提供不同的图标。请咨询您的 KDE 文档以获取这些高级配置主题的帮助。

在编辑配置文件时，您可能需要重启 KDE 以识别更改。退出已打开的应用程序并注销或退出 X；然后登录或重启 X。现在，您应该可以在 KDE 菜单的“应用程序”（Applications）标题下看到 WordPerfect，并且能够从 KDE 文件管理器将 WordPerfect 文档加载到 WordPerfect 中。

## GNOME

GNU 网络对象环境 (`GNOME`) 是 KDE 作为 Linux 集成桌面环境方面的主要竞争对手。因此，它具有与 KDE 类似的功能，包括从菜单中或通过双击文件管理器中的 WordPerfect 文档来启动 WordPerfect。

要在屏幕底部的主 `GNOME` 面板（图 A.13）上添加 WordPerfect 图标，请右键点击面板的空白区域，并从上下文菜单中选择“添加新启动器”（Add new launcher）。此操作将打开图 A.14 所示的“创建启动器”（Create launcher）应用程序对话框。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_750_0.png)

## 附录 A 安装与系统配置

**图 A.13**

`GNOME` 包含一个位于屏幕底部的面板。该面板包含快速启动工具、时钟和其他便利工具。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_751_0.png)

**图 A.14**

`GNOME` 创建启动器应用程序对话框允许您为像 WordPerfect 这样的程序创建新的面板启动器。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_751_1.png)

在“创建启动器”应用程序对话框中，您可以输入关于 WordPerfect 的信息：

- **名称（Name）**——您希望在菜单中显示的名称。例如，您可以使用 WordPerfect 或 WP for Linux。
- **注释（Comment）**——与程序关联的注释。例如，您可能指定您使用的是个人零售版还是下载版。
- **命令（Command）**——启动 WordPerfect 的命令。如果程序或启动它的 shell 脚本在您的路径上，您可以在此处输入 `xwp`。否则，输入程序的完整路径，例如 `/opt/wp8/wbin/xwp`。
- **类型（Type）**——保留默认值：Application（应用程序）。
- **图标（Icon）**——点击“图标”按钮，显示图 A.15 所示的“选择图标”对话框。如果您之前从 `wplib/dt/appconfig/icons/C/usr/share/pixmaps` 拷贝了 CDE 图标并赋予其 `xpm` 扩展名，`GNOME` 将其作为此窗口中的选项之一显示。选择它并点击 OK。

## 图 A.15

您可以从“选择图标”对话框中为 WordPerfect 选择任何喜欢的图标。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_752_0.png)

在“创建启动器”应用程序对话框中输入完信息后，点击 OK，`GNOME` 就会在其面板中创建一个新的 WordPerfect 启动器。您可以像操作其他 `GNOME` 启动器一样对其进行处理——详情参考 `GNOME` 文档。

如果您希望在 `GNOME` 文件管理器窗口中双击 WordPerfect 文件时能够自动链接它们，请从主 `GNOME` 面板菜单选择“设置，`GNOME` 控制中心”（Settings, `GNOME` Control Center）以打开图 A.16 所示的控制中心窗口。在控制中心窗口左侧选择“Mime 类型”以显示和编辑 Mime 条目，通过这些条目将文档类型与应用程序关联。

## 图 A.16

您可以创建一个 Mime 类型来链接到 WordPerfect 文档。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_752_1.png)

配置文件的关联和存储方式。

## 附录 A 安装与系统配置

添加适当的 Mime 类型：

1. 点击控制中心中的“添加”（Add），打开图 A.17 所示的“添加 Mime 类型”对话框。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_753_0.png)

2. 在“添加 Mime 类型”对话框的“Mime Type”字段中输入 WordPerfect。
3. 在图 A.17 所示的“Extension”字段中输入您想要与 WordPerfect 关联的文件扩展名。
4. 在“添加 Mime 类型”对话框中点击 OK。WordPerfect 应该出现在控制中心。
5. 确保选中了 WordPerfect 并点击“编辑”（Edit），调出图 A.18 所示的编辑对话框。

![](img/fc6d0b1918f77fc89ff58d110e0a8ab2_753_1.png)

## 配置 GUI 支持 WordPerfect

6. 在图 A.18 所示的字段中输入 WordPerfect 的名称，必要时输入其完整路径，后跟一个空格。
7. 点击对话框上部分的图标，进入“选择图标”对话框，其外观和工作方式类似于图 A.15。为 WordPerfect 选择一个图标并点击 OK。
8. 在编辑对话框中点击 OK；然后在控制中心中点击 OK 以选择文件。

您的 WordPerfect 文件将带有独特的图标出现在 `GNOME` 文件管理器中，当您双击其中一个时，WordPerfect 会启动并加载该文件。

## FWWM 家族
