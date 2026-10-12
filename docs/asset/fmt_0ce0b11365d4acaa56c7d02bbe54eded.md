
My brother Vikrant also loves linux who loves unix.

末尾的`g`选项指示对地址行内目标模式的所有出现处执行替换。

### 搜索单词
### 替换单词为
### 带有确认的替换

#### # Linux 脚本编程教程 (LSST) v1.05r3
#### 第 6 章：使用 ex 学习表达式

##### # # 带有确认的替换

给出如下命令：

```
:/Linux/ s/UNIX/gc
```

给出此命令后会问你 - 替换为 UNIX (y/n/a/q)?
输入`y`替换单词，`n`不替换，或`a`替换单词的所有出现处。

#### # Linux 脚本编程教程 (LSST) v1.05r3
#### 第 6 章：使用 ex 学习表达式

##### # # 查找单词

命令如：

```
:the/p
```

它与所有操作系统都不同。
我的兄弟 Vikrant 也喜欢 linux 喜欢 unix。

会找到像 theater, brother, other 等单词。如果你想查找单词 "the" 呢？要查找单词（假设是 Linux），你可以给出如下命令：

```
:<Linux>
Linux is coooool.
:g^<Linux>/p
Linux is coooool.
Linux is now 10 years old.
Rani my sister never uses Linux
```

符号`<`和`>`分别匹配单词开头和结尾的空字符串。要找到开头包含 Linux 模式的行，给出命令：

```
/:^Linux
Linux is coooool.
```

如你所知，`$`是行结束字符，`^`（脱字符）匹配行开头。要找到行开头所有出现处的 "Linux"，给出命令：

```
:g^Linux
Linux is coooool.
Linux is now 10 years old.
```

如果你想在行末尾查找 "Linux"，则给出命令：

```
/:Linux $
Rani my sister never uses Linux
```

以下命令将找到空行：

```
/:^
```

要找到所有空行给出命令：

```
:g/^$
```

要查看不带空行的整个文件，你可以使用如下命令：

```
:g![^/$]
Hello World.
This is vivek from Poona.
I love linux.
它与所有操作系统都不同
```

#### # LSSST v1.05 > 第 6 章 > 查找单词

我的兄弟 Vikrant 也喜欢 喜欢 unix。
他目前正在学习 linux。
Linux 是酷的。
Linux 现在已经 10 岁了。
明年 linux 将有 11 岁了。
我的妹妹 Rani 永远不使用 Linux
她只喜欢玩游戏，别的都不管。
你知道吗？
`.` (DOT) 是 linux 的特殊命令。
好了！我要停止了。

| 命令 | 解释 |
|---|---|
| `g` | 所有出现处 |
| `/[^` | `[^]` 这意味着不 |
| `^\$` | 空行，`^` 和 `$` 的组合。 |

要删除所有空行可以给出如下命令：

```
:g^$/d
好了！我要停止了。
:1,$s p
```

```
Hello World.
This is vivek from Poona.
love linux.
它与所有操作系统都不同
我的兄弟 Vikrant 也喜欢 linux 喜欢 unix。
Linux 是 coooool。
Linux 现在 noow 10 岁了。
```

尝试`u`命令来撤销，撤销你所做的操作，给出如下命令：

```
:u
:1,$s p
Hello World.
This is vivek from Poona.
...
....
...
好了！我要停止了。
```

### 在正则表达式中使用字符范围

尝试以下命令：

```
:/Linux/p
Linux 酷毙了。
Linux 现在已经 10 岁了。
我的妹妹 Rani 从不使用 Linux
```

这只会找到 "Linux" 而不会找到 "linux"，为了解决这个问题，请尝试以下操作：

```
:/Linux]/p
我喜欢 linux。
我的兄弟 Vikrant 也喜欢 linux，他也很喜欢 unix。
他现在正在学习 linux。
Linux 酷毙了。
Linux 现在已经 10 岁了。
明年 linux 将有 11 岁了。
我的妹妹 Rani 从不使用 Linux。
. (DOT) 是 linux 的特殊命令。
```

