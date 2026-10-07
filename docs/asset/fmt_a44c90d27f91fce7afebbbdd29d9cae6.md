
这是关于 Unix 和 Windows 文件系统的最后一点。在 Unix 路径中使用斜杠符号 `/` 分隔目录和文件。当你处理 Windows 路径时，使用反斜杠 `\`。

### 文件系统导航命令

我们准备好学习第一批 Bash 命令了。执行 shell 命令的步骤如下：

1. 使终端窗口激活。
2. 输入命令。
3. 按回车键。

shell 将处理你的输入。

当 shell 忙碌时，它无法处理你的输入。你可以通过命令提示符来区分 shell 的状态。它是一个或多个字符的序列。默认提示符是 `$`。

> 179https://en.wikipedia.org/wiki/Case_sensitivity

180https://en.wikipedia.org/wiki/Command_prompt

Bash 壳

符号 `$` 是提示符。你可以在图 2-4 中看到它。Windows 允许执行以下操作：

- 显示当前目录。
- 到指定的目录。
- 查找文件或目录。

你可以在 Windows 中这样做。表 2-1 显示了这些命令。

表 2-1. 命令与工具

| 命令 | 说明 | 示例 |
| :--- | :--- | :--- |
| `ls` | 显示目录的内容。如果你不带参数调用命令，它显示当前目录。 | `ls /c/Windows` |
| `pwd` | 显示当前目录的路径。如果你加上 `-w` 参数，它显示 Windows 中的路径。 | `pwd` |
| `cd` | 进入指定的相对或绝对路径。 | `cd /c/Windows` |
| `mount` | 将磁盘挂载到根目录。如果你不带参数调用命令，它显示已挂载磁盘。 | `mount` |
| `find` | 查找文件或目录。第一个参数指定搜索目录。 | `find -name vim /c/Windows` |
| `grep` | 通过内容查找文件。 | `grep "PATH" .` |

Bash 只能执行 `pwd` 和 `cd` 命令。它们被称为内置命令⁸。MSYS2 环境提供了一组 GNU 工具。这些是高度专门化的程序。

> ¹⁸https://www.gnu.org/software/bash/manual/html_node/Builtins.html

- `ls`
- `mount`
- `find`
- `grep`

让我们考虑表 2-1 中的命令。我们刚刚启动了终端。我们第一件事是确定当前目录。你可以从命令提示符获取它，但这取决于你的 Bash 配置。你在 Linux 和 macOS 中没有启用此功能。

当你启动终端时，它打开当前用户的主目录。Bash 将其缩写为波号 `~`。你在提示符前看到这个符号。使用波号代替主目录的绝对路径。这让你的命令更短。

调用 `pwd` 命令获取当前目录。图 2-7 显示了此调用及其输出。命令打印用户主目录的绝对路径。在我的情况下，它是 `/home/ilya.shpigor`。

如果你在调用时加上 `-w` 选项，命令将打印 Windows 目录结构中的路径。当你在 MSYS2 环境创建一个文件并在 Windows 中打开它时，这非常有用。图 2-7 显示了应用 `-w` 选项的结果。

![](img/10069385f0665422da9fa132eaf1027c_58_0.png)

图 2-7. `pwd` 命令的输出

# Bash Shell

什么是命令行选项？当程序只有 CLI（命令行界面）时，你与它交互的方式非常有限。程序需要一些输入数据来执行工作。Shell 为你提供了一种传递这些数据的简单方法。只需在命令名后输入它们即可。这些数据被称为程序的参数。Bash 术语将参数分为两类：参数（parameter）和选项（option）。选项是用于切换程序模式的参数。标准规定了选项的格式。它是以单横杠 `-` 或双横杠 `--` 开头的单词或字符。

你以相同的方式向 CLI 程序和 Bash 内置命令传递数据。使用参数和选项来实现。

长命令很不方便。Bash 提供了自动补全功能来节省你的时间。以下是使用它的步骤：

- 输入命令的前几个字母。
- 按 Tab 键。
- 如果 Bash 找到了你想要的命令，它会自动完成补全。
- 如果有多个命令以输入的字母开头，则不会发生补全。再次按 Tab 可以这些命令的列表。

图 2-8 显示了自动补全功能的工作原理。假设你输入了单词 "pw"。然后按了两次 Tab 键。Bash 向你显示以 "pwd" 开头的命令，如图 2-8 所示。

![](img/10069385f0665422da9fa132eaf1027c_59_0.png)

图 2-8. `pw` 命令的自动补全

> 182} https://en.wikipedia.org/wiki/Command-line_interface#Arguments

## ls

我们通过使用 `pwd` 命令获取当前目录。下一步是检查目录内容。`ls` 工具就负责此任务。

假设你刚刚安装了 MSYS2 环境。然后你第一次启动了终端。你处于用户主目录。在那里调用 `ls` 命令。图 2-9 显示了它的结果。命令输出为空。这说明该目录为空，或者只有隐藏文件和目录。

![](img/10069385f0665422da9fa132eaf1027c_60_0.png)

图 2-9. `ls` 工具的输出

Windows 有隐藏文件和目录的概念。Unix 环境也有如此。应用程序和操作系统会根据需要创建隐藏文件。这些文件存储了配置和临时数据。

Windows 资源管理器默认不显示隐藏文件和目录。更改资源管理器设置即可查看它们。

你可以通过更改属性在 Windows 中隐藏文件。如果你想在 Unix 中执行相同操作，应该在文件名开头添加一个点。

当你不带参数启动 `ls` 工具时，它不会显示隐藏对象。你可以添加 `-a` 选项来查看它们。图 2-9 显示了此类调的结果。

`ls` 工具可以显示指定目录的内容。将目录的绝对路径或相对路径传递给工具。例如，以下命令显示根目录的内容：

`ls /`

图 2-10 显示了该命令的输出。

```
ilya.shpigor@DESKTOP-1NBVMQM4 MSYS ~
$ ls /
autorebase.bat   mainenactool.dat msys2.exe
bin               mainenactool.exe msys2.ico
components.xml    mainenactool.ini msys2.ini
dev               mingw32          msys2_shell.cmd
dir               mingw32.ini      network.xml
etc             mingw32.ini      proc
home             mingw64          tmp
InstallationLog.txt mingw64.exe usr
installer.dat    mingw64.ini
$ |
```

图 2-10. `ls` 工具的输出

图 2-10 中没有 `/c` 和 `/d` 目录。根据列表 2-2，这些是 C 盘和 D 盘驱动器的挂载点。挂载点在根目录下。为什么 `ls` 工具没有打印它们呢？这是因为 Windows 文件系统没有挂载点的概念。因此，它没有 `/c` 和 `/d` 目录。它们只在 Unix 环境中存在。这些并不是你可以访问磁盘文件系统的真实目录路径。`ls` 工具读取 Windows 文件系统的目录内容。因此，它不显示挂载点。`ls` 工具在 Linux 和 macOS 中的行为不同。它们能正确显示挂载点。

## mount

如果你的电脑有多个磁盘驱动器，你可以读取它们的挂载点。不带参数调用 `mount` 工具即可实现。图 2-11 显示了它的输出。

> ¹184* https://en.wikipedia.org/wiki/Mount_(Unix)

![](img/10069385f0665422da9fa132eaf1027c_62_0.png)

图 2-11. `mount` 工具的输出

将此输出视为一个四列的表格。这些列显示以下值：

1. 磁盘驱动器、其分区或目录。它是操作系统挂载到根目录的实体。
2. 挂载点。你可以访问挂载磁盘驱动器的路径。
3. 磁盘驱动器的文件系统类型。
4. 挂载参数。例如对磁盘内容的访问权限。

如果我们将 `mount` 输出拆分为这些列，就会得到表 2-2。

| 已挂载分区 | 挂载点 | 文件系统类型 | 挂载参数 |
| --- | --- | --- | --- |
| `C:/msys64` | `/` | `ntfs` | `binary,auto` |
| `C:/msys64/usr/bin` | `/bin` | `ntfs` | `binary,auto` |
| `C:` | `/c` | `ntfs` | `binary,0,noumount` |
| `Z:` | `/z` | `hfs` | `binary,0,noumount` |

表 2-2. `mount` 工具的输出。

这会让 Windows 用户困惑。MSYS2 挂载了 `C:/msys64`。

## cd

`cd` 命令成功后不会输出任何内容。它更改当前目录。你可以在提示符上方看到新路径。相对路径更短，因此输入得更快。在导航文件系统时优先使用它们。

## Bash Shell（续）

> [185] https://en.wikipedia.org/wiki/Shortcut_(computing)

## cd

有一个简单的规则可以区分路径类型。绝对路径以斜杠 `/` 开头。例如 `/c/Windows/system32`。相对路径以目录名开头。例如 `Windows/system32`。

现在你在 `/usr` 目录。你可以获取目录列表并进入。假设你想向上一级到达根目录。有两种方法：进入绝对路径 `/` 或特殊的相对路径 `..`。`..` 指向当前目录的父目录。以此方式调用 `cd`：

```bash
cd ..
```

> 除了 `..` 还有另一个特殊路径 `.`。它指向当前目录。如果你执行命令 `cd .` 则不会发生任何事情。你停留在原地。你需要路径来运行当前目录下的程序。

回到 `/usr` 目录。然后在那里运行 `ls` 工具。它会显示子目录。进入该目录并再次调用 `ls`。你会发现那里有一个 `doc` 目录。它包含了 Bash 文档。以此方式调用 `cd` 命令到达文档：

```bash
cd doc/bash
```

你现在位于 `/usr/share/doc/bash` 目录。在那里调用 `ls` 工具。它会为你显示多个文件。其中之一是 `README`。它包含了 Bash 解释器的简要描述。

你找到了文档文件。下一步是打印它的内容。`cat` 工具可以做到。这里有一个运行它的示例：

```bash
cat README
```

图 2-13 显示了调用 `cat` 后的终端窗口。

# Bash Shell

```bash
bash-maintainers@
while the Bash maintainers do not promise to fix all bugs, we would
like this shell to be the best that we can make it.

