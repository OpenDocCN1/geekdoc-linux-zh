

![](img/c8827ea52a0796def3f6891892ed9d3a_62_0.png)

图 2.3 *运行配置脚本*

## 一个重要的开关

如果你计划编译 XEmacs，有一个重要的配置开关你可能想要使用，特别是如果你计划安装未包含在 XEmacs 包系统中的软件包。你应该输入以下命令：

```
./configure --with-site-lisp
```

如果没有这个开关，XEmacs 不会在 site-lisp 目录中查找文件。你可以在命令行上使用多个开关。这是配置 XEmacs 安装到 /opt 并识别 site-lisp 目录的方法：

```
./configure --with-site-lisp --with-prefix=/opt
```

## 编译和安装

配置脚本运行需要一些时间。信息会在你的屏幕上滚动，显示脚本正在进行的各项测试。最后一步是在 Emacs 源目录的各个子目录中创建各种 Makefile。

现在你可以输入

```
make
```

然后在 XEmacs 构建期间去喝杯咖啡。根据处理器的速度，这可能需要几分钟到几个小时不等。当构建完成后，只需输入

```
make install
```

Emacs 文件将被复制到它们的新位置。一旦你确认新的 Emacs 二进制文件可以工作，你就可以删除整个源目录。

## 使用 GTK 编译 XEmacs

XEmacs 21.4 源包也可以将 GTK 作为其小部件集进行编译，而不是默认的 Athena 集（Athena 集是 X11 程序的标准）。

威廉·佩里（William Perry），Emacs 网页浏览器 W3 的开发者（有关 W3 的更多信息请参见第 20 章），最近获得报酬重写 XEmacs 的屏幕显示部分，以便其利用 GTK 工具包（见图 2.4）。

GTK 是一个跨平台开发平台，近年来变得非常流行，尤其是在 Linux 社区。它最初是为满足 GIMP 图像编辑项目的需要而开发的，但后来它已形成自己的发展路径。GTK 被许多流行的 Linux 应用程序使用，包括 Mozilla 项目、GNOME 桌面环境以及许多其他应用。

![](img/c8827ea52a0796def3f6891892ed9d3a_63_0.png)

从源码构建 GTK-XEmacs 的唯一额外要求是与你安装的 GTK 和 GLib（与 GTK 相关的库包）版本相对应的发展包。大多数 Linux 发行版会自动安装 GTK 和 GLib，但你可能需要手动安装发展包。GTK-XEmacs 还需要 GNOME 发展包，但你不必运行 GNOME 才能使用此版本的 Emacs。

要启用实验性的 GTK 支持，你需要给配置脚本一个参数，如下例所示：

```
./configure --with-gtk
```

如果你是 GNOME 桌面环境的用户，你可以添加这个额外的开关，虽然这并非绝对必要：

```
./configure --with-gtk --with-gnome
```

现在你可以按照上述说明继续进行编译和安装。

## XEmacs 包

XEmacs 开发者没有将最常用的扩展包捆绑在主源发行版中，而是选择将几乎所有包分离出来，对它们进行分类，并单独提供它们。如果没有其中的一些包，XEmacs 的功能将不如你所期望的那样强大。如果你知道你想要什么，单独的软件包位于 CD-ROM 的目录 `/cdrom/packages/xemcs/packages/single` 中。

如果你有可用的磁盘空间，获得所需软件包的最简单方法是安装 Sumo 包，它由所有单独的软件包捆绑在一个 tar 文件中组成。你可能会得到一些你不需要的或不想要的软件包，但你可以在确定哪些软件包实际上对你有用后删除它们。Sumo 文件位于目录 `/cdrom/packages/xemcs/packages`。

从源码编译的 XEmacs 期望在 `/usr/local/lib/xemcs/packages` 中找到其软件包（除非配置方式不同）。如果你将所需的软件包 tar 文件复制到该目录并解压，必要的子目录将被创建并填充文件。

从二进制发行包文件（*.debs 或 RPMs）安装的 XEmacs 将位于 /usr 而不是 /usr/local，因此请相应调整你的操作过程。

你可以在第 12 章中阅读更多关于 XEmacs 软件包系统的内容。

## CD-ROM 上的额外软件包

本书第三部分描述了许多 Emacs 的外部附加软件包。这些软件包未包含在 Emacs 或 XEmacs 的官方发行版中，但其中一些无疑将在未来被添加。Emacs 开发者定期评估新的软件包，如果认为它们足够有用，则计划将其纳入下一个 Emacs 发行版。

你不必等待有用的软件包被包含在内。只需将软件包（有些只是单个 Lisp 文件，其他由几个文件组成）复制到你的 *usr/local/share/emacs/site-lisp* 目录（XEmacs 使用的目录是 */usr/local/lib/xemacs/site-lisp*）。下一节帮助你使它们运行起来。你可以在本书 CD-ROM 的目录 */packages/external* 中找到这些软件包的选择。

## 试用一个软件包

我将使用一个名为 *clipper.el* 的小型单文件软件包作为示例。图 2.5 显示此文件加载到 Emacs 会话中。文件的开头，像大多数 Lisp 文件一样，用分号注释掉了。通常在这里可以找到安装说明。

![](img/c8827ea52a0796def3f6891892ed9d3a_65_0.png)

图 2.5 *clipper.el*

这些行是相关的部分：

```
;;; Usage:

;;

;; install via (require 'clipper) in your .emacs

;;

;; The following functions allow you to manipulate clipper:

;;

;; 'clipper-create' create a new clip

;;

;; 'clipper-delete' delete an existing clip

;;

;; 'clipper-insert' insert a clip into the current buffer

;;
```

你可以通过评估自包含的 Lisp 语句 `(require 'clipper)` 轻松激活此文件。Lisp 和评估在第 7 章中讨论。目前，你只需要知道的是，将光标放在一个带括号的 Lisp 表达式后面，然后按 Ctrl-x Ctrl-e 会评估前面的表达式。这样做之后，你可以通过按 M-x 然后输入 `clipper-create` 来使用 `clipper-create` 等命令（参见前面的摘录）。

第 15 章描述了 clipper.el 是什么以及它能做什么；这只是临时安装一个软件包的插图。如果你按照这个例子操作后关闭 Emacs，然后再次启动它，Emacs 不会加载 clipper.el，命令将不可用。

## 永久激活一个软件包

在试用一个软件包并发现它适合你的需求后，你很可能希望永久安装它，以便每次使用 Emacs 时，该软件包的功能都可用。你通过将 clipper.el 文件中的单条 Lisp 语句 `(require 'clipper)` 复制到你的 `.emacs` 文件中来实现这一点。

此时，你可能还没有一个 `.emacs` 文件，这是一个初始化文件，包含 Emacs 启动时读取的命令和设置。第 9 章详细讨论了该文件；现在只需说明，从像 clipper.el 这样的扩展文件复制的单条语句（如语句 `(require 'clipper)`）可以粘贴到空的 .emacs 文件中，并且是有效的，会被 Emacs 接受。

其他扩展软件包要求将几行内容复制到你的 .emacs 文件中。Emacs 社区已经形成一种惯例，在 Lisp 文件的开头或附近提供说明，因此记得首先查看那里。一些多文件软件包以 tar 存档形式分发，其中通常包含 README 或 INSTALL 文件。

## 结论

你现在应该有一个可用的 Emacs 安装可以进行试验。花一些时间自行实验。你可以尝试按 Ctrl-h t 进行 Emacs 教程。

下一章帮助你学习基本的 Emacs 键盘命令。

