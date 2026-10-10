
`date` 实用工具（第 218 页）显示当前日期和时间：

```
$ date
Thu Apr  3 10:14:41 PDT 2014
```

### `touch`: 创建一个空文件

`touch` 实用工具（第 243 页）创建以你指定的参数为名称的空（零长度）文件。以下示例中，`touch` 创建 `myfile`，并且 `ls` 显示该文件的长度为零字节。

```
$ touch myfile
$ ls -l myfile
-rw-r--r--. 1 sam pubs 0 07-24 14:12 myfile
```

## 编写和执行基本 shell 脚本

shell 脚本在 Windows 下称为批处理文件，是使用 shell 命令和实用工具编写的程序。本节解释了如何编写基本的 shell 脚本。有关创建和执行 shell 脚本的更多信息，请参阅第 336 页的“编写和执行 shell 脚本”。在运行 shell 脚本之前，你必须将命令放入文件中（脚本），并告诉 Linux 该文件是可执行的。你可以使用编辑器创建文件，或者输入以下命令，该命令使用重定向来创建文件。有关使用 `cat` 和重定向创建文件的信息，请参阅第 154 页。

```
$ cat > myprog
echo This is my shell script
date
who
CONTROL-D
```

这个名为 `myprog` 的 shell 脚本包含三个命令（实用工具）：`echo`、`date` 和 `who`。输入每一行以及最后的 `RETURN` 后，按 `CONTROL-D` 告诉 shell 你已完成向文件的写入；shell 显示一个提示符。

![](img/243613168ac865b539f12460d966088e_184_0.png)

图 4-24 `man` 实用程序显示其自身信息

接下来，你需要告诉 Linux，`myprog` 是一个可执行文件。随后，`chmod` 实用程序（第 193 页）使 `myprog` 变为可读且可执行。

```
$ chmod a+x myprog
```

最后，你可以执行 `myprog` 脚本。由于 shell 查找文件的方式，你必须用点和斜杠（`./`）作为程序名称的前缀。有关绝对路径名和相对路径名的讨论，详情请参见第 149 页。在下方的例子中，shell 运行了 `myprog` 中的三个实用程序并显示它们的输出。

```
$ ./myprog
This is my shell script
Mon Jul 22 17:15:50 PDT 2013
sam pts/0
2013-07-21 13:17 (:0)
```

## 从命令行获取帮助

Linux 的发行版通常不附带纸质参考手册。然而，其在线文档一直是 Linux 的优势之一。`man`（或 `manual`）和 `info` 页面自该操作系统早期版本起就可以通过 `man` 和 `info` 实用程序访问。不出所料，随着 Linux 和互联网的不断发展，文档来源也随之扩大。本节讨论了你在使用命令行工作时查找 Linux 信息的一些地方。如果你是在图形环境中工作，请参阅第 113 页的“获取帮助”。另见附录 B。

### `man`：显示系统手册

`man`（manual）实用程序显示（`man`）系统文档页面。当你知道想要使用哪个实用程序但忘记具体如何使用时，这份文档非常有帮助。你也可以查阅 `man` 页面以获取更多关于特定主题的信息，或确定 Linux 提供哪些功能。由于系统文档中的描述通常很简练，如果你已经理解实用程序的基本功能，它们会更有用。你可以使用 `apropos` 实用程序（下一页）搜索 `man` 页面涵盖的主题。

要了解某个实用程序的更多信息，请输入命令 `man`，并将实用程序的名称作为参数。图 4-24 显示了 `man` 显示其自身信息的情况；用户在命令行中输入了 `man`。在 `man` 页面中，你可以通过输入斜杠，接着输入术语，最后按 `RETURN`（回车）键来搜索某个术语。例如，要在 `man` 页面中搜索术语 `function`，请输入 `/functionRETURN`；`man` 将突出显示所有出现的 `function` 字符串，并将光标移动到下一个出现的位置。

**`less`（分页器）** `man` 实用程序通过分页器发送其输出——通常是 `less`（第 220 页），它一次显示一屏信息。当你使用 `man` 显示手册页面时，`less` 在显示每一屏文本后，会在屏幕底部显示一个提示符 [例如，Manual page man(1) line 1...]，并等待你执行以下操作之一：

- 按 `SPACE`（空格）键显示另一屏文本。

- 按 `PAGE UP`（上页）、`PAGE DOWN`（下页）、`UP ARROW`（上箭头）或 `DOWN ARROW`（下箭头）在文本中导航。

- 按 `h`（帮助）显示 `less` 命令列表。

- 按 `q`（退出）退出 `man` 和 `less`，使 shell 显示提示符。

**手册分区** 基于 FHS（文件系统层级标准；第 189 页），Linux 系统手册和 `man` 页面分为十个部分，每个部分描述相关的工具：

1. 用户命令

2. 系统调用

3. 子例程