Enjoy!
chet Ramey
chet.rame@case.edu

Copying and distribution of this file, with or without modification,
are permitted in any medium without royalty the copyright
notice and this notice are preserved. This file is offered as-is,
without any warranty.
$ilya.shipgor@DESKT-INBQ4M MSYS /usr/share/doc/bash
```

图-13. `cat` 工具的结果

某些 Bash 手册并不建议使用 `cat` 工具打印文件。它们认为该工具的目的是合并多个文件并打印结果。手册建议将 `echo` 命令与流重定向结合使用。以下是这种方法的用示例：

```
echo "$(< README.txt)
```

`README` 文件的内容并不适应终端窗口。因此，你在图 2-13 中看到了文件的尾部。使用窗口右侧的滚动条查看文件的头部。此外，还可以使用 `Shift+PageUp` 和 `Shift+PageDown` 快捷键向上或向下翻页。`Shift+↑` 和 `Shift+↓` 键可以上下滚动行。

## 命令历史

每当你调用一个命令时，Bash 都会将其保存在命令历史中。你可以通过上下方向键来浏览历史记录。Bash 会自动输入对应的命令。你只需要按回车键启动它。例如，如果你调用过“`cat README`”命令，按向上方向键并按回车即可重复执行。

`Ctrl+R` 快捷键可以触发所有命令历史的搜索。按下 `Ctrl+R` 并开始输入。Bash 将向你显示以这些字符开头的最后一个命令。按回车执行。`history` 命令显示整个历史。通过这种方式不带参数运行它：

### history

历史记录存储了你执行过的命令。它不会保留你输入后删除的命令。

有一个技巧可以在不执行命令的情况下将命令保存到历史记录中。在命令前添加哈号符号 `#` 并按回车。Bash 会存储输入的这一行，但不会执行它。这是因为哈号符号表示注释。当解释器遇到注释时，它会忽略这一行。然而，Bash 在历史记录中保留了注释行，因为它们是该语言合法的构造。

