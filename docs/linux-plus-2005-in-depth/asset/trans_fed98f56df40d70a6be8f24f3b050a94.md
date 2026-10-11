
## 编辑文本文件

尽管 vi 编辑器是 Linux 和 UNIX 系统上最常用的文本编辑器，但市面上还存在其他更易于使用的文本编辑器。

mcedit 编辑器（Midnight Commander 编辑器）是一个易于使用的文本编辑器，它支持正则表达式，并且允许使用鼠标来高亮文本。要使用 mcedit 编辑器编辑 project4 文件，只需在命令提示符下输入 `mcedit project4`，终端屏幕上将显示以下内容：

```
project4	[--···] 0 L: 140 1/18 0 1/583b
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache Lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth

1Help 2Save 3Mark 4Replac 5Copy 6Move 7Search 8Delete 9Pulldn 10Quit
```

请注意，你可以通过使用键盘上的功能键来访问 mcedit 的大部分功能，如屏幕底部所示（F1 = 帮助，F2 = 保存，等等）。

尽管 mcedit 是一个简单且直观的文本编辑器，但它缺乏 vi 编辑器那样的功能。vi 编辑器的一个替代方案是 GNU Emacs（Editor MACros）编辑器，它提供了与 vi 编辑器相当的功能集。要在 Emacs 编辑器中打开 project4 文件，只需输入 `emacs project4`，终端屏幕上将显示以下内容：

```
File Edit Options Buffers Tools Help
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache Lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth

-uu---\f1 project4 (fundamental)-\|i-All\|-------------------------
```

有关 GNU 项目及其目标的信息，请输入 `C-h C-p`。

Emacs 编辑器使用 **Ctrl** 键与某些字母组合来执行特殊功能，可以配合 LISP（**LISt** Processing）人工智能编程语言使用，并且支持数百个键盘功能，类似于 vi 编辑器。表 4-8 列出了在 Emacs 编辑器中使用的一些常见键盘功能。

### 表 4-8 GNU Emacs 编辑器中常用的键盘功能

| 按键 | 描述 |
| :--- | :--- |
| Ctrl+a | 将光标移动到行首 |
| Ctrl+e | 将光标移动到行尾 |
| Ctrl+h | 显示 Emacs 文档 |
| Ctrl+d | 删除当前字符 |
| Ctrl+k | 从光标位置删除到行尾的内容 |
| Esc+d | 删除当前单词 |
| Ctrl+x + Ctrl+c | 退出 Emacs 编辑器 |
| Ctrl+x + Ctrl+s | 保存当前文档 |
| Ctrl+x + Ctrl+w | 将当前文档另存为新的文件名 |
| Ctrl+x + u | 撤销最后一次更改 |

不幸的是，Emacs 编辑器不是一个容易使用的编辑器，因为用户必须记住多个键组合才能有效工作或使用高级功能；一个在 KDE 或 GNOME GUI 环境中运行的 Emacs 版本被称为 **xemacs 编辑器**，它更易于使用，因为许多功能的键组合被图形图标取代。要使用 xemacs 编辑器打开 project4 文件，只需在 KDE 或 GNOME 桌面中打开一个命令行终端，并输入 `xemacs project4`，如图 4-3 所示。

![](img/09bf13b782f71165e17bb3839040c96a_170_0.png)

图 4-3 xemacs 文本编辑器

尽管 xemacs 编辑器可能并非在所有包含 GUI 环境的发行版中都可用，但大多数 Linux 发行版中都有一个源自 UNIX 系统且易于使用的图形化编辑器：**nedit 编辑器**。在 GUI 环境的命令行终端中输入 `nedit project4` 时看到的显示效果示例如图 4-4 所示。

![](img/09bf13b782f71165e17bb3839040c96a_170_1.png)

图 4-4 nedit 文本编辑器

此外，GNOME 和 KDE GUI 环境现在都自带自己的文本编辑器（gedit 编辑器和 kedit 编辑器），它们与 nedit 相似但提供更多功能。用户在 GUI 环境的命令行终端中输入 `gedit project4` 和 `kedit project4` 时看到的显示效果示例分别如图 4-5 和图 4-6 所示。

![](img/09bf13b782f71165e17bb3839040c96a_171_0.png)

图 4-5 gedit 文本编辑器

![](img/09bf13b782f71165e17bb3839040c96a_171_1.png)

图 4-6 kedit 文本编辑器

## 章节总结

