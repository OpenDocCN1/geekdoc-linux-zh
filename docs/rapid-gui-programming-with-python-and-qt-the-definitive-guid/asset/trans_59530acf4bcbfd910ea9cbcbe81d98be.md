
图 A.6 在 Mac OS X 中设置要使用的 Python

...正在使用。如果不是，请参阅上一段；或者，输入您想使用的 Python 版本的完整名称——例如，`python2.5 con-演figure.py`。

首先必须构建 SIP，方法是在终端中输入以下内容：

```
cd $HOME/Desktop
tar xvfz sip-4.6.tar.gz
cd sip-4.6
python configure.py
make
sudo make install
```

当你在最后执行 `sudo` 命令时，系统会要求输入管理员密码（通常是你自己的密码）。现在，可以安装 PyQt 了。

```
cd $HOME/Desktop
tar xvfz PyQt-mac-gpl-4.2.tar.gz
cd PyQt-mac-gpl-4.2
python configure.py
make
sudo make install
```

同样，当你在执行 `sudo` 命令时，系统会提示输入密码。构建 PyQt 可能需要相当长的时间，因此你需要耐心。

Qt 的文档可以通过 *Qt Assistant* 访问，可以从 *Finder* 中运行它。PyQt 的文档以 HTML 格式提供在 `$HOME/Desktop/PyQt-mac-gpl-4.2/doc` 目录中。值得将其移动到一个永久位置，并在浏览器中添加一个合适的书签。它附带了许多示例；至少值得一看 PyQt 示例并运行演示。（例如，将目录更改为 `$HOME/Desktop/PyQt-mac-gpl-4.2/examples/tools/qt_demo` 并运行 `./qt_demo.py`。）

如果你下载了本书的示例，你可能想解压缩 `pyqtbook.tar.gz` 到 `$HOME` 以获取包含所有本书示例和练习模型答案的 `$HOME/pyqt` 目录，并按章节分类。在 `$HOME/pyqt` 目录中，你将找到 `mkpyqt.py` 和 `makepyqt.pvy`；你可能想将这些移动（或软链接）到 `$PATH` 上的一个目录——例如，`$HOME/bin`——以便更方便地使用。一些示例依赖于 *Qt Designer* 的 `.ui` 文件或 `.qrc` 资源文件。如何将它们转换为 Python 模块在第 207 页有说明，但为了现在的方便，最好直接执行转换：

```
cd $HOME/pyqt
./mkpyqt.py -r
```

这将转换在 `pyqt` 目录及其子目录中发现的任何 `.ui` 和 `.qrc` 文件。² 如果你更喜欢使用 GUI 工具 `makepyqt.pvy`，你可能需要点击其 More→Tool paths 选项并设置到 `pyuic4` 的路径。可能还需要设置其他工具的路径。

这就完成了 Mac OS X 的安装。如果你解压了示例，你可以转到桌面，点击 `pyqt` 目录，然后点击 `chap12` 目录，再点击 `multipedes.pvy` 以查看一个图形应用程序。如果出现不想要的终端窗口，右键点击 `multipedes.pvy`，点击“信息”对话框；将“打开方式”设置更改为正确版本的 Python Launcher，并将更改应用于所有 `.pvy` 后缀的文件。

现在你准备好在你的 Mac OS X 机器上编写和运行 PyQt 应用程序了——它们也可以在 Windows 和 Linux 上不变地运行！

### 在 Linux 和 Unix 上安装

如果你正在运行 Kubuntu（7.04 Feisty Fawn 及更高版本），你已经安装了 PyQt4！因此，你只需要安装本书的示例（见第 573 页）以及文档包 `python-doc` 和 `python-qt4-doc`。

对于没有预装 PyQt4 的 Linux 和大多数其他 Unix 系统，需要安装四个工具：Qt C++ 应用程序开发框架，Python 解释器及其附带的库，SIP 绑定工具，以及 PyQt4 本身。安装所有工具的最方便方法是根据正在使用的 Linux 或 Unix 发行版使用标准包来安装这些工具。

