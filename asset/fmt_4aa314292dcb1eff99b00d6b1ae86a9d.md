
`列表 4.31` 显示该 `CentOS` 发行版将 `vi` 命令指向 `vim` 命令。因此，对于该发行版，`vi` 和 `vim` 命令都会启动 `vim` 编辑器。

某些发行版（如 `Ubuntu`）默认没有安装 `vim` 编辑器。相反，它们使用一个名为 `vim.tiny` 的替代品，它不会允许你尝试这里讨论的所有各种 `vim` 命令。你可以通过获取 `vim` 程序的文件名来检查你的发行版是否安装了 `vim`。输入 `type vi` 并按回车，如果得到错误或别名，则输入 `type vim`。一旦收到程序的目录和文件名，输入命令 `readlink -f` 后面跟目录和文件名。例如：`readlink -f /usr/bin/vi`。如果你看到 `/usr/bin/vi.tiny`，你需要切换到不同的发行版来练习 `vim` 命令，或者安装 `vim` 包（第 13 章）。

要开始使用 `vim` 编辑器，根据你的发行版输入 `vim` 或 `vi`，后跟你想要编辑或创建的文件名。`图 4.2` 显示了一个 `vim` 文本编辑器

## 图 4.2 使用 vim 编辑器

![](img/0c1e7d2699b9d354c8d2f84669d18d73_162_0.png)

在 `图 4.2` 中，编辑的文件是 `numbers.txt`。`vim` 编辑器在底部有一个状态栏，显示你打开了新文件。`vim` 编辑器有三种标准模式：

`命令模式`这是你进入编辑器时所处的模式，有时称为普通模式。在这里你可以输入命令。

`插入模式`插入模式也称为编辑模式。这是你输入文本的模式。

`Ex 模式`这种模式通过在命令模式下按下冒号进入。它允许命令行编辑。例如，要保存文件，输入 `:w`。要退出，输入 `:q`。

`命令行`命令行位于屏幕底部。这是你输入命令的地方。

# 第 4 章 ■ 文本的搜索与分析

某些发行版默认安装了 `vim` 教程。这是学习使用 `vim` 编辑器的方便方法。要开始，只需在命令行中输入 `vim tutor` 即可。如果你需要在教程完成之前离开，只需输入 `Ex` 模式下的命令 `q` 退出即可。

只学习一个文本编辑器而忽略其他的是很有诱惑力的。当然，这并不会对你通过 `CompTIA Linux+` 认证考试有帮助。但是，至少知道两个文本编辑器对你的日常 `Linux` 工作是有用的。对于简单的修改，`nano` 文本编辑器表现出色。对于更复杂的编辑，`vim` 编辑器是王者。两者都值得你花时间去掌握。

# 学习流式编辑器

有时你可能希望在不调出标记文本编辑器的情况下编辑文本文件。在这种情况下

我们将探索的第一个流式编辑器是流式编辑器（`stream editor`）。调用它的命令是 `sed`。该编辑器根据你提前提供的一系列命令来编辑数据。它是一个快速编辑器，因为它只对文本进行一次遍历完成修改。

`sed` 编辑器根据命令行输入的命令或存储在文本文件中命令来更改数据。处理过程如下：

- 从输入流中一次读取一行
- 将提供的编辑器命令与文本进行匹配
- 按命令指定的修改文本
- 将修改后的文本输出到 `STDOUT`（标准输出）

在 `sed` 编辑器对某行文本执行了所有预定义的命令后，它会读取下一行并重复编辑过程。一旦 `sed` 到达文本行的末尾，它就会停止。

在查看一些示例之前，理解命令的基本语法是重要的。它如下：
`sed [OPTIONS] [SCRIPT]... [FILENAME]`

默认情况下，`sed` 将使用来自 `STDIN` 的文本根据命令进行修改。`列表 4.32` 显示了一个示例。

### 列表 4.32：使用 sed 修改 STDIN 文本

```bash
$ echo "I like cake." | sed 's/cake/donuts/'
like donuts.
$
```

