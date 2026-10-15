
如果你遇到困难，现在应该能够通过邮件向 Launchpad 发送命令，邮件带有加密签名，可以证明邮件是由你发送的且未被任何人劫持。我们在 Launchpad 上验证签名并……

我们正在招聘具有可靠性和稳定性能力的软件工程师

我们正在寻找由精明、有积极性且有经验的人组成的团队加入我们的使命！

批准你自己的交易报告 - 2011 年 7 月 29 日：你如何管理你的项目

明天再也不用月单了 - 2011 年 7 月 27 日

如何听有关各种场景你能听到的最佳消息。

图 38.1 Launchpad 是在 Ubuntu 中开发的起点。

Launchpad 是 Ubuntu 开发发生的地方。它集成了之前介绍的 Bazaar 版本控制系统，使得跟踪软件代码的更改变得简单得多，并允许在时撤销这些更改，同时跟踪执行这些操作的人。Launchpad 整合了 Soyuz，这是一种发行和存档管理软件，用于处理 Launchpad 内部的自动包构建。

对于使用 Launchpad 的开发者来说，这意味着过程变得稍微简单了。他们可以专注于编写和编辑代码，让 Launchpad 处理更改的保存和包的创建。这对于编写和维护需要源码版本控制等大型项目的活跃开发者非常有用。它还托管了错误报告和跟踪、邮件列表、软件界面翻译等许多功能。这大部分内容超出了本章的范围，但对严肃的开发者来说非常有吸引力。

我们感兴趣的是，注册的 Launchpad 用户可以创建个人存档库（PPA）。这是一种提供软件包的更简单的方法。任何拥有 PPA 的人都可以提取源代码来构建软件包。这些软件包将可以在 apt 仓库中可用，该仓库可以添加到任何 Ubuntu 用户的源列表中，并使用 Ubuntu 中的任何标准包管理工具（如 apt、Ubuntu 软件中心和 Synaptic）进行下载或删除。每个 Launchpad PPA 的网页上都包含说明说明，描述了如何添加该仓库，使得这种简单的软件共享方法变得轻而易举，即使是非技术的终端用户也可以添加和删除。图 38.2 显示了 Google 稳定版本的 PPA。

![](img/d9236e4682dfcf03b759a19829a318ef_729_0.png)

图 38.2 用于 Google Chromium 稳定版本的 Launchpad PPA。

## Quickly

几位非常有见地且才华的 Ubuntu 开发者聚在一起开始讨论。这些人是懂得如何编程并享受编程的人。同时，他们希望 Linux 上的编程变得简单且有趣，并决定对于某些人来说，这并不有趣，因为学习起来可能太难了。有太多的选择、太多的工具以及太多的文档需要阅读和学习才能入门。他们有一个“如果……”的时刻：如果我们写一个程序，对工具和模板做出非常主观的筛选，并将它们提供给初级程序员以及那些只想快速编写一个应用程序而无兴趣在选择之前研究每个可用选项的人，结果会怎样？并不是每个人都关心 Gtk 与 Qt 的优劣，甚至不知道它们是什么。为什么要让那些对这些感兴趣的人来做这些选择呢？Quickly 就是这些讨论的结果，是其中一些开发者创建的解决方案。

Quickly 是一个帮助你快速编写和打包软件程序（以及其他内容）的工具。你可以从一组应用程序模板中进行选择，并使用一些简单的 Quickly 命令来创建代码、编辑 GUI 并发布你的软件供他人使用。Quickly 的模板很容易编写。所以，如果你是语言 foo 的粉丝，你可以创建一个 foo-project 模板。或者，如果你想帮助人们为你的杀手级应用制作插件，你可以创建一个 killer-app-plugin 模板。你甚至可以为管理公司文档创建一个模板，创建你出色的 LaTeX。更好的是，如果你不知道这些是什么意思，并想用带有漂亮的 GUI 制作实用的 Python 工具，你可以通过 Quickly 实现。

最流行的模板是 ubuntu-application 模板，这并不意外，因为 Ubuntu 社区编写了 Quickly 且到目前为止经常使用它。这个模板使用了一组特定的工具，这些工具是 Linux 中最常见的工具。它们包括：

