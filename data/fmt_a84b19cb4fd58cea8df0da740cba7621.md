
将合适的 CD 或 DVD 插入计算机的驱动器（假设驱动器可写），在下载 ISO 镜像的文件夹中右键点击 ISO 镜像图标，并选择“刻录光盘”。当 Windows 磁盘映像刻录机出现时，选择刻录映像。

`Roxio Creator`：这是一款第三方 Windows 应用程序包含许多刻录 CD 和 DVD 的功能。您可以在此处阅读有关该的产品：http://www.nero.com/en/products/creator/。

`N CD/DVD Burning Nero`：Nero 是另一款适用于 Windows 系统的流行 CD/DVD 刻录软件。您可以了解更多关于 Nero 的信息：http://www.nero.com。

# 在 MacOS 系统上刻录 CD/DVD

与 Windows 似的，macOS 操作系统内置了 CD/DVD 刻录软件。要在 MacOS 系统上将 ISO 镜像刻录磁盘，请按照以下步骤操作：

- 1. 在您的 MacOS 系统上下载所需的 ISO 镜像。桌面上应该会出现一个代表 ISO 的图标。
- 2. 将空白 CD 或 DVD 插入您的 CD/DVD 刻录机，根据镜像的大小选择合适的类型。
- 3. 右键点击您刚刚下载的 Linux ISO 图标，并选择“刻录‘Linux’到磁盘”。会弹出一个窗口，询问您是否确定要刻录该映像。
- 4. 填写您想要为 ISO 指定的名称和写入速度，然后选择“刻录”。映像开始刻录到磁盘。
- 5. 映像刻录完成后，弹出磁盘；您已准备好在合适的计算机上启动该 CD 或 DVD 了。

# 在 Linux 中刻录 CD/DVD

Linux 同时拥有图形界面和命令行工具，用于将 CD 和 DVD 映像刻录到物理介质。本节中的示例展示了如何从桌面使用 K3b，或使用 `ddrecord`（或 `wodird`）将 ISO 镜像刻录到 CD 或 DVD。如果尚未安装，您可以按照以下方法安装任其一：

对于 Fedora 或 RHEL

```
# yum install k3b
# yum install wimdim
```

对于 Debian 或 Ubuntu

```
# apt-get install k3b
# apt-get install wimdim
```

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_834_0.png)

# 第七部分：附录

## 在 Linux 桌面刻录 CD 或 DVD

以下是如何在正在运行的 Linux 系统（如 Fedora）中使用 `K3b` 创建可启动的 Linux CD 或 DVD。`K3b` 随 KDE 桌面一起提供，但在 GNOME 桌面环境下也运行得良好良好。

- 1. 下载您想要复制到计算机硬盘的 ISO 镜像。（CD 映像大小约为 700MB。单层 DVD 小于 4.7GB）。
- 2. 打开 CD/DVD 刻录程序。对于此过程，我推荐使用 `K3b` CD 和 DVD 创建器 (http://www.k3b.org/)。在 Fedora 中，选择“活动”并输入 `K3b`（或在终端窗口中输入 `K3b`）。出现“`K3b – CD 和 DVD 创建器`”。
- 3. 从 `K3b` 窗口，选择“工具” > “刻录映像”来刻录 CD 或 DVD ISO 映像。系统会要求您选择一个映像文件。
- 4. 浏览到您下载或复制到硬盘的映像并选择它。如果您选择了所需的映像，将出现“刻录映像”窗口，并显示映像的校验和。图 A.3 显示了准备好选择 Fedora 映像的 `K3b` 窗口。

### 图 A.3

使用 `K3b` 刻录您的 CD 或 DVD。

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_835_0.png)

- 5. 将空白 CD 或 DVD 插入 CD/DVD 驱动器（这可能是一个组合 CD/DVD 驱动器）。
- 6. 映像刻录完成后，弹出磁盘；您已准备好在合适的计算机上启动该 CD 或 DVD 了。

（注：原文后续部分似乎存在重复或乱码文本，已根据指令翻译逻辑进行了对齐处理）

- 7. 映像刻录完成后，弹出磁盘；您已准备好在合适的计算机上启动该 CD 或 DVD 了。

# 附录 B：练习答案

如果你正确完成了之前的练习，Nautilus（文件管理器）和 Firefox 应该位于不同的工作区中。以下是在 GNOME 3 和 GNOME 2 中在工作区之间切换的方法：

## GNOME 3

