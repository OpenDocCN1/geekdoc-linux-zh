
在此示例中，`number` 是打印任务号。你可以通过输入 `rm` 后跟任务号来取消队列中的任务。要打印 `foo.txt`，例如，使用 `rm`。

# 清除和重置终端

在执行 `ls` 命令后，正在工作的终端窗口可能会变得拥挤。你可以随时退出终端窗口并打开一个新的，但有一个更快更简单的方法来清除终端中显示的内容：在 shell 提示符下输入 `clear` 命令。该命令会清除终端窗口。

有时，你可能会意外打开一个程序或其他文本文件。关闭文件后，你可能会发现输入的文本与显示的内容不匹配。在这种情况下，输入 `reset` 将终端窗口恢复到默认值。

# 使用 cat 操作文件

该实用工具名为 `cat`（`concatenate` 的缩写），意为合并文件。`cat` 命令会在屏幕上显示整个文件的内容（例如，输入 `cat filename.txt`）。如果文件很长，它会快速滚动屏幕。为了防止这种情况，使用 `cat filename.txt | less` 命令。

使用管道（`|`）和 `less` 命令可以一次显示页文件。你可以使用上下箭头向前翻页。关于使用管道合并两个独立函数的更多信息，请参见本章后面的“管道与分页器”章节。

# 使用重定向

重定向意味着让 shell 改变标准输出的去向。

## 152 第二部分：基础

重定向标准输出，使用 `>` 符号。在 `cat` 命令（或任何向标准输出内容的实用工具或应用程序）之后放置 `>` 将将其输出重定向到文件名。

例如，单独使用 `cat` 将你输入的内容输出到屏幕，就像你刚刚输入的那行一样。以下示例显示 `cat` 重复输入的每一行：

```
sam@halloween sam$cat

buy some sneakers

buy some sneakers

then go to coffee shop

then go to the coffee shop

then buy some coffee

then buy some coffee
```

将 `cat` 输出重定向到文件，在 shell 提示符下输入以下（按回车键将进入下一个空行）：

```
sam@halloween$cat > sneakers.txt

buy some sneakers

then go to the coffee shop

then buy some coffee
```

按回车进入空行，并使用 `Ctrl-D` 键退出 `cat`。

注意图 8-5 中没有重复的条目。这是因为标准输出 `cat` 被重定向了。重定向你创建的名为 `sneakers.txt` 的新文件。你可以在启动 `cat` 时所在的目录找到它（如果想查看列表，输入 `ls`）。

正如你之前学的，可以使用 `cat` 读取文件。在提示符处输入：

```
cat sneakers.txt
```

为另一个文件使用重定向并命名为 `home.txt`。在此示例中，输入以下内容：

```
sam@halloween sam$cat > home.txt

bring the coffee home

take off shoes

put on sneakers

make some coffee

relax!
```

现在，在空行再次使用 `Ctrl-D` 键退出 `cat`。接下来，使用 `cat` 将 `home.txt` 与 `sneakers.txt` 合并，并将两个文件的输出重定向到一个新文件 `saturday.txt`（在图 8-5 中找到示例）。输入以下内容：

```
sam@halloween sam]$cat sneakers.txt home.txt > saturday.txt
```

```
File Edit Terminal Go Help

[sam@Halloween sam]$ cat sneakers.txt home.txt > saturday.txt

[sam@Halloween sam]$ cat sneakers.txt

buy some sneakers

then go to the coffee shop

then buy some coffee

bring the coffee home

take off shoes

put on sneakers

make some coffee

relax!

[sam@Halloween sam]$ |
```

图 8-5. 合并文件和重定向输出

你可以看到 `cat` 已在 `sneakers.txt` 结束后添加了 `home.txt`。

## 第8章：Shell 命令行基础 153

### 追加标准输出

你可以使用输出重定向将新信息添加到现有文件的末尾。这与你使用 `>` 符号类似，你是在告诉你的 shell 将信息发送到标准输出以外的地方。

然而，当你使用 `>>` 时，你是在向文件中添加信息，而不是完全替换文件的内容。

最好的解释就是演示。取两个在之前的示例中已经创建的文件（`sneakers.txt` 和 `home.txt`），并使用追加符号（`>>`）将它们合并。你想将 `home.txt` 中的信息添加到 `sneakers.txt` 已有的信息中，因此输入以下：

```
cat home.txt >> sneakers.txt
```

现在使用命令 `cat sneakers.txt` 检查文件。最终输出显示文件末尾有 `home.txt` 的内容。

```
[sam@halloween sam]$cat sneakers.txt

buy some sneakers

then go to the coffee shop
then buy some coffee
bring the coffee home
take off shoes
put on sneakers
make some coffee
relax!
[sam@Halloween sam]$
```

你输入的命令是将 `home.txt` 文件的输出追加到 `sneakers.txt` 中。

通过追加输出，你通过使用现有文件而不是创建新文件来节省了时间（并减少了磁盘碎片）。

现在比较 `sneakers.txt` 和 `saturday.txt` 文件的结果，你会发现它们是完全相同的。要进行比较，请输入以下：

```
cat sneakers.txt; cat saturday.txt
```

两个文件的内容都将被显示——首先是 `sneakers.txt`，然后是 `saturday.txt`。

```
File Edit View Terminal Go Help
[sam@Halloween sam]$ cat sneakers.txt; cat saturday.txt
buy some sneakers
then go to the coffee shop
buy buy some coffee
bring the coffee home
take off shoes
put on sneakers
make some coffee
relax!
buy some sneakers
then go to the coffee shop
buy buy some coffee
bring the coffee home
take off shoes
put on sneakers
make some coffee
relax!
[sam@Halloween sam]$
```

图 8-6. 命令链接与文件比较

### 重定向标准输入

你不仅可以重定向标准输出，还可以对标准输入执行相同类型的重定向。

当你使用标准输入符号 `<` 时，你是在告诉 shell 你想将一个文件作为命令的输入读取。

使用你已经创建的文件来演示这个概念。只需输入：

```
cat < sneakers.txt
```

由于你使用了小于号（`<`）来将 `cat` 命令与文件分开，`sneakers.txt` 的输出被 `cat` 读取了。

### 管道与分页器

管道（pipe）是键盘上与反斜杠位于同一键上的符号。在 Linux 中，管道将一个命令的标准输出连接到另一个命令的输入。考虑本章早些时候讨论过的 `ls` 命令。`ls` 有许多可用选项，但如果目录的内容滚动太快而无法查看怎么办？

例如，查看 `/etc` 目录的内容。

```
ls -al /etc
```

在输出离开屏幕之前，如何更仔细地查看输出呢？

一种方法是将输出管道到一个名为 `less` 的工具。`less` 是一个分页器工具，允许你每次一页（或一屏）查看信息。

```
ls -al /etc | less
```

现在你可以每次查看一页 `/etc` 的内容。要移动屏幕，可以按 `b` 键向上移动，按 `q` 键退出。或者，你可以使用方向键进行翻页。为了向下移动屏幕，可以按 `d` 键。管道也可以用于打印特定的行。输入以下将打印 `sneakers.txt` 中包含 "coffee" 的行：

```
cat sneakers.txt | more
```

`more` 命令
