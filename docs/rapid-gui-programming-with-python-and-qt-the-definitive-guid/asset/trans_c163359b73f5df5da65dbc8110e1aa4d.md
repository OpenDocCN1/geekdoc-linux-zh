
其中包括 Tcl/Tk。Python 安装完成后，安装程序可能会要求你重启——在进行 PyQt 安装之前，你应该先重启。

![](img/9bfe0a027fcc8793bb087287001100dd_579_0.png)

![](img/9bfe0a027fcc8793bb087287001100dd_579_1.png)

# 图 A.3 Windows 上的 Python 和 PyQt 安装程序

现在你可以安装 PyQt4 本身。通过双击 **PyQt-gpl-4.2-Py2.5-Qt4.2.3.exe**，或你下载的 PyQt 版本，来启动 PyQt 安装程序。安装程序的第一屏显示在图 A.3 的右侧。如果你将 Python 安装在了非标准位置，你必须在“选择安装位置”屏幕上输入正确的位置——PyQt 是作为 Python 扩展安装的，因此其库会被放置在 Python 目录中。（基于此原因，如果你将来想要卸载 Python，应该先卸载 PyQt，然后再卸载 Python。）

PyQt 是必须安装的最后一个工具，安装完成后一切即可就绪并正常工作。为了测试，请单击 开始→所有程序→PyQt GPL v4.2→Examples and Demos。这将启动标准 Qt 演示应用的 PyQt 版本。在此应用程序内部，你可以运行 PyQt 提供的许多演示应用。演示程序的源代码以及许多其他 PyQt 示例通常安装在 `C:\Program Files\PyQt4\examples`。

如果你下载了本书的示例，不妨将 `pyqtbook.zip` 解压缩到 `c:` 以获取 `c:\pyqt` 目录，该目录包含所有书中的示例，以及按章节分类的练习参考答案。在 `c:\pyqt` 目录本身中，你会找到 `mkpyqt.py` 和 `makepyqt.py`；这些实用程序在第 207 页有说明。如果你想在阅读本书之前尝试任何示例，请确保先运行 `makepyqt.py`。（运行 `makepyqt.py` 时，将其路径设置为 `c:\pyqt`，勾选其“递归”复选框，然后单击“构建”按钮。这样所有示例就准备好运行了。）

这就完成了 Windows 上的安装，对于 PyQt GUI 编程来说已经足够了。但如果你还想编写一些控制台应用程序，或者有时在控制台中运行 PyQt 应用程序（这对调试很有用），只需多几个步骤就能让这件事方便许多。

单击 开始→所有程序→附件→Windows 资源管理器。当 Windows 资源管理器运行后，导航到“我的电脑\本地磁盘 (C:)\Documents and Settings”，然后导航到包含你用户名的目录，在该目录内，导航到 Start Menu\Programs\Accessories。复制并粘贴“控制台”（或 MS-DOS 提示符）快捷方式，并将副本重命名为“控制台 (PyQt)”。右键单击新的“控制台 (PyQt)”快捷方式以编辑其属性。在“常规”页面上，将目标更改为 `cmd.exe /k C:\pyqt\pyqt.bat`。现在，当你需要一个对 PyQt 友好的控制台时，可以单击 开始→所有程序→附件→控制台 (PyQt)，出现的控制台将自动运行 `C:\pyqt\pyqt.bat`。此批处理文件仅包含两行：

```
set OMAKEQSPEC=win32-g++
path=c:\pyqt;c:\MinGW\bin;c:\Python25;c:\Python25\lib\idelib;%path%
```

你可能会喜欢使用纯文本编辑器编辑此文件，添加包含 cd 命令的第三行——例如 `cd C:\pyqt`——以便控制台在方便的目录中启动。如果你将 MinGW 或 Python 安装在了非标准位置，你本来就需要编辑此文件，以填入它们的正确路径。

现在你已准备好在你的 Windows 机器上编写和运行 PyQt 应用程序——并且它们无需修改即可在 Mac OS X 和 Linux 上运行！

# 在 Mac OS X 上安装

要在 Mac OS X 上安装 PyQt，你必须已经安装了 Xcode 工具。这是因为安装 PyQt 需要编译器和构建工具。Xcode 是一个非常大的软件包，通常随机器提供的独立开发人员光盘提供；也可以在线从 http://developer.apple.com/tools/xcode 获取。以下说明假设 Xcode 已经安装。

虽然 Mac 通常预装了一个版本的 Python，但它可能是旧版本，在这种情况下，我们建议安装一个最新版本用于 PyQt 开发。要检查 Python 版本，启动终端，输入 `python -V`；如果这打印出“Python 2.5”或更高的版本号，则无需安装新版本的 Python。

