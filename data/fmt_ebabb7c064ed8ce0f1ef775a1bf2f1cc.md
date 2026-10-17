
| 按键 | 功能 | 按键 | 功能 |
| :--- | :--- | :--- | :--- |
| `CTRL + O` | 保存 | `CTRL + X` | 退出 |
| `CTRL + G` | 帮助 | `ESC + X` | 切换菜单显示 |
| `Page Up` | 上一页 | `Page Down` | 下一页 |
| `ESC + d` | 显示单词计数 | `CTRL + C` | 复制当前位置 |
| `CTRL + K` | 剪切当前行 | `ESC + 6` | 复制当前行 |
| `CTRL + U` | 粘贴 | `CTRL + \` | 查找和替换 |
| `CTRL + W` | 搜索 | `CTRL + -` | 跳转到行 |
| `CTRL + A` | 跳转到行首 | `CTRL + E` | 跳转到行尾 |
| `ESC + \` | 跳转到文件第一行 | `ESC + /` | 跳转到文件最后一行 |

> **注意** 在某些系统上，可能使用 `pico` 编辑器代替 `nano`。

**常见用法示例：**

- `nano [FILE]` 打开指定文件进行编辑
- `nano -v [FILE]` 以只读模式打开指定文件

### vi / vim

**用途：** 功能齐全的文本编辑器。

**用法语法：** `vi/vim [OPTIONS] [FILE]`

```
$ vim ShoppingList.txt
Milk
Eggs
Cheese
Tacos
~
~
~
~
~
~
~
~/home/nick/ShoppingList.txt" 4 lines, 19 characters
使用 vi 编辑文本文件
```

`vi` 编辑器（也称为 `vim`）是一个针对 Unix、Linux 和 BSD 系统的复杂且功能齐全的文本编辑器。传统 Unix 系统通常将 `vi` 用作默认文本编辑器。现代 Linux 和 BSD 系统使用 `vim`，它是 `vi` 的增强版本。

`vi` 和 `vim` 编辑器有两种基本操作模式：命令模式和编辑模式。在键盘上按下 `Esc` 激活命令模式。在命令模式下，可以使用命令键来激活特定的编辑功能。下表列出了 `vi` 和 `vim` 中最常用的命令。

| 按键 | 功能 | 按键 | 功能 |
| :--- | :--- | :--- | :--- |
| `:w` | 保存 | `A` | 在光标后附加文本 |
| `:x` | 保存并退出 | `r` | 替换光标前的文本 |
| `:q` | 退出 | `R` | 替换光标后的文本 |
| `i` | 在光标前插入文本 | `YY` | 复制当前行 |
| `I` | 在行首插入文本 | `p` | 粘贴复制的文本 |
| `a` | 在光标后追加文本 | `/ [TEXT]` | 搜索指定文本 |

vi 和 vim 的命令键

**常见用法示例：**

- `vi [FILE]` 使用 vi 打开指定文件进行编辑
- `vim [FILE]` 使用 vim 打开指定文件进行编辑
- `view [FILE]` 以只读模式打开指定文件

### Emacs

**用途**：健壮且可扩展的文本编辑器。

**用法语法**：`emacs [OPTIONS] [FILE]`

![](img/8f33496304c637dbf51ff6ddc3c7ff29_63_0.png)

`Emacs` 是至今仍在 Unix、Linux 和 BSD 系统上使用的最古老的文本编辑器之一。其可编程宏和代码语法高亮功能使其成为软件开发人员和 Web 程序员的首选。上述截图显示了 `Emacs` 编辑器的用户界面。

> **注意**：`Emacs` 是一个功能极其强大的编辑器，主要面向高级用户、软件开发人员和出版商。新用户应先专注于学习 `nano` 和 `vi` 编辑器，然后再尝试精通 `Emacs`。

常见用法示例：

- `emacs [FILE]` | 打开指定文件进行编辑。

### sed

**用途**：复杂的流编辑器。

**用法语法**：`sed [OPTIONS] [FILE]`

```bash
$ cat ShoppingList.txt
Milk
Eggs
Cheese
Tacos

