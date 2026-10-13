
你可以使用此脚本列出 tar 文件（tar 是 tape archive 的缩写，是在 UNIX 中分发文件的常见格式）的内容，或根据脚本被调用的名称创建 tar 文件。待读取或创建的 tar 文件指定为脚本的第一个参数 $1。

让我们将此脚本命名为 mytar，并为其创建两个符号链接，分别命名为 listtar 和 maketar，如下所示：

```
$ ln -s mytar listtar
$ ln -s mytar maketar
```

如果脚本以 maketar 的名称被调用并给定一个目录或文件名，它将创建包含该目录或文件内容的 tar 文件。假设你有一个名为 fruits 的目录，其内容如下：

```
$ ls fruits
apple banana mango peach pear
```

你可以将脚本作为 maketar 调用，以获得包含此目录的名为 fruit.tar 的 tar 文件，方法是发出以下命令：

```
$ ./maketar fruits
```

如果要列出此命令创建的 tar 文件的内容，可以按如下方式调用脚本：

```
$ ./listtar fruits.tar
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/apple
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/banana
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/mango
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/pear
rw-r--r-- 500/100 0 Nov 17 08:48 1998 fruits/peach
```

确切的输出取决于系统上 tar 的版本。某些版本包含比此处显示更详细的输出。

## 使用说明

$0 的另一个常见用途是在脚本的使用说明中。使用说明是脚本输出的简短消息，用于告知用户脚本的正确调用语法。所有供多位用户使用的脚本都应包含使用说明。

通常，使用说明类似于以下内容：

```
echo "Usage: $0 [options][files]"
```

回到 mytar 脚本，添加使用说明会很有帮助，特别是如果脚本以 listtar 或 maketar 以外的名称执行时。你可以按如下方式实现此更改：

```
case $0 in
  "*listtar") TARGS="-tvf $1" ;;
  "*maketar") TARGS="-cvf $1.tar $1" ;;
  *) echo "Usage: $0 [file/directory]" ; exit 0 ;;
esac
```

现在如果脚本被调用为例如 mytar，它将输出以下消息：

Usage: mytar [file/directory]

此消息正确描述了脚本的使用方法，但没有告知你脚本的名称被错误给出。有两种可能的纠正方法：

- 在使用说明中硬编码有效名称
- 修改脚本使其使用其参数来决定应以何种模式运行

为演示选项的使用，下文将使用后一种方法。

## 选项和参数

选项在命令行中给出以更改脚本或程序的行为。例如，ls 命令的 -a 选项会将 ls 命令的行为从列出所有可见文件更改为列出所有文件（如第 3 章所述）。本节将向你展示如何使用选项来更改脚本的行为。

通常你会看到或听到选项被称为参数。两者之间的区别很微妙。命令的参数是命令行中命令名称之后出现的所有单独字符串或单词，而选项只是那些改变命令行为的参数。

例如，在以下示例中：

```
$ ls -aF fruit
```

命令是 ls，其参数为 -aF 和 fruit。ls 命令的选项为 -aF。

## 处理参数

为说明选项的使用，让我们更改 mytar 脚本，使其使用第一个参数 $1 作为模式参数，$2 作为要读取或创建的 tar 文件。你可以按如下方式实现此更改：

```
USAGE="usage: $0 [-c|-t] [file|directory]"
case "$1" in
  -t) TARGS="-tvf $2" ;;
  -c) TARGS="-cvf $2 $2" ;;
  *) echo "$USAGE"
     exit 0
     ;;
esac
```

三个主要更改如下：

- 所有对 $1 的引用都已更改为 $2，因为现在第二个参数是文件名。
- listtar 已被 -t 替换。
- maketar 已被 -c 替换。

现在运行 mytar 会产生以下输出：

Usage: ./mytar [-c|-t] [file|directory]

要使用此版本创建目录 fruits 的 tar 文件，请使用以下命令

```
$ ./mytar -c fruits
```

要列出生成的 tar 文件 fruits.tar 的内容，请使用以下命令

```
$ ./mytar -t fruits
```

## 使用 basename

目前，mytar 的使用说明输出脚本被调用时使用的完整路径。它真正应该输出的只是脚本的名称。你可以使用 basename 命令来纠正此问题。

basename 命令接受文件或目录的绝对或相对路径名，并从该路径返回仅文件或目录名。基本语法如下：

```
basename file
```

例如，

```
$ basename /usr/bin/sh
```

打印以下内容：

```
sh
```

