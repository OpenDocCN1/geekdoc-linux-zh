
| Alt+Right mouse button | Display the window control menu by clicking anywhere in a window except on its title bar |
| Ctrl+Alt+Backspace | Emergency exit from the X Window System. This immediately returns you to the graphical login prompt or to text mode. If you have any open windows with unsaved documents (such as a text editor), the information in those windows will be lost. |
| Alt+F1 | Display the GNOME main menu |
| Alt+F4 | Close the active window |
| Alt+F5 | Return a maximized window to its previous size |
| Alt+F7 | Move the active window; use the arrow keys to move the window (the current screen location is shown in the middle of the window), then press Enter when you're done moving |
| Alt+F8 | Resize the active window; use the arrow keys to adjust the size (the current size is shown in the middle of the window), then press Enter when you're done resizing |
| Alt+F9 | Minimize the current window |
| Alt+F10 | Maximize the current window |
| F1 | Open a window displaying the online help system |

# CONFIGURING GNOME AND KDE

GNOME 和 KDE 都是高度可配置的。在本节中，您将了解如何访问桌面配置实用程序，并探索一些示例配置更改。

## Switching Between Desktop Interfaces

尽管 Red Hat Linux 和 Fedora 中的默认桌面界面是 GNOME，但许多用户喜欢可以选择使用的界面。您可以使用桌面切换器实用程序来选择登录时显示的桌面。

要使用此实用程序，您在终端窗口中输入命令 `switchdesk`，后跟要切换到的桌面的名称（例如 GNOME 或 KDE）。请记住，您可以右键单击桌面并选择打开终端来打开终端窗口。例如，此命令将您的默认桌面更改为 KDE（如果您已安装 KDE 软件包）：

```
$ switchdesk KDE
```

还有一个名为桌面切换器的图形版本（使用 `switchdesk-gui` 命令启动），如图 2-4 所示。相应的软件包默认情况下未安装，因此，如果您想尝试此程序而不是使用命令行版本，则需要从 Fedora CD 安装该软件包——如第 10 章“管理软件包和文件系统”中所述。

![](img/43f64015de86d989e30eff5bb284fb96_96_0.png)

图 2-4 桌面切换器实用程序，显示典型 Fedora 系统上可用的桌面界面和窗口管理器

Linux 系统上的每个用户都可以独立运行桌面切换器或 `switchdesk` 来选择他或她喜欢使用的桌面界面。当您在桌面切换器中选择一个可用的桌面或使用命令行上的 `switchdesk` 时，您必须退出 X Window System 并再次登录才能使更改生效。为此，请使用 GNOME 主菜单上的最后一项注销。当您再次登录时，您选择的桌面将运行。

> 如果您尝试使用 `twm` 等窗口管理器，您应该计划从命令行使用 `switchdesk` 命令将设置改回 GNOME。

## Saving Your Configuration Between Logins

每次注销时，GNOME 都可以记录哪些应用程序窗口处于打开状态，以便下次登录时自动打开相同的应用程序。（但这些应用程序中的文档不会自动加载。）当您正在处理大量窗口并且需要注销一天时，这很有用。下次登录时，您从 GNOME 中打开的所有终端窗口、浏览器和其他应用程序都将按您离开时的状态打开。

要保存登录之间的配置，请在选择 GNOME 菜单上的注销时出现的消息框中选择保存当前设置复选框。此复选框默认未选中，因为在必须处理应用程序窗口时，注销和登录需要额外的时间。您可以更改此设置，以便每次注销时默认保存当前设置。下一节将介绍如何更改此设置。

## Configuring the Graphical Login Screen

您可以使用 GNOME 提供的实用程序根据自己的喜好设置图形登录屏幕。由于图形登录屏幕供系统上的所有用户使用，因此您必须以 root 身份登录或输入 root 密码后才允许配置图形登录屏幕的大部分内容。

要配置图形登录屏幕，请在 GNOME 主菜单上选择系统设置，然后选择登录屏幕。（您也可以从终端窗口运行 `gdmsetup` 命令。）如果您未以 root 身份登录（您通常不应以 root 身份登录），则在运行此实用程序之前必须输入 root 密码。

在 GDM 设置实用程序的常规选项卡上（如图 2-5 所示），您可以选择基本选项，例如系统启动时是否应自动登录用户，或是否在您指定的延迟后自动登录用户。您的选择当然取决于您情况所需的便利性和安全性水平。例如，空闲 10 分钟后自动登录非常方便，但如果您经常在工作时让系统无人看管，也会带来很大的安全风险。

> 图形登录提示的所有配置选项都无法在 GDM 设置实用程序中访问。您也可以通过编辑文件 `/etc/X11/gdm/gdm.conf` 来更改配置设置，但这是一个相当高级的操作。

![](img/43f64015de86d989e30eff5bb284fb96_98_0.png)

## 图 2-5 GDM 设置实用程序

在常规选项卡上，您还可以选择对本地或远程登录的用户使用标准问候程序（登录屏幕）还是图形问候程序。远程登录是 X Window System 的强大功能，但本书中未详细讨论。 第 15 章“高级主题和故障排除”包含一些额外信息。此实用程序的安全性和 XDMCP 选项卡也在第 15 章中进一步讨论，尽管此时至少查看安全选项卡是有帮助的，以了解它提供的选项；其中一些可能很有帮助，例如允许在图形登录屏幕内（即成功登录之前）配置图形登录屏幕。

单独的选项卡配置标准和图形问候屏幕。图形问候程序默认用于本地用户（坐在计算机前面的用户）。在图形问候程序选项卡上，您会看到图形登录屏幕的主题列表。主题是一组颜色、字体和图像，为显示提供特定的外观和感觉。您可以为桌面界面的其他部分设置主题，如下一节所述。在图形问候程序选项卡中，您可以从图 2-6 所示的列表中选择已安装的主题之一，或单击安装新主题按钮，将您从 Internet 站点下载或自行创建的主题添加到列表中。

图形登录屏幕的面部浏览器功能使其为每个用户显示一个小图形图像。如果您为图形问候程序选择的主题包含面部浏览器，或者在标准问候程序选项卡上选择了面部浏览器选项（窗口底部左侧的杂项部分下），则可以通过选择 GNOME 主菜单上的首选项，然后选择登录照片来配置您自己的图形图像（您的面部或您选择的任何图像）。

![](img/43f64015de86d989e30eff5bb284fb96_99_0.png)

Figure 2-6 The Graphical greeter tab within the Login Screen Setup window

## The Panel

正如你所学到的，Panel 是 GNOME 桌面界面底部的一条栏。KDE 也包含类似的一条栏。Panel 是一个独立的应用程序，显示以下内容：

- 桌面界面的主菜单
- 你经常使用的程序的图标
- 工作区切换器
- 每个打开窗口的带标签按钮（你可以点击任意按钮使该窗口处于活动并可见状态）
- 日期和时间指示器
- 其他信息项

当你右键单击 Panel 上的任何图标时，会出现一个菜单，你可以在其中移动该项目在 Panel 上的位置，完全从面板中移除该项目，或查看该项目的属性（例如，查看图标打开的是哪个应用程序）。图 2-7 显示了当你右键单击 Panel 上的 Launcher 图标并选择 Properties 时出现的 Launcher Properties 对话框。

![](img/43f64015de86d989e30eff5bb284fb96_100_0.png)

Figure 2-7 The Launcher Properties dialog box used to configure the Panel
