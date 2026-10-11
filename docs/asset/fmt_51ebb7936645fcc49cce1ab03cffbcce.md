
属于 Tcl/Tk。接下来的三个部分描述了 `man`、`xman` 和 `tkman`，随后是关于 `man` 文件的内部结构和格式的一些信息。

## 如何使用 man

```
man [Options] [area] subject
```

`man` 在系统所有已知的 `man` 目录中搜索指定为 `subject` 的手册文件。如果指定的不是主题而是文件名（例如 `/cdrom/man/man1/abc.1`），则会显示该文件的内容。

可选的 `area` 指定会将 `man` 文本的搜索限制在一个主题区域内——例如 `man 3 print`。当不同主题区域存在多个同名文本时，这种指定是必要的。否则，`man` 只显示找到的第一个 `man` 文本。

在 UNIX 和 Linux 书中，命令以其 `man` 编号显示——例如 `find(1)`。因此，你一眼就能知道如何调用 `man`。`man` 知道 1 到 n 的主题区域。（有时，编程命令会被分配带有不同字母的额外区域）。

- 1 用户命令
- 2 系统调用
- 3 C 编程语言函数
- 4 文件格式，设备文件
- 5 配置文件
- 6 游戏
- 7 杂项
- 8 系统管理命令
- 9 内核函数
- n 新命令

如果你想阅读所有同名文本（所有主题），必须使用带有 `-a` 选项的 `man`。然后，`man` 显示找到的 `man` 文本。一旦你读完文本并按 `Q` 退出 `man`，就会显示下一个主题的 `man` 文本。

- `-a` 显示所有同名的 `man` 页。（如果不使用此选项，只会显示不同主题区域的多个同名文件中的第一个。但在某些 LINUX 发行版中，`-a` 被设置为默认值。）
- `-f keyword` 显示关键字的含义（一行文本）。此选项对应显示包含该关键字的所有可用 `man` 文本列表。然而，它不会执行全文搜索——只分析每个 `man` 文本的关键词。此选项对应 `apropos` （在 oman 中为 `SEARCH APROPOS`）。

如果 `-f` 和 `-l` 选项或 `whatis` 和 `apropos` 命令不起作用，可能意味着缺少包含 `man` 内容信息的数据库。你可以通过执行 `/usr/sbin/makewhatis` 来修复此。（该程序相当消耗 CPU 资源。）

- `-Area_list` 仅搜索指定的主题区域。如果你需要区分多个同名文本，此选项非常有用。

一旦 `man` 文本显示在屏幕上，就可以可以使用键盘快捷键在文本中进行导航（如果在 `/usr/lib/man.config` 中指定的默认显示程序较少）：

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_95_0.png)

| 快捷键 | 功能 |
|---|---|
| Home, End | 向上或向下滚动 |
| Y, E | 跳到文本行开头/结尾向上或向下 |
| U, D | 向上或向下翻页 |
| Shift+G | 跳到向前搜索的开头/结尾 |
| pattern | 向后搜索 |
| ? Shift+N | 重复搜索（向前/向后） |
| Q | 退出 |
| H | 显示带有额外快捷键的帮助文本 |

## X 版本 xman 的特殊功能

`xman` 作为后台程序运行，因此不会影响终端窗口的工作。`xman &` 显示一个小的控制窗口，当你点击“Help”按钮时，它会显示关于 `xman` 用法的帮助文本。“Manual Page”会进入一个更大的窗口，可以在其中选择所需的帮助文本。与 `man` 不同，无法在调用时将所需的帮助主题作为参数传递给 `xman`。

## xman [Options]

- `-bothshown` 将主窗口分为两个部分（主题列表和帮助文本）。
- `-notbox` 在不启动控制窗口的情况下启动 `xman`。

在主窗口中，通过“Section”菜单，可以查看每个九个主题区域的可用文本列表。通过鼠标点击来选择所需的主题。

## MAN - 所有命令的在线手册 71

