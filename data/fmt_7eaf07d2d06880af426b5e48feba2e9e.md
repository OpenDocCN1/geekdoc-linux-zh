
> 与 GNOME一样，本小时讨论的窗口管理器不仅适用于 Linux，还适用于任何带有 X 器的 UNIX 系统，例如 XFree86。

## 桌面环境

你显示器上用于窗口的整个区域被称为*桌面环境*，或*桌面外壳*。桌面外壳允许你在图形化设置中运行应用程序和操作文件，而不是使用键盘输入命令。计算机（更准确地说说是内核）接收到的输入与你输入命令是相同的——只是在你和内核之间多了一层。桌面提供了一个你可以用来与计算机通信的接口。

## 图形界面

任何桌面系统的基础都是使用鼠标进行指向和点击的图形界面。在 UNIX 系统（包括 Linux）中，图形界面被称为 X。X 以图片或*图形*的形式在你的显示器上显示信息。你可以使用鼠标与屏幕上的图形进行交互。当你点击屏幕上的按钮或框时，X 会接收来自鼠标的输入并将其翻译计算机理解的命令。然而，为了让 X 运行，必须有东西告诉 X 显示什么以及显示的外观如何。该功能由 GNOME 和窗口管理器完成。

## 窗口管理器

在图形界面环境中，有一个区域被称为*桌面*，其上通常有图标和菜单。你可以点击菜单名称或应用程序图标来运行它。应用程序将在窗口中打开，你可以将其拖动到桌面的任何地方。

## 与窗口管理器协作

你可以将窗口最大化以占据整个桌面，或将其最小化使其从桌面上消失。通常窗口周围有一个边框，上面有应用程序或文件的名称，可能还有允许你关闭和更改窗口大小的图标。如图 4.1 所示，窗口管理器控制着窗口的所有方面：

- 窗口的大小
- 窗口边框
- 窗口的设计和外观
- 窗口功能
- 窗口在桌面上的移动
- 桌面的整体外观

图 4.1

窗口管理器控制窗口的位置和功能，但并不控制窗口内部出现的应用程序。

桌面图标 -

![](img/56ffc05f2012b0375f08095ea492838b_62_0.png)

| 应用程序图标 | GNOME 面板 | 任务切换器 (Enlightenment) | 图标盒 (Enlightenment) |

## 它们是如何整合在一起的

窗口管理器告诉 GNOME 窗口所在的位置以及放置方式。GNOME 还会从窗口管理器获取关于哪些程序已打开以及它们如何配置的信息。然后，GNOME 使用这些信息创建 GNOME 任务列表，并在你注销时保存会话。窗口管理器和 GNOME 都向 X 发送信息，从而在屏幕上显示正确的信息。

在 的白皮书《GNOME Technologies: A Brief Description of the Technology Behind GNOME》中，David Mason 将 GNOME 与窗口管理器之间的信息交换描述为“提示（hints）”。如果窗口管理器无法从 GNOME 读取提示，则该窗口管理器就不符合 GNOME 标准，并且在窗口管理器中无法使用 GNOME 的完整功能。

图 4.2 X、窗口管理器和 GNOME 之间的关系。

![](img/56ffc05f2012b0375f08095ea492838b_63_0.png)

窗口管理器向 GNOME 发送关于打开文件的信息，例如应用程序名称、路径以及窗口的大小和位置。GNOME 使用来自窗口管理器的信息添加到面板上的 GNOME 任务列表中。

如果你在应用程序内部使用拖放操作（例如，在文件管理器中将文件从一个目录移动到另一个目录），GNOME 库中的其他函数会将该信息发送到 X 服务器。然后，X 服务器告诉内核移动文件。

窗口管理器还会向 X 服务器发送信息，以便应用程序出现在正确的位置，并使你可以使用鼠标和键盘与窗口进行交互。

## 符合 GNOME 标准的窗口管理器

如果一个窗口管理器是“符合 GNOME 标准的”，意味着你可以在窗口管理器中充分利用 GNOME 的功能。它可以接受来自 GNOME 的指令并向 GNOME 提供信息，以跟踪启用如 GNOME 任务列表、会话管理和拖放等功能的项目。

尽管 GNOME 在很大程度上与几乎所有的 X 窗口管理器兼容，但符合 GNOME 标准的程度各异。迄为止，完全符合 GNOME 标准的窗口管理器只有 Enlightenment、FVWM、sawmill、IceWM 和 WindowMaker。

