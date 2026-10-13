
| `C-x3` | 水平分割当前编辑窗。 |

| `C-x1` | 使当前编辑窗填充整个屏幕（隐藏/移除其他窗格）。 |

| `C-xo` | 选择下一个编辑窗。 |

| `C-xk` | 关闭（不保存）你正在工作的文件或缓冲区。例如，在打开 emacs 教程后使用此快捷键再次退出。 |

![](img/92a94ba94656919835b7a50a27c9d9ba_135_0.png)

### 表 5.2 续

| 快捷键 | 解释 |

| --- | --- |

| `C-xb` | 切换到另一个缓冲区——迷你缓冲区会提示你缓冲区名称；如果你不确定打开的缓冲区名称，按 `Tab` 键查看完整列表。 |

| `C-xi file` | 在光标位置插入文件。迷你缓冲区会提示你文件名。 |

| `C-x C-c` | 完全退出 emacs。 |

| `C-g` | 取消 emacs 进程。 |

在我们结束对 emacs 的讨论之前，最后一个快捷键将带你走向通往成为 emacs 专家的道路。要查看 emacs 中可用命令的列表，按 `M-x` 然后按 `Tab` 键。会出现一个包含 emacs 命令列表的缓冲区。反复按 `C-xo` 直到光标出现在该窗格中；你可以使用 `Page Up` 和 `Page Down` 浏览可用命令。如果你看到一个想尝试的命令，将其输入迷你缓冲区并按回车。

各种 emacs 命令包括以下：

- `M-x dunnet` 启动一个基于文本的冒险游戏。
- `M-x auto-fill` 开启自动换行。
- `M-x calendar` 打开一个包含三个月日历的新窗格。
- `M-x ansi-term` 在当前窗格中打开一个 shell。在运行此命令之前，务必使用 `C-x2` 或 `C-x3`，以便你可以在不同窗格之间通过 `C-xo` 同时编辑文件和工作，如图 5.5 所示。

![](img/92a94ba94656919835b7a50a27c9d9ba_136_0.png)

![](img/92a94ba94656919835b7a50a27c9d9ba_137_0.png)

# 让控制台为你工作服务

如果你成为一名 emacs 用户，你很快会发现，不时，你的工作目录下会出现一些名称与你正在处理的文件相似的文件，但有细小的添加。例如，如果你正在处理一个文件 `myfile.txt`，你可能在同一个目录下还会发现 `#myfile.txt` 或 `myfile.txt-`。

这些是 emacs 为了保护你的数据而创建的“安全”文件。

当你在不保存文件的情况下退出时，emacs 会将文件保存，使用相同名称，并在前后加上 hash 标记（`#`），以防你以后想恢复所做的更改。

当你对现有文件进行更改并保存时，emacs 会保留原始（未修改的）文件。

## 为了高效管理对文件分组

如果你成为一名 emacs 用户，你很快会发现，不时，你的工作目录下会出现一些名称与你正在处理的文件相似的文件，但有细小的添加。例如，如果你正在处理一个文件 `myfile.txt`，你可能在同一个目录下还会发现 `#myfile.txt` 或 `myfile.txt-`。

这些是 emacs 为了保护你的数据而创建的“安全”文件。

当你在不保存文件的情况下退出时，emacs 会将文件保存，使用相同名称，并在前后加上 hash 标记（`#`），以防你以后想恢复所做的更改。

当你对现有文件进行更改并保存时，emacs 会保留原始（未修改的）文件。

## 在命令行上对文件分组

为了说明，考虑以下问题。假设你想将 `myfile.txt`、`newfile.txt` 和 `emacsfile.txt` 存在名为 `firstfiles` 的目录中。使用你在第 4 章“操作文件和目录”中学到的技能，你首先创建目录，然后使用 `mv` 移动它们：

```
u@workstation20]$ mkdir firstfiles
u@workstation20]$ mv myfile.txt newfile.txt emacsfile.txt firstfiles
```

但是移动三个文件需要输入很多字。似乎有更简单的方法——确实有。在 shell 中使用时，星号（`*`）是用于文件名扩展的特殊字符之一。文件名扩展使用特定的匹配工具来收集文件并将组传递给 shell。听起来很复杂，但实际上很简单。这里有一个使用文件名扩展执行该任务的示例：

```
u@workstation20]$ mv *.txt firstfiles
```