按下 Windows 键，并在右列选择你想要的工作区。或者，你也可以通过按下 `Ctrl+Alt+Tab` 直接进入你需要的应用程序，然后按 `Tab` 键和方向键高亮你想要打开的程序。

## GNOME 2

使用鼠标点击底部面板右侧的工作区微型图标来选择你想要的工作区。如果你开启了桌面特效（系统 ⟷ 偏好 桌面特效 ⟷ Compiz），尝试按下 `Ctrl+Alt+右方向键`（或左方向键）来旋转切换到下一个工作区。

- 7. 若要打开系统已安装的应用程序列表，并尽可能通过几次点击或按键选择一个图片查看器，请执行以下操作：

### 在 GNOME 3 中

将鼠标移动到屏幕左上角进入概览（Overview）屏幕。选择“应用程序”（Applications），然后从右列选择“工具”（Utilities），最后选择“图片查看器”（Image Viewer）。

### 在 GNOME 2 中

选择“应用程序”（Applications） ⟷ 图形（Graphics） ⟷ 图片查看器（Image Viewer）在桌面上打开图片查看器。

- 8. 若要将当前工作区的窗口视图更改为较小的视图以便进行切换，请执行以下操作：

### 在 GNOME 3 中

在多个工作区打开了多个窗口的情况下，按下 `Alt+Tab` 键。在按住 `Alt` 键的同时，反复 `Tab` 直到高亮你想要的应用程序。释放 `Alt` 键进行选择。

### 在 GNOME 2 中

在多个工作区打开了多个窗口的情况下，按下并按住 `Ctrl+Alt+Tab` 键。在按住 `Ctrl+Alt` 键的同时，反复 `Tab` 直到高亮你想要的应用程序。释放 `Ctrl` 和 `Alt` 键进行选择。

- 9. 若要使用键盘从桌面启动音乐播放器，请执行以下操作：

### 在 GNOME 3 中

- a. 按下 Windows 键进入概览屏幕。

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_840_0.png)

b. 输入 `Rhythm`（直到图标出现并被高亮）并按回车。（在 Ubuntu 中，如果你没有安装 Rhythmbox，输入 `Bansh` 来打开 Banshee 媒体播放器。）

### 在 GNOME 2 中

按下 `Alt+F2`。在出现的应用程序框中，输入 `rhythmbox` 并按回车。

- 10. 若要仅使用按键为桌面截屏，在 GNOME 3 和 GNOME 2 中按下 `Print Screen`（打印屏幕）键可拍摄整个桌面截图。按下 `Alt+Pnt Screen` 可仅拍摄当前窗口的截图。在这两种情况下，图像都会保存在家目录目录下的 `Pictures` 文件夹中。

## 第 3 章：使用 Shell

- 1. 在 Fedora 或 Ubuntu 中切换虚拟控制台并返回桌面（此功能在 RHEL 系统中已禁用），请执行以下操作：

    a. 按住 `Ctrl+Alt+F2`。将出现一个文本的控制台。
    b. 输入你的用户名（按回车）和密码（按回车）。
    c. 输入命令例如 `id`，并返回登录提示符。
    d. 输入 `exit` 退出 shell 并返回登录。按下 `Ctrl+Alt+F1` 返回到带有桌面的虚拟控制台。（在不同的 Linux 系统中，桌面可能位于不同的虚拟控制台。`Ctrl+Alt+F7` 和 `Ctrl+Alt+F2` 也是常见的位置。）

- 2. 将你的终端（Terminal）字体设为红色，背景设黄色。

    a. 从 GNOME 桌面，选择“应用程序”（Applications）  系统工具（System Tools）  打开终端窗口。
    b. 在终端中，选择“编辑”（Edit） ﬙ 偏好（Preferences）。
    c. 选择“颜色”（Colors）选项卡，并选择“来自系统主题的颜色”（Colors from system theme）。
    d. 选择“文本颜色”（Text Color）旁边的框，从可用选项中点击你需要的红色，然后点击“选择”（Select）。
    e. 选择“背景颜色”（Background Color）旁边的框，从可用选项中点击你需要的黄色，然后点击“选择”（Select）。
    f. 关闭“配置文件”（Profile）窗口以返回带有新颜色的终端窗口。
    g. 返回并重新选择“使用系统主题的颜色”（Use colors from system theme）以恢复默认终端。

- 3. 查找 `mount` 命令和 `tracepath` 的帮助页（man page）。
