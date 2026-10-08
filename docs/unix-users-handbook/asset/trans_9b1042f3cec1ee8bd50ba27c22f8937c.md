

![](img/75f39fc91296b889c0653851accdfd46_458_0.png)

图 8-8 vi 中删除文本的示例 (x, X, dw, 和 dG)

![](img/75f39fc91296b889c0653851accdfd46_459_0.png)

图 8-9 vi 中删除文本的示例 (dd 和 db)

## 在 vi 中修改文本

好吧，你已经添加了文本并删除了文本，现在你想要修改文本。到目前为止，vi 还没那么糟糕，对吧？表 8-5 汇总了一些用于修改文本的命令。

### 表 8-5 在 vi 中修改文本

| 命令 | 替换操作 |
| :--- | :--- |
| (在这些命令前加上数字可以重复执行该命令任意次。) | |
| `r`char | 用 char 替换当前字符。 |
| Rtext `escape` | 替换当前字符为 text，直到输入 `escape` 为止。 |
| stext `escape` | 用 text 替换当前字符。 |
| S 或 ctext `escape` | 用 text 替换整行。 |
| cw text `escape` | 将当前单词更改为 text。 |
| Ctext `escape` | 将当前行剩余部分更改为 text。 |
| cG `escape` | 更改到文件末尾。 |
| ccursor_cmd text `escape` | 将当前位置到 cursor_cmd 之间的内容更改为 text。 |

现在让我们看看图 8-10 和 8-11 中在 wisdom 文件中替换文本的一些示例。

![](img/75f39fc91296b889c0653851accdfd46_461_0.png)

图 8-10 vi 中修改文本的示例 (r, R, cw, 和 cG)

![](img/75f39fc91296b889c0653851accdfd46_462_0.png)

图 8-11 vi 中使用 cc 修改文本的示例

## vi 中的查找和替换

vi 中有许多查找和替换功能。表 8-6 汇总了 vi 中一些更常见的查找和替换功能。

![](img/75f39fc91296b889c0653851accdfd46_462_1.png)

### 表 8-6 vi 中的查找和替换

| 命令 | 查找和替换操作 |
| :--- | :--- |
| `/`text | 在文件中向前查找 text。 |
| `?`text | 在文件中向后查找 text。 |
| n | 沿与原查找相同的方向重复查找。 |
| N | 沿与原查找相反的方向重复查找。 |
| ftext | 在当前行中向前查找 text。 |
| Ftext | 在当前行中向后查找 text。 |
| ttext | 在当前行中向前查找 text，并停在 text 之前的字符处。 |
| Ttext | 在当前行中向后查找 text，并停在 text 之后的字符处。 |
| `:set ic` | 查找时忽略大小写。 |
| `:set noic` | 使查找区分大小写。 |
| `:s/oldtext/newtext/` | 用 newtext 替换 oldtext。 |
| `:m,n s/oldtext/newtext/` | 在第 m 行到第 n 行之间用 newtext 替换 oldtext。 |
| `&` | 重复上一个 `:s` 命令。 |
| `:g/text1/s/text2/text3` | 查找包含 text1 的行，用 text3 替换 text2。 |
| `:g/text/command` | 对所有包含 text 的行执行 command。 |
| `:v/text/command` | 对所有不包含 text 的行执行 command。 |

现在让我们看看图 8-12 中在 wisdom 文件中搜索和替换文本的一些示例。

![](img/75f39fc91296b889c0653851accdfd46_464_0.png)

你可以使用 `:g` 和 `:v` 执行高级搜索。你可以使用以下命令查找并显示文件中所有包含 `while` 的行：

```
:g/while/p
```

此命令行中的 `/p` 是用于 ex 编辑器的打印命令。你可以使用以下命令查找文件中所有包含 `while` 的行并删除这些行：

```
:g/while/d
```

你还可以指定希望进行搜索的特定行号。以下命令查找第 10 行到第 20 行之间包含 `while` 的所有行，并显示其出现的行号：

```
:10,20g/while/nu
```

`:g` 对包含我们要查找的文本的行执行命令，而 `:v` 对不包含指定文本的行执行命令。以下三个命令以与前三个命令作用于包含 `while` 的行相同的方式，作用于不包含 `while` 的行：

```
:v/while/p
```

```
:v/while/d
```

```
:10,20v/while/nu
```

第一个命令打印不包含 `while` 的行。第二个命令删除未出现 `while` 的行。第三个命令打印第 10 行到第 20 行之间未出现 `while` 的行号。