- Linux 文件系统采用分层结构，使用一系列目录来存储文件，这些目录和文件的位置可以使用绝对或相对路径名来描述。
- Linux 文件系统中可以存在许多类型的文件，例如文本文件、二进制数据、可执行程序、目录、链接文件和特殊设备文件。
- `ls` 命令可用于查看文件名，并提供广泛选项来修改此视图。
- 通配符元字符可用于在使用常见 Linux 文件命令时简化多个文件的选择。
- 文本文件是最常见的文件类型，其内容可以通过多个实用程序查看，例如 `head`、`tail`、`cat`、`tac`、`more` 和 `less`。
- 正则表达式元字符可用于与某些编程语言和文本工具实用程序（如 `grep`）配合使用，以指定特定的文本模式。
- 尽管存在许多命令行和图形化文本编辑器，`vi`（`vim`）是一个强大的双模文本编辑器，在大多数 UNIX 和 Linux 系统上都是标准配置。

## 关键术语

- **metacharacter**（元字符）— 用于表示用户主目录的元字符。
- **absolute pathname**（绝对路径名）— 从根目录开始指向特定文件或目录的完整路径名。
- **binary data file**（二进制数据文件）— 包含机器语言（二进制 1 和 0）并存储由二进制编译程序使用的信息（如常见功能和图形）的文件。
- **cat command**（cat 命令）— 用于在屏幕上显示（或连接）文本文件全部内容的 Linux 命令。
- **cd (change directory) command**（cd（更改目录）命令）— 用于在目录树中更改当前目录的 Linux 命令。
- **command mode**（命令模式）— vi 中的两种输入模式之一；它允许用户执行任何与向文档插入文本无关的可用文本编辑任务。
- **concatenation**（连接）— 将文本连接在一起以形成一个更大的整体。在 Linux 中，单词和文本字符串被连接在一起以形成显示的文件。
- **directory**（目录）— 文件系统中用于将其他文件组织成逻辑树结构的特殊文件。
- **egrep command**（egrep 命令）— grep 命令的一个变体，用于使用扩展正则表达式在文件中搜索模式。
- **Emacs (Editor MACroS) editor**（Emacs（编辑器宏）编辑器）— 一种流行且广泛使用的文本编辑器，比 *vi* 更适合文字处理；由 Richard Stallman 开发。
- **executable program**（可执行程序）— 可由 Linux 操作系统执行，在内存中作为进程运行并执行有用功能的文件。
- **fgrep command**（fgrep 命令）— grep 命令的一个变体，不允许使用正则表达式。
- **file command**（file 命令）— 用于显示指定文件名的文件类型的 Linux 命令。
- **filename**（文件名）— 赋予文件的用户友好标识符。
- **filename extension**（文件扩展名）— 跟在文件名末尾点（.）后面的一系列标识符，用于表示文件类型；文件扩展名 .txt 表示文本文件。
- **gedit editor**（gedit 编辑器）— GNOME 桌面的文本编辑器。
- **grep (Global Regular Expression Print) command**（grep（全局正则表达式打印）命令）— 使用正则表达式元字符在文件中搜索字符模式的 Linux 命令。
- **head command**（head 命令）— 显示文本文件前若干行的 Linux 命令；默认情况下，head 命令显示前 10 行。
- **home directory**（主目录）— 文件系统中专供用户存储个人文件和信息的目录。
- **insert mode**（插入模式）— *vi* 中的两种输入模式之一；它允许用户向文档插入文本，但不允许任何其他功能。
- **kedit editor**（kedit 编辑器）— KDE 桌面的文本编辑器。
- **less command**（less 命令）— 用于在终端屏幕上分页显示文本文件的 Linux 命令；用户可以使用光标键在文件中导航。
- **linked file**（链接文件）— 代表与其他文件相同数据的文件。
- **ll command**（ll 命令）— `ls -l` 命令的别名；它提供详细的文件列表。
- **log file**（日志文件）— 包含过去系统事件的文件。
- **ls command**（ls 命令）— 用于列出指定目录中文件的 Linux 命令。
- **mcedit editor (Midnight Commander Editor)**（mcedit 编辑器（午夜命令编辑器））— 一个用户友好的终端文本编辑器，支持正则表达式和计算机鼠标。
- **more command**（more 命令）— 用于在终端屏幕上分页逐行显示文本文件的 Linux 命令。
- **named pipe file**（命名管道文件）— 一个临时连接，将信息从一个内存中的命令或进程发送到另一个命令或进程；它也可以由文件系统上的一个文件来表示。
- **nedit editor**（nedit 编辑器）— 大多数 Linux 发行版中可用的常用图形化文本编辑器。