以下是针对我们的 `cat` 命令调用的注释技巧示例：

```bash
#cat README
```

你已经将注释过的命令保存到历史记录中。现在你可以通过按方向键在那里找到它。删除行开头的哈符号并按回车。Bash 将执行你的命令。

你可以通过 `Alt+Shift+3` 快捷键执行注释技巧。它在大多数终端模拟器中有效。使用该快捷键的步骤如下：

- 1. 输入命令，但不要按回车。
- 2. 按 `Alt+Shift+3`。
- 3. Bash 将命令保存到历史记录中而不执行它。

有时你需要从终端窗口复制文本。这可以是命令，也可以是它的输出。这是一个示例。假设某些文档需要 Bash README 文件的一部分。使用剪贴板复制它。剪贴板是文本数据的临时存储区域。当你用鼠标在终端窗口中选择内容时，剪贴板会自动保存。你可以将这些数据粘贴到任何其他窗口。

从终端窗口复制文本的步骤如下：

- 1. 使用鼠标选择文本。按住左鼠标键并将光标拖过所需的文本。
- 2. 点击鼠标中间键，将剪贴板中的文本粘贴到相同或另一个终端窗口。你会在当前光标位置插入文本。
- 3. 右键点击并选择“粘贴”项，将文本粘贴到终端以外的应用程序中。