注意 `列表 4.32`，`echo` 命令的文本输出被管道作为输入到流式编辑器。`sed` 工具的 `s` 命令（`substitute`，替换）指定如果找到第一个字符串 `cake`，则在输出中将其更改为 `donuts`。注意，`sed` 之后的整个命令被视为 `SCRIPT`（脚本），并被封装在单引号中。还要注意，文本单词通过斜杠（`/`）与命令、引号以及彼此隔开。

记住，仅使用 `s` 命令不会更改文本流中单词的所有实例。`列表 4.33` 显示了此的一个示例。

### 列表 4.33：使用 sed 全局修改 STDIN

```bash
$ echo "I love cake and more cake." | sed 's/cake/donuts/'
love donuts and more cake.
$

$ echo "I love cake and more cake." | sed 's/cake/donuts/g'
I love donuts and more cake.
$
```

在 `列表 4.33` 中，只有单词 `cake` 的第一次出现被修改了。然而，在第二个命令中，`sed` 脚本末尾添加了 `g`，它代表全局（`global`）。这导致所有 `cake` 的出现都更改为了 `donuts`。
你也可以修改存储在文件中的文本。`列表 4.34` 显示了此的一个示例。

### 列表 4.34：使用 sed 修改文件文本

```bash
$ cat cake.txt
Christine likes chocolate cake.
Rich likes lemon cake.
Tim only likes yellow cake.
Samantha does not like cake.
$

$ sed 's/cake/donuts/' cake.txt
Christine likes chocolate donuts.
Rich likes lemon donuts.
Tim only likes yellow donuts.
Samantha does not like donuts.
$

$ cat cake.txt
Christine likes chocolate cake.
Rich likes lemon cake.
Tim only likes yellow cake.
Samantha does not like cake.
$
```

在 `列表 4.34` 中，文件包含含有单词 `cake` 的文本行。当 `cake.txt` 文件作为参数添加到 `sed` 命令时，其数据根据脚本被修改。注意文件中的数据并没有被修改。流式编辑器仅将修改后的文本显示到 `STDOUT`。

流式编辑器有一些常用的命令选项。常用的选项显示在 `表 4.10` 中。

## 表 4.10：sed 命令常用选项

| 短格式 | 长格式 | 描述 |
| :--- | :--- | :--- |
| `-e` | `--expression` | 向脚本添加命令。 |
| `-f` | `--file` | 使用来自文件的脚本。 |
| `-r` | `--regexp` | 使用扩展表达式。 |

一个实用的选项是 `-e`。在查看一些示例之前，理解命令的基本语法是重要的。它如下：
`sed [OPTIONS] [SCRIPT]... [FILENAME]`

默认情况下，`sed` 将使用来自 `STDIN` 的文本根据命令进行修改。`列表 4.32` 显示了一个示例。

### 列表 4.32：使用 sed 修改 STDIN 文本

```bash
$ echo "I like cake." | sed 's/cake/donuts/'
like donuts.
$
```

注意 `列表 4.32`，`echo` 命令的文本输出被管道作为输入到流式编辑器。`sed` 工具的 `s` 命令（`substitute`，替换）指定如果找到第一个字符串 `cake`，则在输出中将其更改为 `donuts`。注意，`sed` 之后的整个命令被视为 `SCRIPT`（脚本），并被封装在单引号中。还要注意，文本单词通过斜杠（`/`）与命令、引号以及彼此隔开。

记住，仅使用 `s` 命令不会更改文本流中单词的所有实例。`列表 4.33` 显示了此的一个示例。

### 列表 4.33：使用 sed 全局修改 STDIN

```bash
$ echo "I love cake and more cake." | sed 's/cake/donuts/'
love donuts and more cake.
$

$ echo "I love cake and more cake." | sed 's/cake/donuts/g'
I love donuts and more cake.
$
```

在 `列表 4.33` 中，只有单词 `cake` 的第一次出现被修改了。然而，在第二个命令中，`sed` 脚本末尾添加了 `g`，它代表全局（`global`）。这导致所有 `cake` 的出现都更改为了 `donuts`。
你也可以修改存储在文件中的文本。`列表 4.34` 显示了此的一个示例。

### 列表 4.34：使用 sed 修改文件文本

```bash
$ cat cake.txt
Christine likes chocolate cake.
Rich likes lemon cake.
Tim only likes yellow cake.
Samantha does not like cake.
$
```