让我们确保命令达到了预期效果：

```
u@workstation20]$ ls
firstfiles
u@workstation20]$ ls firstfiles
emacsfile.txt newfile.txt myfile.txt
```

显然，新的简化命令产生了预期结果。`*.txt` 分组了所有以 `.txt` 四字符结尾的文件。

我们将介绍其他示例；但在之前，请看表 5.3，它列出了常用的文件名扩展模式。

### 表 5.3 常用模式匹配字符及其影响

| 模式 | 匹配效果 |

|---|--- |

| `*` | 匹配任意数量的字符，包括零字符 |

| `?` | 匹配单个字符 |

| `[a-b]` (范围) | 匹配 a 到 b 范围内的单个字符；例如，`[A-Z]` 会匹配字母 x 或 P，但不会匹配数字 9 或字母 a |

| `[AaBbCc]` (列表) | 匹配提供列表中的单个字符 |

通过几个示例可以帮你更好地理解这些模式的含义，以及它们如何帮助在 Red Hat Linux 中处理文件组。让我们创建一个示例表。假设你要删除家目录中的一组文件，你正在

# 让命令行为你为你工作

表 5.4 显示了一些示例通配符参数和文件，以及它们分别匹配（或不匹配）的内容。

### 表 5.4 使用展开的示例命令及其影响

| 命令 | 效果 |

| --- | --- |

| `rm *.txt` | 会删除任何以 `.txt` 结尾的文件——例如，`a.txt`、`b.txt`、`hello.txt` 或 `everybody_cool.txt`，但不会删除 `bicycle`、`car_bills.xls` 或 `myoldtext` |

| `rm *.jpg` | 会删除任何以字母 a 开头并以字母 jpg 结尾的文件——例如，`a.jpg`、`aswermachine.jpg` 和 `anastasia.jpg`，但不会删除 `boat.jpg`、`file.txt`、`monkeys.jpg` 或 `macaroni_list` |

| `rm *.tif` | 会删除 `kitchen.gif`、`kluckchicken.tif`、`monkeys.tif` 和 `work.kday.tif`，但不会删除 `casino.gif` 或 `fountain.tif` |

| `rm [1-9]*` | 会删除 `leg.gif`、`log.txt`、`lug.jpg`、`log.my_hours.please log.goog.go`、`log.this`，但不会删除 `log glover.txt` 或 `log` |

| `rm [a-f]*` | 会删除 `every.txt`、`bacon.jpg`、`cradle.dog`、`walking.schedule`、`everybody.mp3` 和 `fanatics_favorites`，但不会删除 `goose.txt`、`xylophone.jpg` 或 `Barbie.gif` |

| `rm *` | 会删除当前工作目录下的所有文件。添加 `-rf` 选项将删除当前目录下的所有文件和目录。（还记得第 4 小时的 `-r` 和 `-f` 选项吗？） |

![](img/92a94ba94656919835b7a50a27c9d9ba_139_0.png)

在使用文件名扩展名分组文件时要小心；粗率地构建模式可能会导致意想不到的后果。例如，在使用表 5.4 所示的方法删除文件时，Linux 在删除所有匹配你提供的模式的文件之前不会向你发出警告，也不会询问你是否确定。

文件名展开可以在大多数情况下使用，通过减少管理大量文件时需要阅读和输入的字量，让你的命令行操作变得更轻松。作为最后一个示例，将你用 vi 创建的文件移回主目录，同时将你用 emacs 创建的文件留在 `firstfiles` 目录中：

```
[@workstation20 you]$ mv firstfiles/*vi* 
[@workstation20 you]$ ls
firstfiles mynewfile.txt myfile.txt
[@workstation20 you]$ ls firstfiles
emyacsfile.txt
[@workstation20 you]$ **
```

## 防止文件名展开

有时，你并不希望 shell 执行文件名展开——例如，当你想在文件名中使用星号或问号等特殊匹配字符，或者将它们作为命令的参数时。

假设，例如，你想在主目录下创建一个名为 `*new*` 的目录，用来存放你正在处理的一些新改进文件。在 Linux 中，在文件名或目录名中使用星号并不是非法的。然而，当你尝试创建一个目录时，它并没有生效：

```
@workstation20 you$ mkdir *new*
mkdir: 'myfile.txt' exists but is not a directory
@workstation20 you$
```
