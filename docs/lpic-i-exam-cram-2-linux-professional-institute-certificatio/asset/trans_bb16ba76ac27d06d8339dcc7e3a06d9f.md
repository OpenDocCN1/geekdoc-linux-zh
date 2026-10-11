
## 当 Cat 逆向运行时

# 值可以是 b（即 512 字节）、k（即 1024 字节）或 m（即 1024 千字节）。例如，如果你需要将一个 8.8MB 的文本文件分割成 1.44MB 的块，可以使用以下命令：

```
split -b1440000 bigtextfile.txt
ls -l x77
-rw-r--r-- 1 root root 1440000 Feb 23 09:25 xaa
-rw-f--r-- 1 root root 1440000 Feb 23 09:25 xab
-rw-f--r-- 1 root root 1440000 Feb 23 09:25 xac
-rw-f--r-- 1 root root 1440000 Feb 23 09:25 xad
-rw-f--r-- 1 root root 1440000 Feb 23 09:25 xae
-rw-f--r-- 1 root root 249587 Feb 23 09:25 xag
```

在某些情况下，你希望以逆向或倒序显示文件，这正是 `tac` 命令的用武之地。你可以这样使用它：

```
cat file |
```

这将产生类似于以下内容的输出：

```
1 Watchdog Timer Interfaces For The Linux Operating
2
3 Alan Cox <alan@lxorguk.ukuu.org.uk>
4
5 Custom Linux Driver And Program Development
```

对该文件使用 `tac` 会产生以下输出：

```
tac file |
```

这将产生类似于以下内容的输出：

```
5 Custom Linux Driver And Program Development
4
3 Alan Cox <alan@lxorguk.ukuu.org.uk>
2
1 Watchdog Timer Interfaces For The Linux Operating
```

## 安全查看二进制文件

`od` 命令用于安全地查看二进制文件或非 ASCII 文件；否则，显示内容很可能会变得乱码，并且系统会发出悲鸣的蜂鸣声。

`od` 能够以不同的方式显示文件，包括：
- `-a` 命名
- `-o` 八进制
- `-d` 十进制
- `-x` 十六进制
- `-t` 浮点数

这些格式中大多数并不常用于日常使用，只有十六进制和八进制格式显示的输出比较有趣。

> 注意关于如何查看二进制文件的问题。`od` 命令几乎是唯一可能的查看方式。

如果你在意外查看二进制文件后遇到控制台乱码问题，请使用 `reset` 命令。它会重新初始化终端，使其再次可读。

## 格式化命令

`pr` 和 `fmt` 命令用于对文本流或文件进行换行和格式化，以便打印。

`pr` 命令适用于格式化源代码和其他文本文件以便打印。它会在每个格式化的 66 行页面的顶部添加日期和时间块、文件名（如果存在）以及页码，如下所示：

```
pr 501inefile
```

这将产生类似于此处所示的输出：

```
2004-02-23 21:19        501inefile                 Page 1

1       Watchdog Timer Interfaces For The Linux Operating System
2
3           Alan Cox <alan@lxorguk.ukuu.org.uk>
4
5           Custom Linux Driver And Program Development
```

`pr` 命令可以显示数据列，将列裁剪以适应每页的数量，如下所示：

```
pr --columns=2 501inefile
2004-02-23 21:02        501inefile                 Page 1

1       Watchdog Timer Inte           26     and some Berkshire cards. T
2                                   27     internal temperature in deg
3       Alan Cox <a                  28     giving the temperature.
4                                   29
5       Custom Linux D               30     The third interface logs ke
```

`fmt` 命令也适用于格式化文本文件，但它仅限于将长行换行以适应较小的页面或 `pr` 设置的列宽。

前面 `pr` 列的示例会在列处截断数据，导致页面上的数据丢失。这可以通过混合命令来解决，如下所示：

```
[root@localhost root]# fmt -35 501nefile | pr -column=2
2004-02-23 21:49                              501nefile
                                              Page 1

1     Watchdog                    temperature. 29 30  The third
    Timer Interfaces For The     interface logs kernel messages
    Linux Operating System 2     on additional alert events.
3     Alan Cox                   31 32  Both software and
```

## 翻译文件

`tr` 命令用于更改文件或流中的字符，但不能更改整个单词或短语——那是 `sed` 的工作。

例如，如果你有一个包含书中示例中许多命令的文件，但其中一些命令因为编辑器将每行首字符大写而失效，你可以使用以下命令将文件中的大写字母转换为小写字母：

```
tr A-Z a-z < commands.txt
```