4. 设备

5. 文件格式

6. 游戏

7. 杂项

8. 系统管理

9. 内核

10. 新增

这种布局密切模仿了 UNIX 手册集一贯的划分方式。除非你指定了手册分区，否则 `man` 将显示你指定参数所对应的单词在手册中最早出现的位置。大多数用户在第 1、6 和 7 部分中找到所需信息；程序员和系统管理员经常需要查阅其他部分。

在某些情况下，手册包含名称相同的不同工具条目。例如，以下命令显示系统手册第 1 部分中 `crontab` 实用程序的 `man` 页面：

```
$ man crontab
```

要查看第 5 部分中 `crontab` 文件的 `man` 页面，请输入此命令：

```
$ man 5 crontab
```

前面的命令指示 `man` 只在第 5 部分查找 `man` 页面。在文档中，你可能看到该 `man` 页面被引用为 `crontab(5)`。使用 `-a` 选项可以查看给定主题的所有 `man` 页面（按 `GRETURN` 显示随后的每个 `man` 页面）。例如，输入命令 `man -a crontab` 可以查看 `crontab` 的所有 `man` 页面。

### `apropos`：搜索关键词

当你不知道执行特定任务所需的实用程序名称时，可以使用 `apropos` 配合关键词作为参数进行搜索。此实用程序在所有 `man` 页面的简短描述行中搜索该关键词，并显示包含匹配项的行。`man` 实用程序在调用时使用 `-k`（keyword）选项时，提供与 `apropos` 相同的输出。

`apropos` 使用的数据库，名为 `man-db` 或 `makewhatis`，在系统首次安装时不可用，但会由 `cron` 或 `crond` 自动构建（有关 `cron/crond` 的讨论请参阅第 607 页，手动构建此数据库的说明请参阅第 69 页）。

以下示例显示了以 `who` 为关键词调用 `apropos` 时的输出。输出包括每个实用程序的名称、包含它的手册分区以及来自 `man` 页面的简短描述。此列表包括你所需的实用程序（`who`），并标识了其他可能有用的相关工具。

```
$ apropos who
at.allow (5)      - determine who can submit jobs via at or batch
at.deny (5)       - determine who can submit jobs via at or batch
jwhois (1)        - client for the whois service
w (1)             - Show who is logged on and what they are doing.
who (1)           - show who is logged on
who (1p)          - display who is on the system
whoami (1)        - print effective userid
whos (1)          - client for the whois service
whos.jwhois (1)   - client for the whois service
```

### `whatis`

`whatis` 实用程序类似于 `apropos`，但仅查找实用程序名称的完整单词匹配：

```
$ whatis who
who (1)           - show who is logged on
who (1p)          - display who is on the system
```

![](img/243613168ac865b539f12460d966088e_187_0.png)

图 4-25 命令 `info coreutils` 显示的初始屏幕

### `info`：显示关于实用程序的信息

文本型 `info` 实用程序（www.gnu.org/software/textinfo/manual/info）是一个基于菜单的超文本系统，由 `GNU` 项目（第 3 页）开发并随 Linux 分发。它包含关于自身的教程（输入命令 `info info`）以及许多由 `GNU` 项目开发的 Linux shell、实用程序和程序的文档。图 4-25 显示了当你输入命令 `info coreutils` 时 `info` 显示的屏幕（`coreutils` 软件包包含 Linux 核心实用程序）。

#### `man` 和 `info` 显示不同的信息

> **提示** `info` 实用程序比 `man` 显示关于 `GNU` 实用程序更完整和最新的信息。当 `man` 页面显示由 `info` 涵盖的实用程序的简略信息时，`man` 页面会引用 `info`。`man` 实用程序经常显示非 GNU 实用程序可用的唯一信息。当 `info` 显示非 GNU 实用程序的信息时，它通常是 `man` 页面的副本。

由于此屏幕上的信息来自可编辑文件，你的显示可能与本节中显示的屏幕不同。当初始 `info` 屏幕显示时，你可以按以下任意按键：

- `h` 或 `?` 列出 `info` 命令

- `SPACE` 翻页显示

- `m` 后跟你想显示的菜单名称，或后跟 `SPACE` 显示菜单列表

- `q` 或 `CONTROL-C` 退出

![](img/243613168ac865b539f12460d966088e_188_0.png)

图 4-26 输入两次 /sleepreturn 后命令 info coreutils 显示的屏幕

`info` 用于描述键盘按键的符号与 `emacs` 使用的符号相同，你可能不太熟悉。例如，符号 `C-h` 等同于 `CONTROL-h`。类似地，`M-x` 表示按住 `META` 或 `ALT` 键并按 `x`。在某些系统上，你需要按 `ESCAPE` 然后按 `x` 来复制 `META-x` 的功能。