## 在 vi 中复制文本

你可以在 vi 中复制文本。一些用于复制的命令显示在表 8-7 中。

### 表 8-7 vi 中的复制

| 命令 | 复制操作 |
| :--- | :--- |
| yy | 提取（Yank）当前行。 |
| nyy | 提取 n 行。 |
| p (小写) | 将提取的文本放在光标之后。 |
| P (大写) | 将提取的文本放在光标之前。 |
| "(a-z)nyy | 将 n 行复制到括号中命名的缓冲区。省略 n 则针对当前行。 |
| "(a-z)ndd | 将 n 行删除到括号中命名的缓冲区。省略 n 则针对当前行。 |
| "(a-z)p | 将括号中缓冲区命名的行放在当前行之后。 |
| "(a-z)P | 将括号中缓冲区命名的行放在当前行之前。 |

现在让我们看看图 8-13 中在 wisdom 文件中复制文本的一些示例。

![](img/75f39fc91296b889c0653851accdfd46_467_0.png)

## vi 中的撤销和重复

![](img/75f39fc91296b889c0653851accdfd46_467_1.png)

你可以轻松使用表 8-8 中显示的命令在 vi 中撤销更改。

### 表 8-8 vi 中的撤销和重复

| 命令 | 撤销操作 |
| :--- | :--- |
| u | 撤销最后一次更改。 |
| U | 撤销对当前行的所有更改。 |
| . (句点) | 重复最后一次更改。 |
| , (逗号) | 沿相反方向重复最后一个 f, F, t, 或 T 查找命令。 |
| ; (分号) | 重复最后一个 f, F, t, 或 T 查找命令。 |
| "np | 检索第 n 次删除（缓冲区中保存有限数量的删除记录，通常是九个）。 |
| n | 重复最后一个 / 或 ? 查找命令。 |
| N | 沿相反方向重复最后一个 / 或 ? 查找命令。 |

## 保存文本并退出 vi

你有多种方式保存文件并退出 vi，其中一些汇总在表 8-9 中。

![](img/75f39fc91296b889c0653851accdfd46_468_0.png)

### 表 8-9 保存文本并退出 vi

| 命令 | 保存和/或退出操作 |
| :--- | :--- |
| `:w` | 保存文件但不退出 vi。 |
| `:w file` | 保存文件更改但不退出 vi。 |
| `:wq` 或 ZZ 或 `:x` | 保存文件并退出 vi。 |
| `:q!` | 不保存文件而退出 vi。 |
| `:e!` | 重新编辑文件，丢弃自上次写入以来的更改。 |

## vi 中的选项

![](img/75f39fc91296b889c0653851accdfd46_469_0.png)

在 vi 中，你可以设置和取消许多选项。要设置一个选项，你输入 `:set option`。要取消一个选项，你输入 `:set nooption`。表 8-10 汇总了一些更常用的选项。

### 表 8-10 vi 中的选项

| 选项 | 操作 |
| :--- | :--- |
| `:set all` | 打印所有选项。 |
| `:set nooption` | 关闭选项。 |
| `:set nu` | 在行前加上行号。 |
| `:set showmode` | 显示是输入模式还是替换模式。 |
| `:set noic` | 查找时忽略大小写。 |
| `:set list` | 显示制表符 (^I) 和行尾 ($)。 |
| `:set ts=8` | 设置文本输入的制表位。 |
| `:set window=n` | 将文本窗口的行数设置为 n。 |

让我们在图 8-14 中为行加上行号并显示输入或替换模式。

![](img/75f39fc91296b889c0653851accdfd46_470_0.png)

除了表 8-10 中的选项外，还有许多其他可用的选项。以下是一个在 UNIX 系统上通过 `:set all` 命令生成的选项列表。你应该在 `vi` 中执行此命令以查看可用的选项：

```
:set all
noautoindent
autoprint
noautowrite
nobeautify
directory=/var/tmp
nodoubleescape
noedcompatible
noerrorbells
noexrc
flash
hardtabs=8
noignorecase
keybaordedit
nokeybaordedit!
nolisp
nolist
magic
mesg
nomodelines
nonumber
nonovice
noopimize
paragraphs=IPLPPQPP LIpplpipnpbp
prompt
noreadonly
redraw
remap
report=5
scroll=11
sections=NHSHH HUuhsh+c
shell=/sbin/sh
shiftwidth=8
noshowmatch
noshowmode
noslowopen
```