$ sed s/Tacos/Nachos/ ShoppingList.txt > NewShoppingList.txt
$ cat NewShoppingList.txt
Milk
Eggs
Cheese
Nachos
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_64_0.png)

`sed` 是一个复杂的流编辑器。它使用正则表达式来修改流式传输到它的数据。正则表达式是一种模式匹配语言，在所有的 Unix、Linux 和 BSD 系统上都提供支持。

在上面的示例中，`sed` 命令读取 `ShoppingList.txt` 文件的内容，并使用正则表达式将单词 *Tacos* 的所有实例替换为 *Nachos*。结果输出到一个名为 `NewShoppingList.txt` 的新文件中。

> **注意**：正则表达式*复杂*且*无法在这本书中完全涵盖*。请访问 www.DontFearTheCommandLine.com 寻找资源以学习更多关于正则表达式语法的知识。

**常见用法示例**：

| `sed [OPTIONS] [EXPRESSION] [FILE]` | 使用 sed 编辑文件 |
|---|---|

### awk

**用途**：文本处理和模式匹配程序。

**用法语法**：`awk [EXPRESSION]`

```
$ ls -l ShoppingList.*
-rw-r--r-- 1 nick nick 24 2010-04-12 23:10 ShoppingList.old
-rw-r--r-- 1 nick nick 23 2010-04-12 19:33 ShoppingList.txt
$ ls -l ShoppingList.* | awk -F ' ' '{ print $1 " $8 }'
-rw-r--r-- ShoppingList.old
-rw-r--r-- ShoppingList.txt
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_65_0.png)

`awk` 是一个模式匹配和文本处理实用工具。它将输入的每行视为一系列字段。每行中的字段被分组到一个数组中，并根据其位置分配相关变量。在上面的示例中，`awk` 用于从 `ls` 命令的输出中提取并打印第一个和第八个字段（$1 和 $8）。

`awk` 命令也可用于执行批量处理功能，例如重命名多个文件，如下一个示例所示。

```
$ ls
File1 File3 File5 File7 File9
File2 File4 File6 File8
$ ls | awk '{print "mv "$1" "$1".txt"} ' | sh
$ ls
File1.txt File3.txt File5.txt File7.txt File9.txt
File2.txt File4.txt File6.txt File8.txt
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_65_1.png)

在这个示例中，`awk` 命令用于通过为列出的文件添加 .txt 扩展名来重命名它们。

> **注意**
>
> `awk` 是一个强大且复杂的实用工具，无法在这本书中完全涵盖。请访问 `www.DontFearTheCommandLine.com` 寻找资源以学习更多关于 `awk` 用法语法的知识。

常见用法示例：

| [INPUT] | awk [EXPRESSION] | 使用 awk 命令处理输入 |
|---|---|---|

### strings

**用途**：从二进制文件中提取可读字符。

**用法语法**：`strings [OPTIONS] [FILE]`

```
$ strings unknown.mp3
...
TAG Girl You Know It's True
Milli Vanilli
Girl You Know It's True
1989
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_66_0.png)

`strings` 命令从二进制文件中提取文本。二进制文件包含使用标准文本处理程序无法读取的数据。二进制文件的示例包括 MP3、JPEG 和 MPEG 等。

在上面的示例中，从 `unknown.mp3` 文件中提取了可读文本。这些信息可用于识别二进制文件的内容。

> **注意**
>
> *strings 命令默认显示最少 4 个字符的结果。你可以使用 `-n` 选项覆盖默认的最低字符长度。*

**常见用法示例**：

| 命令 | 描述 |
|---|---|
| `strings [FILE]` | 显示二进制文件中的可读文本字符 |