在给出命令 `info coreutils` 后，按几次 `SPACE`（空格）键翻页。输入 `/sleepRETURN` 以搜索字符串 `sleep`。当你输入 `/` 时，`info` 将光标移动到窗口的最后一行，并显示 ``Regexp search [string];``，其中 `string` 是你最后一次搜索的字符串。按 `RETURN`（回车）搜索 `string` 或输入你要搜索的字符串。输入 `sleep` 会在该行显示 `sleep`，按 `RETURN`（回车）会在 `info` 文本中显示 `sleep` 的下一个出现位置。

#### 你可能会发现 `pinfo` 比 `info` 更容易使用

> `pinfo` 实用程序类似于 `info`，但如果你不熟悉 `emacs` 编辑器命令，它更直观。此实用程序在文本环境中运行，`info` 也是如此。当 `pinfo` 可用时，它使用颜色使界面更易于使用。如果系统上未安装 `pinfo`，请按照第 534 页的说明安装 `pinfo` 包。从终端模拟器中运行 `pinfo`。

现在输入 `/RETURN`（或 `/sleepRETURN`）以搜索 `sleep` 的下一次出现，如图 4-26 所示。行左端的星号表示此条目是一个菜单项。星号后面是菜单项的名称及对该项的描述。每个菜单项都是指向描述该项的 `info` 页面的链接。要跳转到该页面，请搜索或使用 `APRO` 键将光标移动到包含该菜单项的行，然后按 `RETURN`（回车）。如图 4-26 中光标定位的那样，按 `RETURN`（回车）显示关于 `sleep` 的信息。或者，你可以在菜单命令中输入菜单项名称以查看信息：要显示信息

# 在命令行中工作

![](img/243613168ac865b539f12460d966088e_189_0.png)

> 图 4-27 `sleep` 实用程序的 `info` 页面

以 `sleep` 为例，输入命令 `m sleep`，然后按 `RETURN` 键。当你输入 `m`（代表 `menu`，菜单）时，`info` 会将光标移动到窗口的最后一行（就像你输入 `/` 时那样），并显示 ``Menu item:``（菜单项：）。输入 `sleep` 后，该行会显示 `sleep`，按下 `RETURN` 键则会显示你所指定的菜单项的信息。

图 4-27 展示了关于 `sleep` 信息的 `top node`（根节点）。`节点` 将一组信息分组，你可以通过按空格键来翻页。要显示下一个节点，请按下 `n`。要显示上一个节点，请按下 `p`。

当你阅读本书并学习新的实用程序时，你可以使用 `man` 或 `info` 来了解有关这些实用程序的更多信息。如果本地系统可以打印 PostScript 文档，你可以使用带有 `-t` 选项的 `man` 实用程序来打印手册页。例如，`man -t cat | lpr` 会打印关于 `cat` 实用程序的信息。你还可以使用 Web 浏览器显示文档，然后从浏览器中打印所需的信息。

### `--help` 选项

你可以在命令行上使用的另一个工具是 `--help` 选项。大多数 GNU 实用程序都提供 `--help` 选项，用于显示有关该实用程序的信息。非 GNU 实用程序可能会使用 `-h` 或 `--help` 选项来显示有关自身的信息。

```
$ cat --help
Usage: cat [OPTION] [FILE]...
Concatenate FILE(s), or standard input, to standard output.

-A, --show-all           equivalent to -vET
-B, --number-nonblank    number nonempty output lines, overrides -n
-E, --show-ends         display $ at end of each line
...
```

如果 `--help` 显示的信息超出了屏幕范围，请使用管道（垂直线；第 158 页）将输出通过 `less` 分页器（第 129 页）进行查看：

```
$ ls --help | less
```

## `bash` 的 `help` 命令

`bash` 的 `help` 命令显示有关 `bash`（Bourne Again Shell）命令、控制结构和其他功能的信息。在 `bash` 提示符下，输入命令 `help` 后跟你想要查询的关键字。以下是一些示例。

```
$ help help
help: help [-dms] [pattern . . .]
Display information about builtin commands.

Display brief summaries of builtin commands. If PATTERN is
specified, gives detailed help on all commands matching PATTERN,
otherwise the list of help topics is printed.
. . .

$ help echo
echo: echo [-neE] [arg . . .]
Write arguments to the standard output.

Display the ARGS on the standard output followed by a newline.
Options:
-n do not append a newline
. . .

$ help while
while: while COMMANDS; do COMMANDS; done
Execute commands as long as a test succeeds.
. . .
```

`/usr/share/doc` 目录通常包含比 `man` 或 `info` 提供的更详细且不同的有关实用程序的信息。通常，这些信息是供那些将要编译和修改该实用程序的人使用的，而不仅仅是使用者。这些目录包含数千个文件，每个文件都包含关于单独主题的信息。如下例所示，`/usr/share/doc` 中大多数目录的名称都以版本号结尾：