对于 ArchLinux、Debian、Fedora、Gentoo、Kubuntu、Pardus、Ubuntu 以及许多其他发行版，所需的组件可以作为包获得。这些可以使用 *Adopt*、*Pirut*、*apt-get*、*yum* 或系统使用的其他包管理器进行安装。对于 *PyQt4*，包通常称为 *pyqt4* 或 *PyQt4* 或 *pyqt4-dev-tools*。*PyQt4* 的文档包通常称为 *pyqt4-doc* 或 *python-qt4-doc* 或 *PyQt4-examples*。Python 的文档通常在一个名为 *python-doc* 或 *python-docs* 的包中。IDLE 通常可以在一个名为 *idle* 或 *python-tools* 的包中单独获得。如果你想要一个更强大的 IDE，*Eric4* 本身是用 *PyQt* 编写的，可以在许多流行发行版的包中获得。包管理器应该能够找出依赖关系，但如果它无法做到，你可能需要请求它安装 Python 本身，甚至可能还需要 *Qt* 和 *g++* 编译器。*Qt Designer* 可视设计工具和翻译支持工具通常单独打包——例如，在名为 *qt4-designer* 和 *qt4-dev-tools* 的包中。

如果你足够幸运，可以使用标准包进行安装，那么一旦完成，你就可以编写 *PyQt* 程序了，并且可以跳过本书示例的安装，这在第 573 页有描述。

对于旧发行版的用户、没有合适包可用或只有部分组件可用包的用户，以及那些想要手动构建以获取最新版本的用户，手动构建和安装其实相当简单。但是，如果你从源代码构建，我们做出两个假设：首先，C++ 编译器及工具链（如 *make*）已经安装并可运行；其次，你以 *root* 用户身份安装（使用 *su* 或 *sudo*），或者知道如何使用 configure 的 *--prefix* 选项在本地安装。

安装所需的文件是 *qt-x11-opensource-src-4.2.3.tar.gz*、*Python-2.5.1.tgz*、*sip-4.6.tar.gz* 和 *PyQt4-gpl-4.2.tar.gz*。本书的示例在文件 *pyqtbook.tar.gz* 中。

首先获取 *Qt*。前往 http://www.trolltech.com/developer/downloads/qt/ index 并点击 *Qt/X11 Open Source Edition* 链接，在页面底部附近，下载 *qt-x11-opensource-src-4.2.3.tar.gz*。较高的版本号，例如 4.3.1，也应该没问题。

现在是获取 Python 的时候。前往 http://www.python.org/download 然后点击当前生产版本链接，并下载其他平台源代码版本之一——例如，*Python-2.5.1.tar.gz* 或 *Python-2.5.1.tar.bz2*。我们假设你获取的是 *.tgz* 版本——后来的 *2.x* 系列版本，如 *2.5.2* 或 2.6.0，只要是生产版本（不是 alpha、beta 或 release candidates）就没问题。

必须获取的最后两个工具是 SIP 和 PyQt。前往 `http://www.riverbankcomputing.co.uk/sip/download.php` 并下载源代码包 `sip-4.6.tar.gz`，然后前往 `http://www.riverbankcomputing.co.uk/pyqt/download.php` 并下载源代码包 `PyQt-x11-gpl-4.2.tar.gz`。同样，版本号可能会更高——例如，对于 PyQt 是 4.3。

如果你想要运行书中展示的示例或查看练习的模型答案，你可以解压缩可从 `http://www.qtrac.eu/pythbook.html` 获取的 `pythbook.tar.gz` 文件。

现在所有部件都已就绪，你可以执行安装。Qt 和 Python 必须首先安装，然后是 SIP，最后是 PyQt 本身。我们假设版本是前面提到的那些，但显然，使用你下载的版本并相应调整。我们假设下载的 tarball 在 `$HOME/packages` 目录中，并且你要么在运行 `su` 后以超级用户身份执行所有操作，要么使用 `sudo` 以超级用户身份执行每个 `make install`。

首先，你需要构建 Qt。如果你使用的是 `sudo`，最后一行应该是 `sudo make install`。

```
cd $HOME/packages
tar xvfz qt-x11-opensource-src-4.2.3.tar.gz
cd qt-x11-opensource-src-4.2.3
./configure -fast -qt-sql-sqlite -no-qt3support
make install
```

`-qt-sql-sqlite` 选项将构建 SQLite 进程内数据库；这在第 15 章中使用，但如果需要可以省略。`-fast` 和 `-no-qt3support` 选项应该略微减少构建时间，但两者都可以安全地省略。如果你想查看其他可用选项，包括可以安装的数据库驱动程序，运行 `./configure` `-help`。构建 Qt 可能需要相当长的时间（从半小时到超过三个小时，取决于处理器），因为它有超过 600,000 行 C++ 代码。

Python 和 SIP 不需要那么长的时间。接下来你应该构建 Python，同样如果你使用 `sudo`，请使用 `sudo make install`（从现在开始我们将默认如此）。

```
cd $HOME/packages
tar xvzf Python-2.5.1.tgz
cd Python-2.5.1
./configure
make install
```