![](img/56ffc05f2012b0375f08095ea492838b_64_0.png)

> 支持 GNOME 的红帽在其发行版中封装了几个窗口管理器，包括 FVWM、NextStep 和 Enlightenment。检查你的文件系统已安装了哪些窗口管理器。

## Enlightenment

Enlightenment 是 GNOME 的默认窗口管理器，它作为桌面环境运行。像 GNOME 的其他部分一样，Enlightenment 是免费软件。它由 Enlightenment 项目不断开发和扩展。Enlightenment 项目的网站为 http://www.enlightenment.org。

除了所有 Linux 变体，Enlightenment 还运行于以下平台：

- Solaris
- FreeBSD
- Linux [ libc5 和 glibc ]
- AIX *
- Irix *
- HP/*

## 第4 章

> 在 AIX、Irix 和 HP 平台上安装 Enlightenment 必须采取额外步骤。请查看 Enlightenment 网站 http://www.enlightenment.org。

![](img/56ffc05f2012b0375f08095ea492838b_65_0.png)

为了高度可配置，Enlightenment 比任何其他窗口管理器都有更多的自定义选项。你可以使用 Gimp 等图形设计工具设计边框、按钮和菜单。你可以使用 Enlightenment 配置管理器选择选项，或者下载整个主题。

Enlightenment 也是一个桌面外壳，这意味着你可以单独使用它启动应用程序。根据 Enlightenment 项目的计划，Enlightenment 将拥有自己的文件管理器、拖放和小程序管理功能。然而，目前这些功能处于计划阶段。

## Enlightenment 的优点

- Enlightenment 完全符合 GNOME 标准。
- 作为 GNOME 的默认窗口管理器，Enlightenment 安装和运行相对简单。
- Enlightenment 在外观和功能上设计为高度可配置。
- 有数百种主题可供 Enlightenment 使用。许多主题精美且富有创意（见图 4.3）。

## Enlightenment 的缺点

- 由于 Enlightenment 有许多配置选项，有些人初次使用时觉得复杂。
- 与其他窗口管理器相比，Enlightenment 非常复杂。它占用大量的系统资源，因此可能会降低速度，例如加载 GNOME 和打开窗口。如果你有快速处理器和大内存（超过 64MB），这可能不是问题。

## 安装 Enlightenment：所需的软件

对于这些说明，假设你正在运行 lib6（或 glibc2），你拥有版本 6 或更高版本的 X Window 系统，并且你的系统配备了 Intel 处理器。如果你没有 X Window 版本，请访问 http://www.x11.org 下载最新版本。（如果你不确定是否有 lib6 或 X Window 版本 6，请参阅附录 A，“排除故障”）。如果你没有 Intel 处理器，你必须从源代码编译 Enlightenment。欲了解更多请访问 http://www.enlightenment.org。

## 4.3 Enlightenment

你可以使用 Enlightenment 创建出惊艳的桌面外观。

![](img/56ffc05f2012b0375f08095ea492838b_66_0.png)

你还需要：

- 一个 GCC 编译器
- 一个 Imlib 包或 tar 包（图形服务器）
- 一个 Fnlib 包或 tar 包（用于位图字体）
- 一个 Enlightenment 包或 tar 包

可选地，你可以安装：

- ESD（一个用于混音的音频服务器）
- Eterm（用于支持位图的终端）
- Eplus（包括时钟和 CD 播放器等）
- Emusic（用于 MP3/MOD/WAV/CD/AU 播放器）
- Gtk-Perl（用于编辑 ConfigEdit）
- Perl（配合 Gtk-Perl 使用）

所有模块都可以在 http://www.enlightenment.org 下载，并提供 tarball 包、rpm 和 deb 包。即使你的 Linux 发行版已经包含了 Enlightenment，我们有时也会通过该网站获取最新版本。

在安装或升级 Enlightenment 之前，请确保你已经拥有较新版本的 Enlightenment 支持库 Imlib 和 Fnlib。为了稍微复杂一点，你还必须拥有支持 Imlib 和 Fnlib 的最新版本库！

请验证你是否拥有以下库的最新稳定版本，这些库可以在 Enlightenment 网站以 tarball、rpm 和 deb 格式下载：

- Libgif 或 Libungif
- Libz
