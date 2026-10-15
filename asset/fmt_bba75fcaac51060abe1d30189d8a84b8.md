
# 附加

与 Fink 类似，当你从 Source（源码）菜单选择安装时，FinkCommander 会为你配置、编译并安装软件。FinkCommander 的左上角会显示描述安装每个阶段的消息。安装过程完成后，会显示 Done（完成）消息。此时，新安装工具的 Status（状态）列将包含版本号，告知你现在拥有该工具的当前发布版本。

你还可以使用 FinkCommander 移除软件。Remove（移除）选项出现在 Source 和 Binary（二进制）每个菜单下。

虽然 FinkCommander 的主要目的是让安装软件变得更简单，但它也提供了一种对系统软件进行清单的方便方法。它提供了每个已安装包的列表及其版本号，当前或过时的状态会告诉你是否存在更高版本。

在安装期间，你可以继续浏览可用工具的列表。这不会干扰安装过程。你可以从 Help（帮助）菜单中选择选择 FinkCommander Help，以更好地了解如何充分利用此工具。

| Name (名称) | Installed (已安装) | Status (状态) | Category (类别) | Latest (最新) | Description (描述) |
| --- | --- | --- | --- | --- | --- |
| atari | | 0.0 | games | 0.0-2 | 基于文本的2D 游戏引擎 |
| bash | | 1.4 | tools | 1.4 | |
| bison | | 3.1.2 | tools | 3.1 | 可配置解析器 |
| cmake | | 3.0.2 | tools | 3.0 | |
| decc | | 0.5 | games | 0.5 | 地城调度器 |
| damian | | 0.5.1 | games | 0.5 | |
| git | | 2.3 | tools | 2.3 | 分布式版本控制系统 |
| gnu | | 7.6.1 | tools | 7.6 | |
| make | | 3.1 | tools | 3.1 | 构建自动化工具 |
| mice | | 0.5.1 | games | 0.5 | 控制台游戏 |
| net | | 1.2 | tools | 1.2 | 基于网络的翻译器 |
| perl | | 5.2 | tools | 5.2 | |
| unix | | 1.7 | games | 1.7 | 可选项目列表 |
| wolf | | 1.10.2 | games | 1.10 | 社区游戏 |

- 点击 Source 进行安装。
- 软件开始下载。
- 在文本字段中输入 games。
- 从下拉菜单中选择 Category。
- 出现可下载的游戏列表。

## 安装库

你可以为个人使用或为软件应用程序安装系统库。虽然 Mac OS X 是一个功能极其强大的操作系统，但仍有许多库可以下载以增加你系统功能的。你下载并安装的工具通常需要这些库中的某些。

你安装库的方式与安装其它软件相同，这些软件通常是单单二进制文件。当你将这些文件放置在各种路径的正确位置时，其他软件就可以通过调用各种例程来使用它们。例如，如果你安装了一个用于显示 PNG 格式图像的库，你就不需要将这些例程构建到你的代码中。相反，你可以在代码中使用这些库，并在编译软件时在需要时动态加载这些库。

系统库存储在 `/usr/lib` 中。按照惯例，第三方库位于 `/usr/local/lib`。你应该小心地将这些库安装在适当的目录，以便需要它们的应用程序能够找到它们。

当你在 Mac OS 系统上安装库时，请熟悉环境变量 `DYLD_LIBRARY_PATH`。该变量对于帮助你的可执行文件加载它们所需的库至关重要。如果你的所有库都没有安装在 `/usr/lib` 中，你必须将存储库的目录列表添加到 `DYLD_LIBRARY_PATH` 变量中。你可以为此变量分配一个冒号分隔的包含库的所有目录列表。对于 `tsh` 用户，你可以插入命令例如 `setenv DYLD_LIBRARY_PATH=/usr/local/lib:/lib`，将这两个目录添加到动态链接器搜索库的位置。你可以阅读 `DYLD` 的 man 页来了解更多关于动态链接器如何使用 `DYLD_LIBRARY_PATH` 作为库搜索路径的信息。

你可以通过启动 FindCommander 工具、从工具栏菜单中选择 Category，或在文本字段中输入 `libs` 来下载许多库：FindCommander 会显示它可以为你安装的库列表。

当你通过传统的 `configure-make-make install` 过程安装软件时，你可能有机会按意愿安装库。尽管如此，基本的 `make-install` 过程可能会将二进制文件安装在 `/sw/bin` 或 `/usr/local/bin` 中，但可能无法安装必要的库。阅读 README 和 INSTALL 以确定是否存在可选的 `install-lib` 步骤来处理这个问题。

下一页的表格提供了你可以在 Mac OS X 系统上安装的各种库的描述。虽然列表并不完整，但它包含了你可能发现的许多有用库。与其他应用程序一样，库会随着开发者构建和测试新版本而发生变化。

就像有库一样-.

## 安装 UNIX

### 有用的库

下面的列表包含了你可能想在 Mac OS 系统上安装的库。

