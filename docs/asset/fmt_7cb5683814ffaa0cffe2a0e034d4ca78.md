
# vi 编辑器

## 撤销

### 表 10-8 vi 中的撤销 (UNDO)

| 命令 | 动作描述 |
| :--- | :--- |
| `u` | 撤销上一次修改。 |
| `U` | 撤销当前行的所有修改。 |
| `.`（点） | 重复上一次修改。 |
| `,`（逗号） | 反向重复上一次 `f`、`F`、`t` 或 `T` 搜索命令。 |
| `;`（分号） | 重复上一次 `f`、`F`、`t` 或 `T` 搜索命令。 |
| `"np` | 取回最后 `n` 次删除（缓冲区中删除次数有限，通常为九次）。 |
| `n` | 重复上一次 `/` 或 `?` 搜索命令。 |
| `N` | 反向重复上一次 `/` 或 `?` 搜索命令。 |

## 保存文本并退出 vi

有多种不同的方法来保存文件并退出 `vi`，其中一些总结在表 10-9 中。

### 表 10-9 保存文本并退出 vi

| 命令 | 保存和/或退出动作 |
| :--- | :--- |
| `:w` | 保存文件但不退出 `vi`。 |
| `:w file` | 保存文件中的更改但不退出 `vi`。 |
| `:wq` 或 `ZZ` 或 `:x` | 保存文件并退出 `vi`。 |
| `:q!` | 不保存文件直接退出 `vi`。 |
| `:e!` | 重新编辑文件并放弃自上次写入以来的更改。 |

## vi 中的选项

在 `vi` 中，你可以设置和取消许多选项。要设置选项，你输入 `:set option`。要取消选项，你输入 `:set nooption`。表 10-10 总结了一些最常用的选项。

### 表 10-10 vi 中的选项

| 选项 | 动作 |
| :--- | :--- |
| `:set all` | 打印所有选项。 |
| `:set nooption` | 关闭该选项。 |
| `:set nu` | 在行首显示行号。 |
| `:set showmode` | 显示当前处于插入模式还是替换模式。 |
| `:set noic` | 搜索时忽略大小写。 |
| `:set list` | 显示制表符（`^`）和行尾（`$`）。 |
| `:set ts=8` | 设置文本输入的制表符停止位。 |
| `:set window=n` | 将文本窗口中的行数设置为 `n`。 |

现在让我们在图 10-14 中为行首添加行号并显示插入或替换模式。

![](img/3ab707b472189378db808b8f9502ab8c_972_0.png)

图 10-14 vi 中的选项

除了表 10-10 中的选项外，还有许多额外的选项。

以下是在 UNIX 系统上通过执行 `:set all` 命令产生的选项列表。你应该在 `vi` 中执行此命令以查看你可使用的选项。

```
:set all
noautoindent
autoprint
noautowrite
nobeautify
directory=/var/tmp
nodoubleescape
edcompatible
noerrorbells
noexrc
flash
hardtabs=8
noignorecase
keyboardedit
nokeyboardedit!
nolisp
nolist
magic
msg
nomodelines
onumber
novovice
nooptimize
paragraphs=IPLPPPQPPLIpppippnpnp
prompt
oreadonly
redraw
remap
report=5
scroll=11
```

### 详细配置

```
sections=NHSHH UHush+c
shell=/sbin/sh
shiftwidth=8
noshowmatch
noshowmode
nloslowopen
tstop=8
taglength=0
tags=tags /usr/lib/tags
tagstack
term=hp
noterse
timeout
timeoutlen=500
ttytype=hp
warn
window=23
wrapscan
wrapmargin=0
owriteany
noshowmatch
noshowmode
```

许多选项前面都有一个 `no`，表示该选项未设置。你可能想通过 `:set all` 列出你的选项，然后对你感兴趣的选项进行实验，查看它们对你的 `vi` 会话的影响。

## vi 中的状态

你可以通过 `vi` 中的一些简单命令获取许多有用的状态信息。你可以使用表 10-1 所示的命令显示当前行号、文件行数、文件名和其他状态信息。

### 表 10-1 vi 中的状态

| 选项 | 动作 |
| :--- | :--- |
| `::` | 打印当前行。 |
| `|=` | 打印文件的行数。 |
| `^` | 显示文件名、当前行号、总行数和文件位置百分比。 |
| `:l` | 使用字母 `l` 显示特殊字符，如制表符和换行符。 |

## 定位与标记

你可以定义可以移动的文本节，也可以用字符标记文本并移动到这些标记。表 10-2 总结了 `vi` 中的定位和标记。

### 表 10-2 vi 中的定位与标记

| 选项 | 动作 |
| :--- | :--- |
| `{` | 在第一列插入以定义节。 |
| `}` | 回到节的开头。 |
| <code>&#124;</code> | 移动到下一个节的开头。 |
| `ma-z` | 用字母标记当前位置，例如使用 `mz` 标记为 `z`。 |
| `'*` | 将光标移动到指定的标记，如 `z`。 |

## 合并行

你可以使用表 10-3 所示的命令合并行。

### 表 10-3 合并行

| 命令 | 动作描述 |
| :--- | :--- |
| `J` | 将当前行合并到上一行。 |

## 光标定位与屏幕调整

你可以使用表 10-4 所示的命令将光标放置在任何位置并调整屏幕。

### 表 10-4 光标定位与屏幕调整

| 命令 | 动作描述 |
| :--- | :--- |
| `H` | 移动到行首。 |
| `L` | 移动到行尾。 |
| `M` | 移动到行中间。 |
| `G` | 移动到文件底部。 |
| `gg` | 移动到文件顶部。 |
| `n` | 移动到下一个标记。 |
| `N` | 移动到上一个标记。 |
| `%` | 跳转到匹配的括号。 |
