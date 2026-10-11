
| BusID | "PCI:1:0:0" |

EndSection

- 分辨率 — 你可能想要添加的最后一段主要信息是屏幕分辨率和色彩深度。电脑上安装的每块显卡都有一个相应的屏幕分辨率。`Screen` 部分定义了默认色彩深度（如 8、16 或 24）和模式（如 1024 x 768、800 x 600 或 640 x 480）。将 `DefaultDepth` 设置为代表系统色彩深度的位数，并添加 `Modes` 来设置屏幕分辨率。

如需了解更多关于如何在 `xorg.conf` 文件设置选项的信息，请输入 `man xorg.conf`。如果你的服务器是 XFree86，请输入 `man XF86Config`。

## 选择窗口管理器

全集成的桌面环境在更换窗口管理器时变得不再方便。不过，如果你喜欢，可以完全跳过 KDE 或 GNOME，仅使用 X 和你选择的窗口管理器启动桌面。

尽管我使用 Slackware 作为描述如何更改窗口管理器的参考发行版，但概念与其他 Linux 系统是相同的。通常情况下，如果 Linux 中没有运行桌面环境，你可以通过输入以下命令启动：

```bash
$ startx
```

此命令启动你的桌面环境或窗口管理器，取决于你的系统配置。虽然会读取多种配置文件并运行多个命令，但本质上最终的结果取决于两者之一：

- `/etc/X11/xinit/xinitrc` — 如果用户没有明确请求特定的桌面环境或窗口管理器，默认设置将来自该文件的内容。`xinitrc` 文件是系统级的 X 配置文件。不同的 Linux 系统使用不同的 `xinitrc` 文件。
- `$HOME/.xinitrc` — `.xinitrc` 文件用于让单个用户设置自己的桌面启动信息。任何用户都可以在其家目录下添加一个 `.xinitrc`。结果是，该文件的内容将覆盖任何系统级设置。如果你创建了自己的 `.xinitrc` 文件，其最后一行应该是 `exec windowmanager`，其中 `windowmanager` 是你窗口管理器的名称；例如：

```bash
exec /usr/X11/bin/blackbox
```

Slackware 至少有七种不同的窗口管理器供选择，这是一个尝试尝试的好地方。它还包含一个名为 `xwmconfig` 的工具，允许在范围内更改窗口管理器（在 `/etc/X11/xinit/xinitrc` 文件中）。要使用该工具，root 用户只需在 Slackware 系统的任何终端中输入 `xwmconfig` 即可。图 3.15 显示了该示例。

### 图 3.15

在 Slackware 中，你可以使用 `xwmconfig` 命令更改窗口管理器。

![](img/fa18693414a802b12c8add5f8c4be910_153_0.png)

从该屏幕选择你想要尝试的窗口管理器并点击 OK。下次运行 `startx` 时，该窗口管理器将启动（前提是你没有通过创建自己的 `.xinitrc` 文件来覆盖它）。以下是你的选择：

- Xfce (`www.xfce.org`)
- Blackbox (`blackboxwm.sourceforge.net`) — 另一个轻量级窗口管理器，力求消除库依赖以便在任何环境中运行。提供了许多设置颜色和样式的功能。
- FluxBox (`http://fluxbox.sourceforge.net`) — 基于 Blackbox (`0.6.1`)，FluxBox 增加了许多优秀的功能，如窗口标签（可以将多个窗口合并，以单个窗口上多个标签的形式显示）。它还包含图标栏并添加了实用功能（如使用鼠标轮切换工作空间）。
- Window Maker (`www.windowmaker.org`) — Window Maker 是 NEXTSTEP 图形界面的克隆，NEXTSTEP 是 20 世纪 80、90代流行的 UNIX 工作站。它是一个非常有吸引力的窗口管理器，支持主题、各种窗口装饰，以及更改背景和动画的功能，并可以添加小程序（称为 docks）。
- FVWM (`www.fvwm.org`) — 该窗口管理器支持完全国际化、窗口管理器提示和改进的功能。有趣的功能包括所有方向（甚至是对角线）的窗口阴影和侧边标题（包括垂直方向的文本）。
- FVWM-95 (`http://fvwm95.sourceforge.net`) — 一个为了看起来和感觉像 Windows 而创建的 FVWM 版本。
- Twm (Tabbed Window Manager) — 不再积极维护，但人们在需要真正极简的桌面时仍在使用 twm。在点击 twm 的左鼠标键之前，屏幕上什么都没有。使用弹出的菜单来打开和关闭窗口。