| LIBRARY (库) | DESCRIPTION (描述) | LIBRARY (库) | DESCRIPTION (描述) |
|---|---|---|---|
| db3 | Berkeley 数据库 | libhttp | HTTP 客户端 |
| db4 | Berkeley 数据库 | libiconv | 字符集 |
| dtd | 动态加载 | libiodbc | ODBC |
| expat | 解析 | libpeg | JPEG |
| freetype | 字体渲染 | libpoll | 系统轮询 |
| freep2 | TrueType 渲染 | libtiff | TIFF |
| gc | 通用集合 | libgif | GIF |
| gd | 图形 | libpng | PNG |
| gdbm | dbm | libxml | XML 解析 |
| glib | GLib | libxml++ | C++ |
| gmp | 多精度算术 | libxml2 | XML 解析 |
| gnome | GNOME | libunicode | Unicode |
| gtk+ | GTK+ | pcre | 正则表达式 |
| imlib | 图像 | pdflib | PDF |
| inlib | 接口 | readline | 终端输入 |
| libnet | 网络 | | |
| libdv | DV 视频 | | |

---

## 安装 LYNX 浏览器

你可以在你的 Mac OS 系统上安装 Lynx 浏览器。Lynx 是一个纯文本浏览器，当你处于如 ssh 等纯文本环境时非常有用。作为一个纯文本浏览器，Lynx 起初看起来很奇怪，但你可能会发现它非常用，有时甚至是不可或缺的。Lynx 不会用跳动的青蛙和弹窗广告填充你的屏幕，这种工具的简单性带给你一种优势，因为它很快。Lynx 识别并显示图形的文本等效物。例如，在链接的地方，使用 [链接名称] 或 (图像名称)，如 [company_logo.gtit]。

要启动 Lynx，你可以输入 `lynx` 后跟 URL。要在文档中向前移动，你可以按下空格键。要向后移动，你可以输入字母 `b`。

```
pkg lynx version x86
lynx 2.8.4
The following package will be installed or updated:
curl -f -o http://lynx.org/lynx/release/lynx-2.8.4.tar.gz
Lynx
L
```

### 额外

你可以设置许多选项来定义 Lynx 如何为你工作。学习这些选项的最佳方法是查阅《Lynx 用户指南》。要为此，输入 `lynx localhost` 启动 Lynx。你的本地主页将显示。然后按 `help` 和 `Return`。此命令将激活 Lynx 在线帮助，并将光标定位在《Lynx 用户指南》中。当你按下 `Return` 时，将显示用户指南。你可以使用方向键在指南中移动。完成后，你可以使用左方向键返回你的主页，或输入 `q` 完全退出。

你可以使用 `lynx` 对网站进行基础故障排除。如果你在使用传统浏览器连接网站时遇到问题，可以使用 `lynx` 快速判断网站是否运行正常。由于 Lynx 忽略了图形且运行所需的资源极少，你可以非常快速地测试并显示你的网站。如果你负责一个网站，可以使用 `lynx` 检查你的网站是否上线并正常工作。

![](img/8d9b2c31cb5eb66571f0b2dfd7c634cf_216_0.png)

```
[ferro-] user$ sudo fix install lynx
# Reading package info.
Information about 769 packages read in 5 seconds.
```

```
pkg lynx --version
pkg lynx version 2.8.4-2
The following package will be installed, updated:
```

| 总计 | 已接收 | 剩余 | 平均速度 | 下载总量 | 当前 | 速度 |
|---|---|---|---|---|---|---|
| 3 195k | 3 71540 | 0 | 2321 | 00:11:27 | 00:00:25 | 485k/s |

```
- 输入 `find` 后跟一个空格。
- 系统显示 Lynx 可执行文件的安装位置。
- 输入 `lynx` 并按 `Return`。
```

Fink 使用 `curl` 下载 lynx。

## 使用 LYNX 浏览网页

你可以使用 Lynx 浏览网页。起初，Lynx 看起来可能是一个功能有限的浏览器，但随着你熟悉 Lynx，你会发现从 Web 上快速检索信息是多么有用；比启动 Internet Explorer 所需的时间更短，Lynx 就能让你的网站显示在屏幕上。

你可以像普通浏览器一样跟随链接、搜索文本并下载页面。区别在于，你不需要点击隐藏在图像下或显示为下划线文本的链接，而是通过简单的按键进行移动。当前激活的链接会亮显示。例如，颜色会反转，如果你的屏幕其他部分是白底黑字，你将看到黑色背景。

通过 Lynx，你可以使用单字母命令来导航网页。对于偶尔浏览，你只需要几个基本的导航命令，但如果你想学习 Lynx 更高级的浏览功能，可以使用 Lynx 的帮助功能来学习这些每一个单字母命令。你可以在命令行中输入 `lynx -help`。你也可以通过输入字母 `/` 来获取 Lynx 帮助，然后按 `Enter` 或你偏好的按键打开《Lynx 用户指南》，接着调出按键命令列表。

如果你发现自己在某处卡住了，或者在等待缓慢网站响应时改变了主意，可以输入 `z` 停止当前请求。此命令的作用就像点击 Internet Explorer 中的“停止”按钮。

## 使用 LYNX 浏览网页

| 终端 | 文件 | 编辑 | 滚动历史 | 字体 | 窗口 | 帮助 |
|---|---|---|---|---|---|---|
| 终端 | 文件 | 编辑 | 滚动历史 | 字体 | 窗口 | 帮助 |

```
[Lynx] user@lynx:http://www.tood.net/-stocks/sandrick/
```

```
FRAME lynx/home
```
