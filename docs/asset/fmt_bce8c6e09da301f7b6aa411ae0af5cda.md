
### 在正则表达式中使用字符范围

尝试以下命令：

```
:/Linux/p
```

Linux 酷毙了。  
Linux 现在已经 10 岁了。  
我的妹妹 Rani 从不使用 Linux

这只会找到 `Linux` 而不会找到 `linux`，为了解决这个问题，请尝试以下操作：

```
:/Linux]/p
```

我喜欢 `linux`。  
我的兄弟 Vikrant 也喜欢 `linux`，他也很喜欢 `unix`。  
他现在正在学习 `linux`。  
`Linux` 酷毙了。  
`Linux` 现在已经 10 岁了。  
明年 `linux` 将有 11 岁了。  
我的妹妹 Rani 从不使用 `Linux`。  
`.` (DOT) 是 `linux` 的特殊命令。

这里有一个使用 `[` 和 `]` 的字符列表，它可以匹配该范围内的任意字符。如果列表的第一个字符是 `^`，则它匹配不在列表中的任何字符。例如在 `[Li]`，它将尝试与模式的其余部分匹配 L 或 l。让我们来看另一个例子。假设你想匹配范围内的单个数字字符，可以输入如下命令：

```
/:[0123456789]
```

你甚至可以这样尝试：

```
:/g[0-9]
```

`Linux` 现在已经 10 岁了。  
明年 `linux` 将有 11 岁了。

这里的数字范围通过提供第一个数字（0-zero）和最后一个数字（1）并用连字符分隔来指定。你可以尝试 `[a-z]` 来匹配小写字母，`[A-Z]` 来匹配大写字母。不仅如此，还有某些预定义的命名字符类。它们如下：

| 预定义字符类 | 含义 |
|---|---|
| `[[:alnum:]]` | 字母和数字 (A 到 Z 或 a 到 z 0 到 9) |
| `[[:alpha:]]` | 字母 A 到 Z 或 a 到 z |
| `[[:cntrl:]]` | 删除字符或普通控制字符 (0x7F 或 0x00 到 0x1F) |

### 数字 (0 到 9)

| 预定义字符类 | 含义 |
|---|---|
| `[[:digit:]]` | 数字 |
| `[[:graph:]]` | 可打印字符，如 print，但排除空格字符 |
| `[[:lower:]]` | 小写字母 (a 到 z) |
| `[[:print:]]` | 可打印字符 (0x20 到 0x7E) |
| `[[:punct:]]` | 标点字符 (控制或空格) |
| `[[:space:]]` | 空格、制表符、回车、换行、垂直制表符或分页 (0x0D, 0x20) |
| `[[:upper:]]` | 大写字母 (A 到 Z) |
| `[[:xdigit:]]` | 十六进制数字 (0 到 9, A 到 F, a 到 f) |

例如，为了查找数字或字母（包括大小写），你会写：

```
/[0-9A-Za-Z]
```

与其编写这样的命令，你可以轻松地使用预定义的类或范围：

```
[:alnum:]
```

## . (点) 匹配任意单个字符

例如，输入以下命令：

```
:g/.
```

她只喜欢玩游戏，别的一律。

你知道吗？  
将包含 lo(ves), Do, no(thing) 等。

- `*` 匹配 0 次或多次

例如，输入以下命令：

```
:g/l*
```

Hello World.  
This is vivek from Poona.  
....  
....

```
:g/Li*
```

`Linux` is coooool.  
`Linux` 现在已经 10 岁了。  
我的妹妹 Rani 从不使用 `Linux`

```
:g/c.*and
```

`.` (DOT) 是 `linux` 的特殊字符。

这里匹配第一个字符 `c`，然后是任意单个字符，后面跟着 `n` 个单个字符（1 次或 100 次），最后以 `and` 结尾。这可以根据命令找到不同的单词，如 `command` 或 `catad enc`。

在正则表达式元字符中，如 `.` (DOT) 或 `*`，如果我们使用 `\.` 或 `\*`，它们将失去特殊含义。反斜杠消除了此类元字符的特殊含义，你可以将其作为普通字符使用。例如，如果你想在行开头搜索 . (DOT)，你可以使用：

```
:g/^\.
```

Hello World.  
This is vivek from Poona.  
...  
...  
(DOT) 是 `linux` 的特殊命令。  
好了！我会停的。  
与其那样，不如使用

```
:g/^\.
```

(DOT) 是 `linux` 的特殊命令。

### 使用 & 作为替换字符

尝试以下命令：

```
:1,$s/Linux/&
```

我的妹妹 Rani 从不使用 `Linux`  
`Linux` 酷毙了。  
`Linux` 现在已经 10 岁了。  
我的妹妹 Rani 从不使用 `Linux`  
此命令将目标模式 `"Linux"` 替换为 `"Linux"`。 `&` 在前面意味着用给定的模式替换“上一次找到的模式”，这里上一次找到的模式是 `"Linux"`，它与给定的模式一起使用（最终构建 `"Linux"`）。你能猜到这个命令的输出吗？

```
:1,$s/Linux/&/p
```

恭喜你，成功完成。

## awk 基础

```
$ awk '{ print $2 }' inven
```

Pen  
Pencil  
Rubber  
Cock

`awk` 打印文件的第二个字段。如果你想打印文件的第二个和第四个字段，可以执行以下命令：

```
$ awk '{ print $2 $4 }' inven
```

Pen20.00  
Pencil20.00  
Rubber3.50  
Cock45.00

`$0` 是 `awk` 的特殊变量，用于打印整条记录。你可以通过执行以下 `awk` 命令来验证这一点：

```
$ awk '{ print $0 }' inven
```

1. Pen 5 20.00  
2. Pencil 10 2.00  
3. Rubber 3 3.50  
4. Cock 2 45.50

你也可以像下面所示创建 `awk` 命令（程序）文件：

```
$ cat > prn_pen
/Pen/ { print $3 }
```

然后你可以按照如下方式执行或运行上述 `prn_pen` awk 命令文件：

```
$ awk -f prn_pen inven
```

5  
10

在上面的 `awk` 程序中，`/Pen/` 是搜索模式，如果在行（或记录）中找到了该模式，则打印记录的第三个字段。`{ print $3 }` 被称为动作（Action）。在 shell 提示符下，`$ awk -f prn_pen inven` 中，`-f` 选项指示 `awk` 从指定文件中读取命令，`inven` 是用作 `awk` 输入的数据库文件名。

现在按照如下方式创建下述 `awk` 程序：

```
$ cat > comp_inv
$3 > 5 { print $0 }
```

按照如下方式运行：

```
$ awk -f comp_inv inven
```

2. Pencil 10 2.00

在这里，数据库的第三个字段与 `5` 进行了比较，这就是模式。如果在数据库的任何行中找到了该模式，则打印整条记录。

## 重温 awk

### awk 的预定义变量

`# # # Linux Shell 脚本教程 (LSST) v1.05r3`  
第 7 章：重温 `awk`

### awk 的预定义变量

我们的下一个示例将更多地讨论 `awk` 的预定义变量。按照如下方式创建 `awk` 文件：

```awk
$ cat > def_var
{
  print "Printing Rec. # NR "($0 "),And # of field for this record is " NF"
}
```

按照如下方式运行。

```awk
$ awk -f def_var inven
Printing Rec. #1( Pen 5 20.00),And # of field for this record is 4
Printing Rec. #2( Pencil 10 2.00),And # of field for this record is 4
Printing Rec. #3( Rubber 3 3.5 30.00),And # of field for this record is 4
Printing Rec. #4( Cock 2 45.50),And # of field for this record is 4
```