这里有一个使用`[`和`]`的字符列表，它可以匹配该范围内的任意字符。如果列表的第一个字符是`^`，则它匹配不在列表中的任何字符。例如在`[Li]`，它将尝试与模式的其余部分匹配 L 或 l。让我们来看另一个例子。假设你想匹配范围内的单个数字字符，可以输入如下命令：

```
/:[0123456789]
```

你甚至可以这样尝试：

```
:/g[0-9]
Linux 现在已经 10 岁了。
明年 linux 将有 11 岁了。
```

这里的数字范围通过提供第一个数字（0-zero）和最后一个数字（1）并用连字符分隔来指定。你可以尝试`[a-z]`来匹配小写字母，`[A-Z]`来匹配大写字母。不仅如此，还有某些预定义的命名字符类。它们如下：

| 预定义字符类 | 含义 |
|---|---|
| `[:alnum:]` | 字母和数字 (A 到 Z 或 a 到 z 0 到 9) |
| `[[:alpha:]]` | 字母 A 到 Z 或 a 到 z |
| `[[:cntrl:]]` | 删除字符或普通控制字符 (0x7F 或 0x00 到 0x1F) |

### 数字 (0 到 9)

| | |
|---|---|
| `[:digit:]` | 数字 |
| `[:graph:]` | 可打印字符，如 print，但排除空格字符 |
| `[:lower:]` | 小写字母 (a 到 z) |
| `[:print:]` | 可打印字符 (0x20 到 0x7E) |
| `[:punct:]` | 标点字符 (控制或空格) |
| `[:space:]` | 空格、制表符、回车、换行、垂直制表符或分页 (0x0D, 0x20) |
| `[:upper:]` | 大写字母 (A 到 Z) |
| `[:xdigit:]` | 十进制数字 (0 到 9, A 到 F, a 到 f) |

例如，为了查找数字或字母（包括大小写），你会写：

```
/[0-9A-Za-Z]
```

与其编写这样的命令，你可以轻松地使用预定义的类或范围：

```
[:alnum:]
```

## . (点) 匹配任意单个字符。

例如，输入以下命令：

```
:g/.
她只喜欢玩游戏，别的一律。
```

你知道吗？
将包含 lo(ves), Do, no(thing) 等。

- `*` 匹配 0 次或多次

例如，输入以下命令：

```
:g/l*
Hello World.
This is vivek from Poona.
....
....
```

```
:g/Li*
Linux is coooool.
Linux 现在已经 10 岁了。
我的妹妹 Rani 从不使用 Linux
```

```
:g/c.*and
.(DOT) 是 linux 的特殊字符。
```

这里匹配第一个字符`c`，然后是任意单个字符，后面跟着`n`个单个字符（1 次或 100 次），最后以`and`结尾。这可以根据命令找到不同的单词，如`command`或`catad enc`。

在正则表达式元字符中，如`.` (DOT) 或`*`，如果我们使用`\.`或`\*`，它们将失去特殊含义。反斜杠消除了此类元字符的特殊含义，你可以将其作为普通字符使用。例如，如果你想在行开头搜索`.` (DOT)，你可以使用：

```
:g/^
Hello World.
This is vivek from Poona.
...
...
(DOT) 是 linux 的特殊命令。
好了！我会停的。
```

与其那样，不如使用：

```
:g/^.
(DOT) 是 linux 的特殊命令。
```

### 使用 & 作为替换字符

尝试以下命令：

```
:1,$s/Linux-&
```

```
我的妹妹 Rani 从不使用 Linux
Linux 酷毙了。
Linux 现在已经 10 岁了。
我的妹妹 Rani 从不使用 Linux
```

此命令将目标模式 "Linux" 替换为 "Linux"。 `&` 在前面意味着用给定的模式替换“上一次找到的模式”，这里上一次找到的模式是 "Linux"，它与给定的模式一起使用（最终构建 "Linux"）。你能猜到这个命令的输出吗？

```
:1,$s/Linux/&/p
```
