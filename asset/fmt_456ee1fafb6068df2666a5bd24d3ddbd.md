
```bash
echo "press interrupt (CTRL-C) to interrupt ..."
while [ -f /tmp/my_tmp_file_$$ ]; do
    echo File exists
    sleep 1
done
echo The file no longer exists

trap INT
echo creating /tmp/my_tmp_file_$
date > /tmp/my_tmp_file_$

echo "press interrupt (control-C) to interrupt ..."
while [ -f /tmp/my_tmp_file_$$ ]; do
    echo File exists
    sleep 1
done

echo we never get here
exit 0
```

如果运行运行这个脚本，并在每个循环中按下 `Ctrl+C`（或你的任何中断键），我们将得到以下输出：

```text
creating file /tmp/my_tmp_file_141
press interrupt (CTRL-C) to interrupt ...
File exists
File exists
File exists
File exists
The file no longer exists
creating /tmp/my_tmp_file_141
press interrupt (control-C) to interrupt ...
File exists
File exists
File exists
File exists
```

## 工作原理

此脚本使用 `trap` 命令来安排在发生 `INT`（中断）信号时执行命令 `rm -f /tmp/my_tmp_file_$$`。脚本随后进入 `while` 循环，只要文件存在就会继续。当用户按下 `Ctrl+C` 时，`rm -f /tmp/my_tmp_file_$$` 语句被执行，然后运行 `while` 循环。由于文件已被删除，第一个 `while` 循环正常终止。

脚本接着再次使用 `trap` 命令，这次指定在发生 `INT` 信号发生时不执行任何命令。它重新创建文件并在第二个 `while` 语句内部进行循环。当用户这次按下 `Ctrl+C` 时，没有配置任何要执行的语句，因此会发生默认行为，即立即终止脚本。由于脚本立即终止，最后的 `echo` 和 `exit` 语句永远不会执行。

# 第 2 章

## unset

`unset` 命令从环境中移除变量或函数。它不能删除由 shell 自身定义的只读变量，例如 `IFS`。它并不经常使用。

以下脚本会写入一次 `Hello World`，第二次写入一个换行符：

```bash
#!/bin/sh

foo="Hello World"
echo $foo
\unset foo
echo $foo
```

> `foo=` 的效果与上述程序中的 `unset` 非常相似，但并不完全相同。写入 `foo=` 的效果是将 `foo` 设置为空值，但 `foo` 仍然存在。使用 `unset foo` 的效果是从环境中移除变量 `foo`。

## 另外两个实用的命令和正则表达式

在看到如何利用这些新的 shell 编程知识之前，让我们来看几个非常实用的命令，尽管它们不是 shell 的一部分，但在编写 shell 脚本时通常很有用。在此过程中，我们还将查看正则表达式，这是一种 `Linux` 及其相关程序中到处出现的模式匹配功能。

## find 命令

我们查看的第一个命令是 `find`。我们使用它来搜索文件，它非常有用，但 `Linux` 新手觉得它用起来有点复杂，尤其是因为它接受选项（`options`）、测试（`tests`）和动作类型参数参数，而且一个参数的结果会影响后续参数的处理。

在深入研究选项、测试和参数之前，让我们来看本地机器上文件的一个非常简单的例子。我们以 `root` 身份执行此操作，以确保我们有权限搜索整个机器。

```bash
## find -name wish -print
/usr/bin/wish
#
```

正如你可能猜到的那样，这表示“从 `/` 开始搜索一个名为 `wish` 的文件，然后打印出文件的名称”。

然而，它运行了很长时间，`Windows` 机器上的磁盘咯吱作响。`Linux` 机器（使用 `SAMBA`）挂载了 `Windows` 机器文件系统的一部分。似乎那部分也被搜索了，尽管我们知道要找的文件会在 `Linux` 机器上。

## Shell 编程

这就是第一个选项用用场。如果我们指定 `-mount`，我们可以告诉 `find` 不要搜索挂载的目录：

