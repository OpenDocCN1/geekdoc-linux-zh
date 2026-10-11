
-   **IceWM** — IceWM 可从 http://www.icewm.org 获取。它是一个注重速度、易用性和一致性的优秀窗口管理器。它可以模拟 Motif、OS/2 和 Windows 的外观，并允许你使用位图来自定义外观。

-   **Sawfish** — Sawfish 可从 http://sawmill.sourceforge.net/ 获取。它是一个可扩展的窗口管理器，使用基于 LISP 的脚本语言。所有的窗口装饰都是可配置的，所有的用户界面策略都通过扩展语言来控制。Sawfish 现在是 GNOME 使用的默认窗口管理器。

-   **Window Maker** — Window Maker 可从 http://www.windowmaker.org/ 获取。它是一个 X11 窗口管理器，旨在模拟 NeXTStep 图形用户界面（GUI）的外观和感觉。它相对快速、功能丰富，且易于配置和使用。

## 桌面环境

窗口管理器为你的桌面提供了良好的外观和感觉，但直到最近，关于如何让应用程序看起来和工作起来保持一致，并没有真正的规则。然而，进入计算领域的新桌面环境正在改变这一点。桌面环境包括一套应用程序、文件管理器、控制面板、窗口管理器以及许多其他组件。它们被设计为具有相同的外观和感觉协同工作。两个最流行的桌面环境是 KDE 和 GNOME。每个新的 Linux 用户都有责任尝试这两种环境，并决定他/她最喜欢哪一种。

### KDE

KDE 可从 http://www.kde.org 获取。Linux 的第一个大规模桌面环境是 KDE。它是一个成熟的项目，提供一个易于使用的环境，并捆绑了许多应用程序、一个窗口管理器和一个易于使用的控制面板。KDE 是围绕 Trolltech 的 Qt 库构建的。开发人员可以使用这些库编写其他应用程序，使它们很好地集成并与 KDE 协同工作。Qt 库曾经处于限制性许可证之下，导致其接受度存在一些问题，但这种情况最近发生了变化。

### GNOME

Ximian GNOME 发行版可从 http://www.ximian.com 获取。GNOME（GNU 网络对象模型环境）最初是作为 KDE 的替代品而启动的，因为 KDE 所基于的 Qt 库并不在自由许可证之下。GNOME 最初是一个独立的项目，但一家名为 Helix Code 的公司是由核心开发人员创立的，目的是推广和资助该项目。Helix Code 后来将其名称更改为 Ximian。他们提供了一个出色的 GNOME 发行版，其中包含许多应用程序、sawfish 窗口管理器、控制面板和许多桌面主题。它还包含一个易于使用的更新工具，让你通过自动下载新更新来保持系统的最新状态。

虽然你可以获得没有 Ximian 打包增强的 GNOME，但我们建议你包含这些增强功能，因为它们提供了额外的工具和安装程序。

## 安装 X

**目标**

-   **安装并配置 XFree86。** 验证显卡和显示器是否受 X 服务器支持，安装正确的 X 服务器，配置 X 服务器，安装 X 字体服务器，安装 X 所需的字体（可能需要手动编辑 “Files” 部分的 `/etc/X11/XF86Config`），为显卡和显示器定制和调整 X。命令：XF86Setup, xf86config。文件：/etc/X11/XF86Config, .xresources。

安装 X 最简单的方法是在发行版的主安装过程中完成。这样，所有所需的软件包都会预先安装并配置好。但是，如果你安装了一个没有 X 的系统，后来又决定添加它，你同样可以做到。安装方法取决于你的发行版使用的打包系统。

### 使用 RPM 安装

如果你的系统使用 RPM，建议从发行版 CD-ROM 或站点安装必要的 RPM 软件包。这是因为大多数发行版都会对 X Window 安装进行调整和定制。一些发行版添加特殊的用户工具，例如自动创建菜单。

### 在 Debian 上安装

Debian 用户可以通过输入以下任一命令轻松地将 X 添加到系统中：

```bash
apt-get install task-x-window-system-core
```

或者

```bash
apt-get install task-x-window-system
```