`tr` 命令无法自我提供输入。因此，`<` 操作符是必须的；否则，命令将无法工作。以下命令可以实现相同的结果：

```
tr [:upper:] [:lower:] < commands.txt
```

![](img/49f4f38f3aec011238fa50f89e643db3_254_0.png)

> 请记住，`tr` 无法自我提供输入，因此需要 `<` 重定向符号将输入文件发送给命令。其他任何输入都是损坏的命令，并会导致语法错误。

## 他 sed，她 sed

`sed`，即流编辑器命令，用于处理文本流并执行操作，例如文本文件中的行。`sed` 功能强大得惊人，这意味着它可能相当难以使用。

![](img/49f4f38f3aec011238fa50f89e643db3_255_0.png)

> **sed** 最常用的操作之一是搜索和替换文本，包括单词和完整短语。虽然 **tr** 仅单独处理字符和数字，但 **sed** 能够执行非常复杂的功能，包括每行多个操作。

`sed` 使用以下命令语法：

```
sed -option action/regexp/replacement/flags filename
```

而不是费力解释输入某些选项时会发生什么，让我们看看使用这些选项时 `sed` 做了什么。正确使用 `sed` 包括能够，咳咳，“复用”其他系统管理员的 `sed` 命令。

要在给定文件的每一行中替换第一个 `bob` 实例为 `BOB`，你可以使用这个命令：

```
sed s/bob/BOB/ file1
```

要在给定文件的每一行中替换所有 `bob` 实例为 `BOB`，你可以使用这个命令：

```
sed s/bob/BOB/g file1
```

`sed` 允许对给定流的行进行多个操作，所有这些操作都在进入下一行之前完成。

要在给定文件中搜索并替换 `bob` 为 `BOB`，然后搜索 `B0B` 并将其替换为 `snuffy`，对每一行和每个实例，你可以使用这个：

```
sed 's/bob/BOB/g ; s/BOB/snuffy/g' file1
```

分号字符的使用类似于 bash 独立运行多个命令的能力。然而，这个整体操作，从第一个单引号 (') 到最后一个单引号，全都是在 `sed` 内部执行的，而不是作为 bash 的一部分。

当 `sed` 用于多个命令时，你可以使用分号分隔命令，或使用多个 `-e` 实例来显示多个命令：

```
sed -e s/bob/BOB/g -e s/BOB/snuffy/g file1
```

![](img/49f4f38f3aec011238fa50f89e643db3_255_1.png)

> 在考试中，以及任何你可能使用带有空格模式的 **sed** 的地方，请用单引号括住整个模式/程序，例如
> 
> `sed 's/is not/is too/g' file1`
> 
> 这可以防止你因字符串中的空格而遇到语法错误。

迟早，你会厌倦为 `sed` 输入相同的操作，并希望使用脚本或某种方法来自动化重复任务。`sed` 具有使用包含一组程序的简单脚本文件的能力。前面一组程序的 `sed` 脚本文件示例如下：

```
s/bob/BOB/g
s/BOB/Snuffy/g
```

此脚本文件按以下方式使用：

```
sed -f scriptfile targetfile
```

许多多个程序可以在单个流上执行，整个程序集在每个后续行上执行。

显然，在给定文本流上执行大量程序可能需要时间，但通常这是值得的，因为你只需要验证它在完成后是否正常工作。这肯定比在 vi 中手动完成一切都好！

`sed` 的另一个实用功能是其抑制或没有显示未进行更改的任何行的能力。

例如，如果你想在给定文件的所有行中将 `machine` 替换为 `MACHINE`，但只显示更改后的行，你可以使用带有 `-n` 选项的以下命令，使命令抑制正常输出：

```
sed -n 's/machine/MACHINE/pg' watchdog.txt
```

末尾的 `pg` 字符串打印匹配或更改的行，并对每行所有实例进行全局替换，而不仅仅是每行的第一个实例。

要对行范围进行搜索和替换，在 `s/` 字符串前添加行号或由逗号分隔的范围，例如：

```
sed -n '1,5s/server/SERVER/pg' sedfile
```

The X SERVER uses this directory to store the compiled version of the current keymap and/or any scratch keymaps used by clients. The X SERVER time. The default keymap for any SERVER is usually stored in:

![](img/49f4f38f3aec011238fa50f89e643db3_256_0.png)

> 在考试中，sed 问题都是关于什么能查找并替换字符串，特别关注全局替换与单次替换。

## 获取 grep

更有趣的文本处理命令之一是 `grep`。正确使用，它可以在单个文件、通过 stdin 的文本流或整个文件目录（例如内核源层次结构）中查找几乎任何字符串或短语。

