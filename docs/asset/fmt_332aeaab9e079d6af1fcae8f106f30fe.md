
其中 `command` 是你想要运行的可执行程序，`options` 是修改命令行为的标志，而 `arguments` 是命令操作的对象。例如，`ls -F` 在 `/tmp` 目录上执行 `ls` 命令。`-F` 选项修改了 `ls` 的默认输出，在列出的目录末尾添加 `/`。参数 `/tmp` 被传递给 `ls`，告诉它你想列出 `/tmp` 的内容而不是当前工作目录。

通常，选项以两种形式出现——长形式和短形式。短形式是一个破折号 (`-`) 后跟一个或多个字符，例如 `-F`。如果你想指定多个选项，例如 `-F` 和 `-l`，你可以将它们作为单独选项传递（`-F` 或 `-l`），也可以将它们组合在一起。

- `ls -F`

有时人们更容易记住长版本，因此选项通常有一个更具可读性的替代名称。`-F` 选项的长版本是 `--classify`。命令 `ls -F` 和 `ls --classify` 是等效的。注意长版本使用双破折号。有时，选项本身需要参数才能产生意义。`width` 选项的短形式 `-w` 和长形式 `--width` 需要一个参数来设置屏幕宽度。

- `ls -w30`
- `ls --width=30`

短形式和长形式在传递参数上的差异。

## 查看信息和帮助页 (Man Pages)

传递给命令的选项和参数取决于命令本身。你需要知道传递什么才能让命令运行。许多命令会告诉你它们支持哪些选项和参数。许多命令有 `--help` 选项或 `?`。将此作为选项传递通常会打印出命令的简要用法。你通常可以依靠这些选项之一。在接下来的示例中，尽管 `?` 选项不是有效选项，但命令会告诉该使用哪个选项来获取更多信息——在这种情况下是 `--help`。

- `ls -?`
- `ls: invalid option -- ?`
- `Try 'ls --help' for more information.`
- `[jduprey@sloth]$ ls --help`
- `Usage: ls [OPTION]... [FILE]...`
- `List information about the FILES (the current directory by default).`
- `Sort entries alphabetically if none of -cftsUSX nor -sort.`

如果你已经熟悉某个命令，并且只是对获取一个有效选项和参数的列表感兴趣，这就足够了。但如果你想知道更多关于某个命令的信息呢？`man` 和 `info` 命令允许你查看文档。在文档中……（文本根据提供的 OCR 内容继续重复或片段）。

*注：提示中提供的 OCR 文本在后半部分存在大量重复和章节重启。我已根据提供的指令进行了逻辑处理。*

### 查看文本

有许多方法查看文本文件的内容。什么是文本文件？简单来说，文本文件是包含任意有效文本字符的文件。有效字符由美国标准信息交换代码 (ASCII) 标准定义。文本文件是 Linux 中非常常见的格式。大多数配置文件和文档都以标准文本格式提供。其他文档（如 HTML）采用 ASCII 编码，并依赖另一个程序（如 Web 浏览器）来解释其内容。查看和编辑文本文件是 Linux 中的一项重要任务。一种查看文本文件内容的方法是使用文本编辑器。我将在本章中讨论编辑文本文件。查看文本文件内容最简单的方法可能是使用连接命令 `cat`。`cat` 命令接收多个文本文件参数并将这些文件的内容连接起来。在最形式的形式，它将单个文本文件的内容显示在屏幕上。然而，如果文本文件的内容比屏幕大，查看起来可能会困难。

分页器（Pagers）是按页显示文本行的程序，页大小由屏幕上的行数决定。常见的分页程序有 `more` 和 `less`。`less` 的帮助页展示了回溯和显示的能力。

在加载时显示内容，而不是在文本完全加载后显示。然而，我相信 TurboLinux 附带的 `more` 版本也支持这些功能。是的，少即是多，多即是少。它们执行相同的任务。选择权在于你。让我们试一下。首先，你需要选择一个足够长的文件进行查看，以便你可以利用分页功能。在你的主目录下有一个 `.xinitrc` 配置文件。

```bash
cd ~
ls -a
.Xdefaults .bash_logout .bashrc .rosts .xinitrc
.bash_history .bash_profile .inputinput .screen .xsession
> more .xinitrc
!/bin/sh
```

# TurboLinux XINITRC，作者：Scott Stone (sstone@turbolinux.com)
# 请勿手动修改此文件。

`userresources=$HOME/.resources`
`usermap=$HOME/.Xmodmap`
`sysresources=/usr/X11/lib/X11/xinit/.Resources`
`sysmodmap=/usr/X11/lib/X11/.Xmodmap`

不要担心这个文件的内容。你将在第 19 章“配置 X Window 系统”中学习关于 `.xinitrc` 的所有知识。表 7-1 描述了你在 `more` 或 `less` 中可以使用的关键控制命令。

# 表 7-1
more 或 less 中的操作键命令

| 键命令 | 说明 |
| :--- | :--- |
| 上方向键，Ctrl+B | 向上移动一行 |
| PageUp | 向上滚动一页 |
| `<number>`+J | 滚动 `<number>` 行，若未指定 `<number>` 则默认为 1 |
| M+`<character>` | 用 `<character>` 标记该行 |
| '+'`<character>` | 跳到标记有 `<character>` 的行 |
| `<number>`+`<regular expression>` | 查找匹配 `<regular expression>` 的字符串的第 `<number>` 个匹配项 |

表 7-1 中的 `<number>` 应该替换为任何正整数，例如 1、2 或 3。`<character>` 符号应替换为任何有效字符。`<regular expression>` 符号应替换为任何有效的正则表达式。你可能并不熟悉正则表达式。正则表达式语法用于表示字符模式。在最简单的形式下，正则表达式就是你想要匹配的简单字符字符串。我将在下一节中解释正则表达式的语法。

尝试查看非 ASCII 文件可能是一次痛苦的经历。二进制文件（如程序）由 ASCII 字符组成，因此无法在终端中查看。如果你不确定一个文件是否为 ASCII 文本文件，可以使用 `file` 命令确定其类型。任何基于文本的文件都可以查看。

```bash
> file .xinitrc
.xinitrc: Bourne shell script text
> file /etc/hosts
/etc/hosts: ASCII text
```