这些任务将下载所有所需的软件包，安装它们，并引导你完成 X 的配置。核心任务仅下载基本的 X 窗口系统，而系统任务则下载 X 以及窗口管理程序和其他支持应用程序。

### 使用二进制软件包安装

XFree86 组提供了二进制 *tar* 文件和安装脚本，供那些不想或不能使用其他打包系统的用户使用。这些软件包可以从他们的站点 http://www.xfree86.org 获取。提供了一个 README 文件，其中包含安装说明。以下步骤将引导你使用 *tar* 文件安装 XFree86。请务必先更改到一个临时目录。在下面的示例中，你位于 /root/X 目录。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_369_0.png)

> **提示** 与每个版本的 XFree86 一起分发的发行说明告诉你支持哪些硬件设备。

-   FTP 到 ftp.xfree86.org 并作为匿名用户登录。

    ```sh
    [root@redhat ~]# ftp ftp.xfree86.org
    Connected to ftp.xfree86.org.
    220 public.xfree86.org FTP server (Version wu-2.6.1(l)) Tue
    Jan 2 12:12:36 PST 20 01) ready.
    Name (ftp.xfree86.org:root): anonymous
    331 Guest login ok, send your complete e-mail address as
    password.
    Password:
    230-
    230- Welcome to ftp.xfree86.org, the master server for
    XFree86 distribution.
    230-
    ```

-   更改到 `/pub/XFree86/3.3.6/binaries/Linux-ix86-glibc21` 目录。
-   将 FTP 客户端更改为二进制模式并关闭提示。

    ```sh
    ftp> binary
    200 Type set to I.
    ftp> prompt
    Interactive mode off.
    ```

-   通过输入 `mget all` 下载此目录中的所有文件。
-   通过输入 `cd servers` 更改到 Servers 目录。
-   通过输入 `ls` 列出可用的服务器。
-   为你的视频卡选择合适的服务器，并使用 `get server_filename` 下载它。
-   退出 FTP 客户端。
-   通过输入 `chmod +x *.sh` 使两个安装脚本可执行。
-   通过输入 `mkdir /usr/X11R6` 创建一个名为 `/usr/X11R6` 的目录。
-   通过输入 `cd /usr/X11R6` 更改到 `/usr/X11R6`。
-   从临时目录执行 `preinst.sh` 脚本。
-   使 `extract` 脚本可执行。例如：

    ```sh
    [root@redhat /usr/X11R6]# chmod +x /root/X/extract
    ```

-   执行 `extract` 脚本，参数为包含下载文件的目录。

    ```sh
    [root@redhat /usr/X11R6]# /root/X/extract /root/X/*.tgz
    ```

-   执行 `postinst.sh` 脚本。

    ```sh
    [root@redhat /usr/X11R6]# /root/X/postinst.sh
    ```

-   对提示的链接问题回答“是”。
-   最后一步是运行配置工具来创建所需的 `XF86Config` 文件。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_370_0.png)

`XF86Config` 配置工具将在本章后面的“配置 X”部分中讨论。

## XFree86 的版本

![](img/96d9ccd181675a8ae8b6a1146c919d2b_370_1.png)

-   **2.10 X**
    -   安装并配置 XFree86。验证显卡和显示器是否受 X 服务器支持，安装正确的 X 服务器，配置 X 服务器，安装 X 字体服务器，安装 X 所需的字体（可能需要手动编辑 “Files” 部分的 `/etc/X11/XF86Config`），为显卡和显示器定制和调整 X。命令：XF86Setup, xf86config。文件：/etc/X11/XF86Config, .xresources。

今天有两个主要版本的 XFree86 在使用中。一些发行版仍然在发布 XFree v3，而其他一些已升级到新的 XFree v4。LPI 考试是围绕 XFree v3 编写的，因此它将是这里的重点，但我们试图提及与 XFree v4 的重要区别。

两个版本之间用户会注意到的最大变化是以下几点：

-   合并的 X 服务器
-   略有不同的 `XF86Config` 格式
-   速度

在 XFree v3 中，X 服务器是按视频芯片组分开的。你必须确保为你的硬件安装了正确的服务器。表 9-1 列出了可用的 X