```bash
## find /-mount -name wish -print
usr/bin/wish
#
```

我们仍然找到了文件，但没有搜索其他挂载的文件系统。

`find` 命令的完整语法为：

```text
find [path] [options] [tests] [actions]
```

路径部分非常简单：我们既可以使用绝对路径（如 `/bin`），也可以使用相对路径（如 `..`）。如果需要，还可以指定多个路径，例如 `find /var/home`。

有几个选项，主要的如下：

| 选项 | 含义 |
| :--- | :--- |
| `-depth` | 在查看目录本身之前搜索目录的内容。 |
| `-follow` | 跟踪符号链接。 |
| `-maxdepth N` | 搜索时最多搜索 N 级目录。 |
| `-mount (或 -xdev)` | 不要搜索其他文件系统上的目录。 |

对于测试（tests）。有很多测试可以提供给 `find`，每个测试返回 `true` 或 `false`。当 `find` 工作时，它会依次考虑它找到的每个文件，并按照定义的顺序在每个文件上应用每个测试。如果测试返回 `false`，`find` 将停止考虑当前正在查看的文件并继续下一个；如果测试返回 `true`，`find` 将对当前文件处理下一个测试或动作。我们在下表中列出的测试是最常见的；请参阅手册页以获取你可以应用的可能测试的详细列表。

| 测试 | 含义 |
| :--- | :--- |
| `-atime N` | 文件在 N 天前访问过。 |
| `-mtime N` | 文件在 N 天前被修改过。 |
| `-name pattern` | 文件名匹配模式，模式必须用引号括起来。 |
| `-newer otherfile` | 文件比 otherfile 新。 |
| `-type C` | 文件类型为 C；常见的类型有“d”表示目录，“f”表示普通文件。 |
| `-user username` | 文件由用户所有。 |

## 第 2 章

我们还可以使用运算符组合测试。大多数测试有两种形式：短形式和较长形式：

| 运算符短形式 | 运算符长形式 | 含义 |
| :--- | :--- | :--- |
| `!` | `-not` | 反转测试。 |
| `-a` | `-and` | 两个测试都为真。 |
| `-o` | `-or` | 任一测试为真。 |

我们可以通过括号来强制测试的优先级。由于这些对 shell 有特殊含义，我们还必须使用斜杠引用括号。此外，如果我们对文件名使用模式，使用引号以确保名称不会被 shell 解析而是直接传递给命令。如果我们想编写“比文件 `X` 新或以下划线开头的名称”的测试，我们将写：

```bash
\(-newer X -o -name "_*"
```

我们下一个工作原理部分之后展示一个示例。

## 尝试——带测试的 find

让我们尝试在当前目录中搜索比文件更更新的文件：

```bash
$ find . -newer while2 -print
./elif3
./words.txt
./words2.txt
./_trap
$
```

这看起来不错，但我们也找到了当前目录，这是我们不需要的。所以我们加上 `-type f`：

```bash
$ find . -newer while2 -type f -print
./elif3
./words.txt
./words2.txt
./_trap
$
```

## 工作原理

它是如何工作的？我们指定 `find` 在当前目录（`.`）中搜索比文件新的（`-newer while2`）文件（`-type f`）。

解释可能不太容易理解，但一个示例会让情况更清晰。

让我们看一个更简单的例子，使用安全的命令 `ls`：

```bash
$ find . -newer while2 -type f -ls -1 \;
-rwxr-xr-x 1 rick rick 275 Feb 8 17:07 ./elif3
-rwxr-xr-x 1 rick rick 336 Feb 8 16:52 ./words.txt
-rwxr-xr-x 1 rick rick 1274 Feb 8 16:52 ./words2.txt
-rwxr-xr-x 1 rick rick 504 Feb 8 18:43 ./_trap
$
```

正如你所见，`find` 命令非常有用；只需要练习就能使用它。然而，这种练习将带来丰厚的回报，所以尝试 `find` 命令。