安装 PyQt 所需的文件是 `qt-mac-opensource-4.2.3.dmg`、`python-2.5.1-macosx.dmg`（除非你已经安装了 Python 2.5 或更高版本）、`sip-4.6.tar.gz` 和 `PyQt-mac-gpl-4.2.tar.gz`。书中的示例在文件 `pyqtbook.tar.gz` 中。

首先获取 Qt。前往 http://www.trolltech.com/developer/downloads/qt/index 并单击 Qt/Mac Open Source Edition 链接，在页面底部附近下载 `qt-mac-opensource-4.2.3.dmg`。较高的版本号，例如 4.3.1，也应该没问题。

如果你需要安装最新版本的 Python，前往 http://www.python.org/download 并下载适用于 Macintosh OS X 的 Python 2.5.1 版本——例如 `python-2.5.1-macosx.dmg`。较高的 2.x 系列版本，例如 2.5.2 或 2.6.0，也应该可以，前提是它们是生产发布版本（而不是 alpha、beta 或 release candidate）。

必须获取的最后两个工具是 SIP 和 PyQt。前往 http://www.riverbankcomputing.co.uk/sip/download.php 并下载源软件包 `sip-4.6.tar.gz`，然后前往 http://www.riverbankcomputing.co.uk/pyqt/download.php 并下载源软件包 `PyQt-mac-gpl-4.2.tar.gz`。同样，版本号可能会更高——例如 PyQt 的 4.3。

如果你想运行书中展示的示例或查看练习的参考答案，你可以解压可从 http://www.qttrac.eu/pyqtbook.html 获取的 `pyqtbook.tar.gz` 文件。

现在所有组件都已就位，假设 Xcode 已安装，你可以执行 PyQt 安装。必须先安装 Qt 和 Python，然后安装 SIP，最后安装 PyQt 本身。我们假设版本是前面提到的那些，但显然，请使用你下载的版本并相应调整。我们假设所有下载的文件都在桌面上，并且你知道管理员密码（通常是你自己的密码）。

![](img/9bfe0a027fcc8793bb087287001100dd_581_0.png)

首先通过双击 `qt-mac-opensource-4.2.3.dmg`（或你下载的 Qt 软件包）并遵循说明来设置 Qt。安装程序的第一屏显示在图 A.4 中。我们假设你接受所有默认设置并在标准位置安装。旧版本的 Qt 有一个未优化的构建工具，这意味着设置可能需要惊人的长时间。更新的版本有一个优化的构建工具，运行速度快得多。

![](img/9bfe0a027fcc8793bb087287001100dd_582_0.png)

图 A.5 在 Mac OS X 上安装 Python

安装 Qt 后，如果需要，现在该安装 Python 了。双击 `python-2.5.1-macosx.dmg` 或你下载的软件包。安装程序的第一屏显示在图 A.5 中。这可能会弹出一个包含 `MacPython.mpkg` 文件的新窗口——只需双击此文件即可启动安装程序，并遵循说明。与 Qt 一样，我们假设你接受默认设置并在标准位置安装。如果你已经有一个或多个旧版本的 Python，你会发现它们保持完好，并且在 `/usr/local/bin` 中增加了两个新的 Python 可执行文件及其名称（包括版本号）——例如 `python2.5` 和 `pythonw2.5`。第一个可执行文件用于终端窗口，第二个用于运行 GUI 应用程序，避免在后台不必要地弹出终端。

安装应将刚安装的 Python 版本设为默认版本。要检查，关闭所有现有的终端窗口，然后启动一个新的终端窗口，并输入 `python -V`。如果版本不是刚安装的版本，则需要手动更改设置。关闭终端，然后在 Finder 中，前往 应用程序→MacPython 2.5，并启动 Python Launcher。打开偏好设置对话框（如图 A.6 所示），对于“文件类型设置”组合框中的每个条目——Python 脚本、Python GUI 脚本和 Python 字节码文档——更改 Python 版本。对于 Python 脚本和 Python 字节码文档条目，更改为 `/usr/local/bin/python2.5`（对于 Python GUI 脚本条目，更改为 `/usr/local/bin/pythonw2.5`（注意可执行文件名称中的“w”）。这些值可能无法在下拉列表中找到，在这种情况下必须手动输入。对于每个条目，也要确保取消勾选“在终端窗口中运行”复选框。

SIP 和 PyQt 都必须在终端中构建。关闭所有打开的终端，然后启动一个新的。输入 `python -V` 以确保使用的是正确的 Python。