## find

使用 `cd` 和 `ls` 命令搜索文件或目录是不方便的。特殊的 `find` 工具完成得更好。

如果你不带任何参数运行 `find` 工具，它会遍历当前目录的内容并打印出来。图 2-14 显示了在主目录下运行 `find` 的结果。

![](img/10069385f0665422da9fa132eaf1027c_67_0.png)

图 2-14. `find` 工具的输出

`find` 的第一个参数是要搜索的目录。该工具接受相对路径和绝对路径。例如，以下命令显示根目录的内容：

```bash
find /
```

你可以从第二个参数开始指定搜索条件。如果发现的对象不符合这些条件，`find` 就不会打印它。条件形成一个表达式。该工具有一个嵌入的解释器来处理该表达式。

`find` 条件的一个示例是特定的文件名。当你带有此类条件调用工具时，它只会打印具有此名称的文件。

表 2-3 显示了 `find` 工具常用条件的格式。

### 表 2-3. find 工具的常用条件

| 条件 | 含义 | 示例 |
| --- | --- | --- |
| `-type f` | 仅搜索文件。 | `find -type f` |
| `-type d` | 搜索目录。 | `find -type d` |
| `-name <pattern>` | 搜索名称匹配通配符模式的文件或目录。模式区分大小。 | `find -name README` `find -name READ*` `find -name READ??` |
| `-iname <pattern>` | 搜索名称匹配通配符模式的文件或目录。模式不区分大小。 | `find -iname readme` |
| `-path <pattern>` | 搜索路径匹配通配符模式的文件或目录。模式区分大小。 | `find -path */` |
| `-ipath <pattern>` | 搜索路径匹配通配符模式的文件或目录。模式不区分大小。 | `find -ipath */` |
| `-a` | 逻辑与（AND）。如果发现的对象符合所有条件，工具就会打印它。 | `find -name README -a -path */` |
| `-o` | 逻辑或（OR）。如果发现的对象至少符合一个条件，工具就会打印它。 | `find -name README -o -path */` |
| `!` | 条件的逻辑非（NOT）。如果对象不符合条件，工具就会打印它。 | `find -name README` |

方括号表示特定位置的字符集。例如，模式 `[cb]at.txt`  `cat.txt` 和 `bat.txt` 文件。你可以通过这种方式将模式应用于 `find` 调用：

```bash
find -name "[cb]at.txt"
```

练习 2-1. 通配符

哪些行对应模式 `*ME?`？

- `0_README.txt`
- `README`
- `README.md`

练习 2-2. 通配符

哪些行对应模式 `*/doc?openssl*`？

- `/usr/share/doc/openssl/IPAddress_new.html`
- `/usr/share/doc_openssl/IPAddress_new.html`
- `doc/openssl`
- `/doc/openssl`

让我们将通配符实践。假设你不知道 Bash README 文件的位置。在这种情况下，你应该使用 `find` 工具。从根目录开始使用工具搜索。现在你需要一个搜索条件。在 Unix 中，将文档存储在 `doc` 目录是常见做法。因此，你可以仅搜索这些目录。这样你得到了下面的 `find` 调用：

```bash
find /path */doc/*
```