Linux 许多许多可用窗口管理器。要查看更多，请访问 Xwinman 网站 (`www.plig.org/xwinman`)。

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

### 选择你的窗口管理器

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

```bash
exec /usr/X11/bin/blackbox
```

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

一旦设置了窗口管理器的系统默认，用户就可以设置自己的窗口管理器。

# 图形化管理工具

许多 Linux 系统提供了简化的图形化工具，用于管理 Linux。如果你是普通用户，这些工具通常可以让你完成管理系统所需的所有操作，而无需编辑配置文件或运行 shell 命令。

让我们来看一些大多数 Linux 系统可用的基于 Web 的管理工具。

## 使用基于 Web 的管理

许多开源项目都提供了基于 Web 的管理工具，以便让这些项目对普通用户更容易上手。使用这些工具只需要一个 Web 浏览器（如 Firefox）、服务的端口号以及 root 密码。Samba 和 CUPS 等项目自带了自己的 Web 管理工具。Webmin 是一个通用工具，允许你通过 Web 浏览器管理各种 Linux 服务。

基于 Web 的管理工具的优势在于，你可以在熟悉的界面（你的 Web 浏览器）中进行操作，并且可以远程访问它们。

> 某些 Linux 发行版自带了一套图形化管理工具（例如 SUSE 的 YaST 或红帽 Linux 的 system-config 工具）。通常，你应该使用这些工具，而不是任何基于 Web 的界面，因为发行版自身的工具与其启动和停止服务的工具集成得更好。

## 提供 Web 管理的开源项目

几个主要的开源项目都提供了用于配置这些项目的 Web 界面。无论你使用哪种 Linux，都可以使用 Web 浏览器来配置项目：

- 要设置 Samba 与局域网内的 Microsoft Windows 系统进行文件和打印机共享，请从任何 Web 浏览器使用基于 SWAT 的 Samba 管理工具。在安装并运行 SWAT 后，你可以通过地址栏中的 URL 从 Web 浏览器访问你的服务器配置：

`http://localhost:901`

- Samba 项目还提供了其他管理 Samba 的图形化工具。你可以在 `http://samba.org/samba/GUI` 查看它们。有关这些工具的描述，请参阅第 26 和第 27 章。
- CUPS——通用 UNIX 打印系统 (`CUPS`) 有自己的 Web 管理工具。在安装并配置 CUPS 后，你通常可以在 Web 浏览器的地址栏中输入以下 URL 来使用 CUPS Web 管理：

`http://localhost:631`

你使用 CUPS 管理管理打印机和类，以及各种管理任务。CUPS 的描述见第 26 章。

## 学习基础管理

Samba 和 CUPS 包含在许多 Linux 发行版中。其他提供 Web 管理的项目（可能包含也可能不包含你的 Linux 发行版）包括 SquirrelMail（Web 邮箱接口）和 Mailman（邮件列表设施）。

由于许多 Web 浏览器管理界面以明文发送数据，它们最适合在本地系统使用。然而，因为它们是基于 Web 的，你也可以从局域网或其他网络使用这些界面。但是，如果你计划将这些管理界面暴露给不可信的网络，你应该考虑加密你的通信。

## Webmin 管理工具

Webmin 设施 (`www.webmin.com`) 提供了更完整的基于 Web 的 Linux 和 UNIX 管理功能。虽然 Webmin 并没有随某些自带图形化工具的 Linux 系统（如 Fedora 和 RHEL）提供，但 Webmin 项目已将 Webmin 移植到 70 多不同的操作系统。支持的 Linux 发行版包括 SUSE、红帽（Fedora 和 RHEL）、Debian、Ubuntu、Gentoo、Slackware、Mandriva、Yellow Dog 等（完整列表见 `www.webmin.com/support.html`）。