- Python——流行且易学习的编程语言，涵盖于第 45 章“使用 Python”。
- GTK——用于创建 GUI 界面的跨平台工具包，在 GNOME 桌面环境中广泛使用，使其适合将新程序集成到桌面。
- Glade——来自 GNOME 社区的 GTK 用户界面设计师。它强大且易用，用于聚合项目所需的所有部件和窗口。
- GStreamer——一种在 GNOME 中使用的媒体框架，用于在桌面应用程序中集成音频视频内容。
- Desktop Couch——基于 Apache CouchDB 的数据库格式，允许在桌面程序中集成强大的数据库存储、复制和同步。它被 Ubuntu One 等用于云存储。
- gedit——GNOME 桌面的默认文本编辑器。

默认使用这些非常常用的工具消除了开发者在创建新应用程序时需要做出的许多困惑选择。由于这些选择在 Ubuntu、GNOME 以及整个 Linux 世界中都是常见的，使用它们创建的应用程序几乎可以与任何终端用户的桌面完美融合。

Quickly 包含在 Ubuntu 仓库中并从命令行运行。安装后，最好的方法是运行教程并阅读一些基础信息：

```
matthew@seymour:~$ tutorial ubuntu-application
```

Quickly 的一些实用命令包括：

```
matthew@seymour:~$ quickly create ubuntu-application matthewsapplication
```

创建一个名为 `matthewsapplication` 的 Ubuntu 程序初始模板以及你将在其中进行项目的子文件夹，你会收到一个漂亮的弹出窗口反馈（见图 38.3）。

![](img/d9236e4682dfcf03b759a19829a318ef_731_0.png)

图 38.3 Quickly 让你知道应用程序已成功创建。

要验证应用程序是否已创建，你可以切换到新的应用程序目录并列出内容：

```bash
matthew@seymour:-$ cd matthewsapplication
```

```bash
matthew@seymour:-$ ls -la
total 44
drwxr-xr-x 6 matthew 4096 2013-07-31 15:42 .
drwxr-xr-x 125 matthew 4096 2013-07-31 15:42 ..
-rw-r--r-- 1 matthew 45 2013-07-31 15:42 AUTHORS
drwxr-xr-x 6 matthew 4096 2013-07-31 15:42 bin
drwxr-xr-x 6 matthew 4096 2013-07-31 15:42 bzr
drwxr-xr-x 4 matthew 4096 2013-07-31 15:42 data
drwxr-xr-x 2 matthew 4096 2013-07-31 15:42 matthewsapplication
-rw-r--r-- 1 matthew 191 2013-07-31 15:42 matthewsapplication.desktop.in
-rw-r--r-- 1 matthew 76 2013-07-31 15:42 .quickly
-rw-r--r-- 1 matthew 2956 2013-07-31 15:42 setup.py
-rw-r--r-- 1 matthew 2837 2013-07-31 15:42 setup.pyc
```

按照以下步骤使用 Glade 开始编辑你新应用程序的 GUI：

```bash
matthew@seymour:-$ quickly quick design
```

这会弹出一个漂亮的界面，帮助你创建应用程序所需的所有动作、容器、小部件等（见图 38.4）。

![](img/d9236e4682dfcf03b759a19829a318ef_732_0.png)

图 38.4 Quickly 使用 Glade 帮助你创建用户界面。

在 edit 中更改应用程序行为并编辑 Python 代码（见图 38.5）：

```bash
matthew@seymour:-$ quickly edit
```

![](img/d9236e4682dfcf03b759a19829a318ef_733_0.png)

图 38.5 相邻标签页中的代码文件，便于在 edit 中快速方便地编辑。

通过运行以下命令测试你的新应用程序：

```bash
matthew@seymour:-$ quickly run
```

你可以使用此命令创建应用程序的包构建，这推荐用于测试：

```bash
matthew@seymour:-$ quickly package
```

Quickly 最令人兴奋的功能之一是它与 Launchpad 集成，可以加速处理 PPA 的过程。你需要一个 Launchpad 账户。有两个等效命令可以此此：

```bash
matthew@seymour:-$ quickly release
```

以及
