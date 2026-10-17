
ASP, Inc PO Box 23837 San Jose CA 95153 USA (800) 777-
UNIX * (510) 531-5615

# 第 3 章：变量与参数

```bash
$ print $ADDR
```

ASP, Inc PO Box 23837 San Jose CA 95153 USA (800) 777-
UNIX * (510) 531-5615

# Korn Shell 用户与编程手册

```bash
$ history -r -5
255 functions
254 alias
253 set
252 /etc/env
251 vi /etc/env
250 set
```

通过使用字符串代替计数参数，我们可以反向搜索特定的命令。

```bash
$ history -r set
258 fc -lr set
257 fc -ln -10
256 fc -l 250 265
255 functions
254 alias
253 set
```

参数 `set` 也可以给为 `s` 或 `se`，因为系统也会匹配部分字符串。这意味着字符串 `f` 会匹配 `functions` 和 `fc`，而 `fu` 则只会匹配 `functions`。

## 编辑命令历史文件

除了显示命令历史文件外，还可以使用具有以下格式的 `fc` 命令进行编辑：

```
fc [-e editor] [-r] [range]
或者
fc -e - [old|new] [command]
```

其中，`-e editor` 选项用于指定编辑器。如果未给出，将使用 `FCEDIT` 变量的值；如果未设置，则使用默认的 `/bin/ed`。`-r` 选项会反转命令顺序，使最新的命令首先显示。第一种格式允许你在重新执行之前编辑命令列表。要编辑的命令范围如下给出：

# 第 4 章：编辑命令

- `-n1 n2` 编辑从命令 `n1` 到命令 `n2` 的列表
- `-n` 编辑命令 `n`
- `-n` 编辑上第 `n` 个命令
- `-string` 编辑匹配该字符串的上一个命令

如果没有给出范围参数，则编辑上一个命令。列出的第二种格式允许你编辑并重新执行单条命令，其中 `old=new` 指定在重新执行之前将字符串 `old` 替换为 `new`，`command` 指定要匹配哪条命令。命令可以通过以下方式给出：

- `-n` 编辑并重新执行指定编号的命令
- `-n` 编辑并重新执行上第 `n` 个命令
- `-string` 编辑并重新执行最上一个匹配该字符串的命令

如果未给出命令参数，则编辑上一个命令。命令 `173` 可以像这样被编辑和重新执行：

```bash
$ fc -e - 173
```

另一种实现此方法是使用 `r` 命令。它与 `fc -e-` 命令相同。使用 `r` 也可以给出上一个命令：

```bash
$ r 173
```

如你所见，`r` 命令比 `fc -e-` 命令更易用。替换功能被用于对上一个命令进行微调。让我们从打印 Hello 开始：

```bash
$ print Hello
Hello
```

我们可以像这样将 Hello 改为其他内容：

```bash
$ r Hello=Goodbye print
print Goodbye
Goodbye
```

下一节将介绍如何使用内联编辑器编辑和重新执行命令的更简单的方法。

## 内联编辑器

内联编辑提供了在执行前编辑当前或上一个命令的能力。共有三种内联编辑模式：`emacs`、`gmacs` 和 `vi`。内联编辑模式通过设置 `EDITOR` 或 `VISUAL` 变量来指定，如果这两个变量都没有设置，默认值为 `/bin/ed`。也可以通过 `set -o` 命令指定内联编辑模式，如下所示：

```bash
$ set -o option
```
