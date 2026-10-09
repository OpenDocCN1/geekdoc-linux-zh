
## 9. 单击 **Application font** 旁边的菜单按钮。
## 10. 在“选择字体”对话框中，从“族”列表中选中已安装的字体。
## 11. 单击“确定”，然后单击“关闭”。

## xorg.conf 文件

xorg.conf 文件是 XOrg 的配置文件。该文件用于配置不同的 X Window 参数，位于 `/etc/X11/xorg.conf` 目录中。

## 操作参考：配置 X 使用字体服务器

要配置 X 使用字体服务器：

- 1. 在 CLI 中以 root 身份登录。
- 2. 输入 `service xfs restart` 以重启 X 字体服务器。
- 3. 如有必要，输入 `chkconfig xfs on` 以使 Xfs 在系统启动时可用。
- 4. 输入 `startx` 以启动 X Window。

## 操作参考：在运行级别 3 中配置 XOrg

要在运行级别 3 中配置 XOrg：

- 1. 在 CLI 中以 root 身份登录。
- 2. 输入 `init 3` 以在运行级别 3 中启动。
- 3. 输入 `xinit`、`startx` 或 `init 5` 以从命令行启动 X 服务器。

## 操作参考：在运行级别 5 中配置 XOrg

要在运行级别 5 中配置 XOrg：

- 1. 以 root 身份登录。
- 2. 在命令提示符下，输入 `vi /etc/inittab` 以打开 inittab 文件。
- 3. 确保 `id: runlevel: initdefault` 这一行显示为 `id:5:initdefault`，以便在运行级别 5 中启动。
- 4. 保存并关闭该文件。
- 5. 重启计算机。

## 操作参考：导出 X 会话

要导出 X 会话：

- 1. 在 GUI 中以 root 身份登录。
- 2. 在终端中，输入 `DISPLAY=Client IP Address:0.0` 以设置显示变量。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_869_0.png)

- 3. 在客户端机器的 GUI 中以 root 身份登录。
- 4. 输入 `xhost +Server IP address` 以将服务器添加到主机列表。

## 活动 18-1
### 配置 X 字体服务器

**数据文件：**
MalOtt.ttf

**准备工作：**

1. 您已在 srvA 的 GUI 中以 root 身份登录。
2. 已显示终端窗口。
3. 在终端窗口中，输入 `rpm -qi libFS` 以检查是否安装了 libFS-1.0.0-3.1.i386.rpm 软件包。
4. 输入 `rpm -qi xorg-x11-xfs` 以检查是否安装了 xorg-x11-xfs-1.0.2.4.i386.rpm 软件包。
5. 输入 `rpm -qi chkfontpath` 以检查是否安装了 chkfontpath-1.10.1-1.1.i386.rpm 软件包。
6. 将 MalOtt.ttf 文件从 /085039Data/Graphical_User_Interface 复制到 /root 目录。
7. 输入 `clear` 以清除终端窗口。

**场景：**
您正在为组织中各部门的新员工设置计算机。图形部门的一名新员工需要具有高分辨率和颜色设置的 Linux GUI。该员工还希望将 MalOtt.ttf 字体安装到系统中。

| 您做什么 | 怎么做 |
| :--- | :--- |
| **1.** 安装新字体。 | **a.** 输入 `mkdir /usr/share/fonts/local` 以创建字体目录。 |
| | **b.** 输入 `cp /root/MalOtt.ttf /usr/share/fonts/local` 以将字体文件复制到 /usr/share/fonts/local 目录。 |
| | **c.** 输入 `cd /usr/share/fonts/local` 以导航到 local 目录。 |
| | **d.** 输入 `ttmkfdir -d /usr/share/fonts/local -o=> /usr/share/fonts/local/fonts.scale` |
| | **e.** 输入 `mkfontdir /usr/share/fonts/local` |
| | **f.** 输入 `chkfontpath -a /usr/share/fonts/local` |
| **2.** 配置新字体。 | **a.** 输入 `service xfs restart` 以重启 `xfs` 服务。 |
| | **b.** 输入 `clear` 以清除终端窗口。 |
| | **c.** 选择 **System→Preferences→Fonts** 以显示字体首选项对话框。 |
| | **d.** 单击 **Application font** 旁边的菜单按钮。 |
| | **e.** 在“选择字体”对话框中，在“族”列表中向上滚动并选择 **MalOtt**，然后单击 **OK**。 |
| | **f.** 单击 **Close**。 |

## 活动 18-2
### 配置 XOrg 服务器

**准备工作：**

1. 您已在 GUI 中以 root 身份登录。
2. 已显示终端窗口。

**场景：**
Kevin，您网络上的用户，希望查看其系统 X Window 在环境系统（位于同一网络上）上的情况。您被分配了设置其系统的任务。您决定配置 X 服务器并检查其是否处于正确的运行级别。您决定将 X 会话导出到环境系统。