| Sections | | |
|---|---|---|
| Mail | 目录：(I) 用户命令 | 手册 |
| Xortium\|X86_B54(x) | Rmail | X(x) 帮助 |
| X86_Mono\|X86_BS53(x) | X86_Jcel(x) | X86_Mach32(x) | X86_Math(x) | 退出 |
| X86_Freebdl\|Standard(x) | X86_GK64(x) | X86_B551(x) | X86_ebi(x) | 手册页 |
| X88Freebdl\|X(x) | Xortium(x) | Server(x) | | |
| apt | addintfo | afdotid | | |
| amixer | aml2kr | ametlet | | |
| aster | apres | atoba(x) | | |
| atq | autoreply | baseline | | |
| bash | bash_builtin | bc | fontof(tex) | |

## AFM2TM(I) AFM2TM(I)

### 名称

### 描述

字体（或应该）伴随着字体度文件，例如 `Times-Roman.afm`，它描述了 `Times-Roman` 的特征。使用 Tex 字体，我们需要包含类似信息的 TFM 字体。该程序用于转换 `man` 手册。

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_96_0.png)

最有趣的菜单命令是“Search”。它快速搜索并显示所需的帮助主题。当使用“Apropos”按钮停止搜索时，`man` 会显示包含搜索项的主题列表。（然而，`apropos` 搜索不是全文搜索。只搜索每个 `man` 文本的关键词。）

`xtman` 仅支持鼠标选择主题和滚动 `man` 文本。通过 Shift 和中间鼠标键可以在主题列表和显示的 `man` 文本之间切换。遗憾的是，`xtman` 的键盘快捷键与 `man` 不对应。光标无法用于滚动帮助文本。以下总结了快捷键：

| 快捷键 | 功能 |
|---|---|
| F, B | 空格键 向前或向后翻页 |
| Ctrl+S | 向前一页 |
| 1 to 4 | 向前四行 |
| xtman | 一个 |

## tkman

和 `man` 一样，`tkman` 提供了一个显示界面。一旦安装（以及其他），`tkman` 具有以下优势：

### 文档

## 72 在线文档

![](img/dbea4db79a2d1f2183ab7081a3efe6a8_97_0.png)

- 4.2 `man` 文本
- `man` 页的简单交叉引用
- 已查看文本列表
- 广泛的配置
- `man` 文本的格式

## man 内部

`man` 的中央控制文件是 `/etc/man.config`。有时 `man` 文本仅以格式形式存储（为了节省空间）——但如果需要打印文本，这是一个缺点。`xms` 的配置可以通过 `~/.mandefaults` 中的条目进行进一步修改（参见 `xmas` 手册）。

如果你指定额外的目录，`man` 将搜索以下目录：

- `/usr/man`
- `/usr/local/man`
- `/usr/X11/man`

## MAN – 所有命令的在线手册 73

这些目录中的每一个都有子目录 `manx`（x 代表 1 到 9，n），例如 `/usr/man/manx`。为了能在屏幕上显示这些文本，转换为 ASCII 格式。

## 使用 groff 格式化 man 文本

`groff` 是一个高级命令，用于控制一系列文本程序，包括用于文本的 `groff`、`eqn` 用于数学公式、`gpic` 用于插图、`tbl` 用于表格、`leleg` 用于交叉引用以及等。`groff` 程序共同构成了一个排版系统，在概念上类似于 `LaTeX`，但在格式化能力方面不那么复杂且更容易掌握。

在实践中，`groff` 程序起次要角色——有一个例外：`groff` 用于格式化 `man` 文本。因此，`man` 文本以兼容 `groff` 的语法编写。它们只有在格式化后才变成可读的 ASCII 文本。

如果 `man` 文本不仅以格式化版本存在，还以源码的形式存在，可以使用 `groff` 将该文件转换为高质量的 PostScript 文件。可以在 `man` 目录找到 `man` 源码（例如 `/usr/man/manx`）。以下命令将 `man` 源码 `groff.1` 转换为 PostScript 并在主目录下写入文件 `test.ps`：

```
$ groff /usr/man/man1/groff.1 -mandoc /book/test.ps
```

通过以下命令可以获得相同的结果（尽管控制能力范围较小）：

```
$ man -t groff > /book/test.ps
```

以下对 `groff` 的描述仅解释了将 `man` 源码转换为 `*.dvi` 或 PostScript 文件所需的选项。

### groff [options] file <destination>

`-mname`

使用 `/usr/lib/groff/tmac` 目录中的宏文件 `tmac.name`。对于 `man` 文本的转换，使用的名称必须是 `andoc`。

`-Tformat`
