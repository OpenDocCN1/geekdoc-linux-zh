
窗口管理器提供了一个框架，应用程序可以在其中显示其图形输出，用户可以通过用户生成的事件与应用程序程序进行交互。窗口管理器的外观（按钮的外观、样式和颜色；即其主题）和感觉（按钮的工作方式、菜单的激活方式）与图 22.16 中区域 E 中运行的应用程序的外观和感觉无关。正因为如此，可以重新配置默认 KDE4 窗口管理器的外观和交互性，而不会影响在窗口管理器边框内运行的任何应用程序的外观或交互性。

要了解重新配置默认 KDE4 窗口管理器使其具有不同外观和感觉所需的步骤，请执行实践练习 22.3。在此实践练习中，你将更改 KDE4 交互风格的一个特性，称为焦点策略。焦点策略是图形服务器对当前位置的响应。例如，如果你移动鼠标，并且屏幕光标滚入一个窗口，则该窗口成为输入和输出事件的当前窗口。你还将更改 KDE4 的外观为另一个主题。我们假设你正在使用默认的 KDE4 窗口管理器，并且它具有“默认主题”外观作为默认值。我们还假设你的虚拟桌面图块是虚拟屏幕显示中的一个。

## 表 22.5 KDE4 窗口的 Konsole 窗口组件

| 项目 | 名称 | 描述 |
|---|---|---|
| A | 标题栏 | 显示当前路径并允许窗口移动 |
| B | 控制按钮 | 最小化、最大化和关闭窗口 |
| C | 工具栏 | 允许你使用 xterminal 特定工具 |
| D | 主体 | Xterminal CUI 控制台显示，在此输入命令并查看结果 |
| E | 边框 | 允许使用“手柄”调整窗口大小 |

![](img/02e070097d401d3bf7de4bf1c470b267_1054_0.png)

图 22.16 xterminal 窗口的 Konsole 显示。

### 实践练习 22.3

步骤 0：作为本次练习的初步准备，观察你在移动鼠标并屏幕光标在打开的窗口之间切换时 KDE4 的响应，例如 `Konsole` 窗口或 `Dolphin` 文件管理器窗口。当你用鼠标将光标滚过一个窗口时，窗口显示什么行为？

步骤 1：从 `Kickoff` 应用程序启动器中，做出菜单选择 `系统设置`。系统设置窗口在屏幕上打开。单击“窗口行为”图标，并做出“窗口行为”侧边栏选择。KDE4 窗口行为 – 系统设置窗口在屏幕上打开，类似于图 22.17。

![](img/02e070097d401d3bf7de4bf1c470b267_1055_0.png)

FIGURE 22.17 Window Behavior - System Settings window.

Step 2: Click on the `Focus` tab. Move the slider all the way to the right, to the `Hover` pole.

Step 3: Left-click on the `Apply` button in the Window Behavior - System Settings window.

Step 4: Now move the mouse so that the cursor shifts between windows on screen. The behavior of the window manager has changed, depending on what you set the focus policy to be.

Step 5: Left-click on the `Overview` arrow in the upper-left corner of the Window Behavior - System Settings window. This returns you to the main window, as seen in Step 1.

Step 6: From the Main Menu, click on the `Workspace Appearance` icon. Click on the `Desktop Themes` sidebar choice. The Desktop Theme - System Settings window appears on screen, similar to Figure 22.18.

![](img/02e070097d401d3bf7de4bf1c470b267_1055_1.png)

FIGURE 22.18 KDE4 theme manager window showing the default theme.

In this figure, we have already added the “Steampunk” theme to the available choices (“Air,” “Air for netbooks,” “Oxygen”).

Step 7: Left-click once on the `Get New Themes...` icon in the lower left of this window. Search for a new theme and install it. It now appears in the Desktop Theme - System Settings window. Click on this newly installed theme to make it the current theme.

Step 8: Left-click on the `Apply` button at the bottom of the Desktop Theme - System Settings window, and if you do not want to test the appearance of other themes on your desktop, then click on the `Quit` button at the top of the System Settings window. Your desktop now has the theme of your choice!

## 22.3.5 KDE4 System Settings

The most important configuration tool that you have available to you from the KDE4 desktop is the System Settings facility, activated by making the `Kickoff` Application Launcher icon System Settings choice. This utility allows configuration of single-user attributes, as well as system-wide attributes for all users. A single user with ordinary privileges is allowed to make a variety of changes in the performance of the PC-BSD system itself and the performance of the KDE4 desktop. For example, as shown in Practice Exercise 22.3, you can use a series of on-screen menu choices to change the focus behavior within KDE4 windows and select a new theme.