| 您做什么 | 怎么做 |
| :--- | :--- |
| 1. 配置引导运行级别。 | a. 输入 `vi /etc/inittab` 以打开 inittab 文件。 |
| | b. 验证 `id:[runlevel]:initdefault:` 这一行是否显示为 `id:5:initdefault:`，以便在运行级别 5 中启动。 |
| | c. 关闭文件。 |
| 2. 导出 X 会话。 | a. 输入 `DISPLAY=192.168.0.2:0.0` 以导出 X 会话。 |
| | b. 输入 `exit` 以关闭终端窗口。 |
| | c. 选择 **System→Log Out root** 以注销系统。 |
| | d. 在消息框中，单击 **Log Out** 以注销系统。 |

## 主题 B
### 自定义显示管理器

您已实现 X 以配合 Linux GUI 工作。现在，您希望自定义 GUI 环境。在 GUI 中，桌面是用户交互的第一个屏幕之一。因此，桌面必须具有吸引力且易于使用。在本主题中，您将自定义显示管理器以管理桌面环境。

桌面是任何 GUI 的重要组成部分。用户可能希望根据自己的偏好自定义桌面环境。他们可以在桌面上保留经常访问的应用程序和不同程序的快捷方式。这将便于快速访问各种应用程序和选项。

### 显示管理器

![](img/477ccb2f05b6ba1b2d563ea74f18c197_873_0.png)

**定义：**

*显示管理器*（或*窗口管理器*）是一个控制桌面环境外观和感觉的程序。显示管理器提供图形登录屏幕并管理一组 X 服务器。这些服务器可能位于本地主机或远程系统上。这些管理器可以定制为在系统每次启动时运行。用户最常使用的桌面环境是 GNOME 和 KDE。

您可以自定义 KDE 和 GNOME 中 **Applications**、**Places** 或 **System** 文件夹中存在的任何应用程序。保存设置后，它们将应用于桌面环境。大多数应用程序对 KDE 和 GNOME 都是通用的，而一些则特定于各自的环境，例如 KDE 中的 **Control Center**。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_873_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_873_2.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_873_3.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_873_4.png)

*图 18-7：显示管理器的输出。*

### Linux 的显示管理器

Linux 常见的显示管理器如下：

- *GNOME 显示管理器*（*GDM*）是 Red Hat Linux 的默认显示管理器。GDM 允许用户配置语言设置并登录、关闭或重启系统。
- *KDE 显示管理器*（*KDM*）是 KDE 或 K Desktop Environment 的显示管理器。它允许用户登录、关闭或重启系统。

### GNOME 桌面环境

GNOME 桌面环境（GDE）是大多数 Linux 发行版的默认桌面环境。GNOME 桌面最初显示三个图标：**Computer**、**root's Home** 和 **Trash**。有两个水平面板，一个在桌面顶部，一个在底部。用户可以自定义这些面板，添加常用应用程序的快捷方式。使用 GDM 来自定义 GDE。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_874_0.png)

GNOME 桌面环境

![](img/477ccb2f05b6ba1b2d563ea74f18c197_874_1.png)

*图 18-8：包含其各个组件的 GDM。*

### KDE 桌面环境

在某些发行版（如 RHEL 5）中，KDE 桌面环境与 GDE 一起安装。在 KDE 中，只有底部有一个水平面板。在 RHEL 5 中，可以通过单击 KDE 面板左下角的 Red Hat 标志来访问主菜单。KDE 可以自定义以适应用户需求。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_874_2.png)

KDE 桌面环境

![](img/477ccb2f05b6ba1b2d563ea74f18c197_875_0.png)

*图 18-9：KDE 显示管理器，仅显示一个面板。*

### 配置 KDM

**Configure - KDE** 窗口允许您自定义 KDM 的外观。**Configure - K-Desktop** 窗口中可用的选项在下表中提供。

| Configure - K-Desktop 选项 | 用于 |
| :--- | :--- |
| **Display** | 配置分辨率和其他显示设置。 |
| **Behavior** | 配置桌面行为，例如启用桌面图标以及单击鼠标右键、左键或中键时执行的操作。 |
| **Multiple Desktops** | 配置虚拟桌面的数量。例如，您可以在 RHEL 中指定多达 20 个虚拟桌面。 |
| **Background** | 更改背景设置，例如墙纸和背景。 |
| **Screen Saver** | 设置屏幕保护程序及其计时选项。 |

### KDE 面板配置选项

**Add Applet**、**Add Application** 和 **Add New Panel** 选项用于访问和配置归类于 **Applet**、**Application Button** 和 **Panel** 下的不同应用程序。每个菜单中的一些选项在下表中提供。