使用 basename，你可以按如下方式更改 mytar 脚本中的变量 $USAGE：

```
USAGE="Usage: basename $0 [-c|-t] [file|directory]"
```

以便使用说明产生期望的输出：

```
Usage: mytar [-c|-t] [file|directory]
```

你也可以在 mytar 脚本的第一版本中使用 basename 命令，以避免在 case 语句中使用 * 通配符字符：

```
#!/bin/sh
case `basename $0` in
listtar) TARGB="-tvf $1" ;;
maketar) TARGB="-cvf $1.tar $1" ;;
*) echo "Usage: $0 [file|directory]"
exit 0
esac
tar $TARGB
```

在此版本中，basename 允许你匹配脚本可以被调用的确切名称。作为原始版本潜在问题的说明，你可以看到如果脚本被调用为

```
$ ./makelisttar
```

原始版本将使用第一个 case 语句，即使它是错误的，但新版本将落到后面并报告错误。

## 模拟 basename

一些较旧的 Linux 和 BSD 系统不包含 basename 命令。如果使用此类系统，你可以通过创建提供等效功能的 shell 脚本来模拟此命令。basename 的 shell 脚本版本可能如下所示：

```
#!/bin/sh
if [ -n "$1" ] ; then
echo "$1" | sed 's/.*\/[^\/]*$/'
else
echo 'Usage: basename [file]' >&2
exit 1
fi
exit 0
```

如果不理解 sed 命令的工作原理也不必担心。你将在第 16 章“使用正则表达式过滤文本”中阅读更多相关内容。

## 常见参数处理问题

现在 mytar 脚本使用选项来设置脚本运行的模式，你需要解决另一个问题。也就是说，如果未提供第二个参数 $2，该怎么办？你不必担心如果未提供第一个参数 $1 会发生什么，因为 case 语句通过默认 case * 处理这种情况。

检查所需参数数量的最简单方法是查看参数数量 $# 是否与所需参数数量匹配。你可以按如下方式将此检查添加到脚本中：

```
#!/bin/sh

USAGE="Usage: basename $0 [-c|-t] [file|directory]"

if [ $# -lt 2 ] ; then
    echo "$USAGE"
    exit 1
fi

case "$1" in
    -t) TARGS="-tvf $2" ;;
    -c) TARGS="-cvf $2 $2" ;
    *) echo "$USAGE"
    exit 0
    ;;
esac

tar $TARGS
```

## 处理额外文件

mytar 脚本基本完成，但仍可进行一些改进。例如，它仅处理作为参数给出的第一个文件，并且不会确定该参数是否真的是文件。

你可以通过使用特殊的 shell 变量 $@ 来添加对所有文件参数的处理。让我们首先修改 -t 选项以使用此变量：

```
case "$1" in
    -t) TARGS="-tvf"
        for i in "$@"
        do
            if [ -f "$i" ] ; then
                tar $TARGS "$i"
            fi
        done
        ;;
    -c) TARGS="-cvf $2 $2" ;
```

```
tar $TARGS
;;
*) echo "$USAGE" ;
exit 0
;;
esac
```

主要更改是

- -t case 现在包含一个处理参数的 for 循环。
- for 循环中有一个 if 语句，用于确定参数是否为文件。如果参数是文件，则对该文件执行 tar。

> **$* and $@**
> shell 脚本中指定的参数存储在两个特殊变量 $* 和 $@ 中。这两个特殊变量的主要区别在于它们存储参数的方式：$* 在不保留引用的情况下存储每个参数，而 $@ 在保留引用的情况下存储每个参数。
> 
> $* 的行为有时会引起问题。例如，如果你的脚本有一个包含空格的文件名作为参数：
> mytar -t 'my tar file.tar'
> 使用 $* 而不是 $@ 会造成问题，因为 for 循环将针对名为 my、tar 和 file.tar 的文件执行三次，而不是仅针对你请求的文件 my tar file.tar 执行一次。通过使用 $@，你可以避免此问题，因为每个参数都按其在命令行上被引用的方式存储。

## 一些小问题

mytar 中有两个小问题需要处理：

- mytar 将其所有参数，包括第一个参数 $1，视为文件。因为你使用第一个参数来指示脚本运行的模式，所以不应将其视为文件。这将减少 for 循环的执行次数，并防止脚本尝试对名为 -t 的文件运行 tar。
- 另一个问题涉及脚本在操作失败时应做什么。在列出操作的情况下，如果 tar 无法列出文件的内容，你应跳过该文件并打印错误。
