
现在，当您按 Enter 键换新行时，vim 会返回到您缩进的列（使用 `Tab` 键）。

您可以在 `.vimrc` 文件中看到许多选项——可能需要写一整本书才能描述所有的它们。位于 `http://newbiedoc.sourceforge.net/tutorials/vim/index-vim.html` 上的一个优秀教程可以提供帮助。

在 `.tuxfiles.org/linuxhelper/vimcheat.html` 和 `www.fprintf.net/vimCheatSheet.html` 也有参考性的“速查表”。

# 退出 vim

要退出 vim，您需要使用 `:q` 命令。只要您已经保存了工作（即所有缓冲区都已写入磁盘），这将退出会话。

如果您想保存并退出当前文件到磁盘，请使用 `:wq`。这只有在您为正在操作的文件分配了文件名时才有效。如果没有，您将收到错误消息。为了解决这个问题，您可以通过 `:wq filename` 将要保存的文件名传递给它。在本节之前使用的示例文件的情况下，输入 `:wq /home/justin/mynewfile` 将成功保存文件并干净退出。

要在不保存文件的情况下退出 vim，可以使用 `:q!`。使用此命令，您不会被要求确认，并将立即退出 vim。请谨慎。

# emacs

vim 和 emacs 在哲学和用户体验方面存在强烈的对比。虽然 vim 本质上是小而高效的，但 emacs 宏大而强大的。许多人发现 vim 最苦恼的是需要在命令模式和文本模式之间切换。emacs 的运行方式不同；您可以通过 `Ctrl` 和 `Meta` 键组合使用它（在 Linux 上为 `Alt`）。在图形模式下，emacs 还拥有易于访问的菜单

# 第三部分在 SUSE Linux 中使用命令行

emacs 远不止是一个文本编辑器；它旨在成为一个完整的环境。您可以将 emacs 作为邮件客户端。您甚至可以将其作为集成开发环境（IDE）。（我们不建议这样做，它很慢且无法渲染网页，但如果您必须的话。）您需要安装 `emacs -w` 软件包。

emacs 的可以追溯到 1976 年，当时由 Richard Stallman 在 MIT 人工智能实验室开发。这个名字源于编辑器宏。关于 emacs 的信息在各种网站上都有详尽的记录，包括 emacs 网站和 `www.emacs.org`。

# 安装什么

许多令人眼花缭乱的软件包名称都带有 "emacs"。需要注意的是，SUSE 中包含了两个 emacs 软件包：`emacs` 和 `emacs`。这听起来一个用于控制台环境，另一个用于 X，但事实并非如此。

GNU emacs（名为 `emacs` 的软件包）在图形模式下也可以运行。在历史上的某个点，emacs 的开发出现了一个分支（对图形环境有更好的支持。）这个版本曾经被称为 Lucid，并且是 emacs 的祖先。在 GNU emacs 的情况下，您可以安装 `emacs` 和 `emacs-x11`，或者您可以安装 `emacs emacs-nox`。默认情况下，你会得到 `emacs-x11`，如果 `emacs` 检测到 X 正在运行，它将以图形模式启动；如果您想要文本模式版本，应该安装 `emacs-nox` 而不是 `emacs-x11`。

如果您想在系统中同时安装 `emacs` 和 `emacs`，可以独立安装 `emacs` 软件包。通常情况下，`emacs` 和 `emacs` 可以使用相同的 Lisp 文件（提供模式和额外功能）（通过一种巧妙的技巧）共享用户配置文件。

几乎关于 emacs 的说法都适用于 XEmacs。对于编辑命令和模式，所有情况下我们说的适用于两者。

# 启动 emacs

如果您从命令行启动（输入 `emacs`），那么如果 `emacs-x11` 已安装且 X 正在运行，您将看到类似图 11-8 内容。

如果您想在 xterm 或 konsole 窗口中启动 emacs，输入：

```
emacs -nw
```

`-nw` 选项（无窗口）防止它在自己的窗口中启动，并强制在 xterm 或 konsole 窗口内运行。您将看到类似图 11-9 内容。

308

# 图 11-8

在 X 中启动的 emacs

![](img/e749d3c47634a5bbb94e11699efbe992_340_0.png)

# 图 11-9

emacs-now 启动

![](img/e749d3c47634a5bbb94e11699efbe992_340_1.png)

# 在 SUSE Linux 中使用命令行

你更有可能想要通过打开特定文件来启动 emacs。要这样做，请输入以下：

```
emacs file

emacs -nw file
```
