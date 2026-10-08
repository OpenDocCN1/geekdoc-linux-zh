

# hashstat — 目录内容的内部哈希表

# 摘要

```csh
hashstat
```

# 描述

参见 hash(1)。

# head — 显示文件的前几行

# 摘要

```
/usr/bin/head [-number | -n number] [filename...]
```

# 描述

head 命令将每个文件名的前指定行数复制到标准输出。如果你未指定文件名，head 将从标准输入读取行。number 的默认值为 10 行。

当你指定了多个文件名时，每个文件的开头都会显示在两个箭头之间的文件名，如下所示。

```
== filename <=
```

以下示例展示了显示一组短文件的常用方法，通过名称识别每个文件。
```
castle@ head -9999 kookaburra1 kookaburra2
== kookabral <=
kookaburra sits in the old gum tree
Merry king of the bush is he
Laugh, kookaburra, laugh, kookaburra
Gay your life must be.
```

```
== kookaburra2 <=
kookaburra sits in the old gum tree
Eating all the gumdrops he can see
Stop, kookaburra, stop, kookaburra
Leave some there for me.

kookaburra sits in the old gum tree
```

```
Eating all the gumdrops he can see
Stop, kookaburra, stop, kookaburra
Leave some there for me.
castle@
```

# 选项

- -n number: 将输入文件的前 *number* 行复制到标准输出。将 *number* 参数指定为正十进制整数。
- -number: 将 *number* 行数指定为正十进制整数，效果与 *-n number* 选项相同。如果没有指定任何选项，head 使用默认值 *-n 10*。

# 操作数

- file: 输入文件的路径名。如果未指定操作数，则使用标准输入。

# 使用

参见 largefile(5) 以了解 head 在遇到大于或等于 2 Gbytes (**=31 bytes**) 的文件时的行为。

# 示例

以下示例写入目录中所有文件（以点开头的文件除外）的前 10 行内容。
```
example@ head *
```

# 环境变量

参见 environ(5) 以获取影响 head 执行的环境变量描述：LC_TYPE, LC_MESSAGES 和 NLPATH。

# 退出状态

- 0: 成功完成。
- >0: 发生错误。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNMcu |
| CSI | Enabled |

# 参见

cat(1), more(1), pg(1), tail(1), attributes(5), environ(5), largefile(5)。

# help, sccs-help — 请求 SCCS 错误或警告消息帮助

# 摘要

```
/usr/ccs/bin/help [argument]...
```

# 描述

参见 sccs-help(1)。

# history, fc — 处理命令历史列表

# 摘要

```
sh
/usr/bin/fc [first][last]
/usr/bin/fc -1 [-nr] [first][last]
/usr/bin/fc -s [old=new] [first]
```

```csh
history [-hr] [n]
```

# ksh

```
fc -e [old=new] [command]
fc -e editor [-nlr] [first][last]
```

# 描述

命令历史会创建一个你你最近使用的命令的编号列表。你可以显示这些命令并按原始发布的方式重新使用它们。你也可以通过编辑来更改命令。history 命令的语法和参数在每个 shell 中不同。

# /usr/bin/fc

fc 命令列出或编辑之前之前输入到交互式 shell 中的命令。
命令历史列表通过数字引用命令。列表中的第一个数字是任意指定的。数字与其命令之间的关系不会改变，除非你登录且没有其他进程访问该列表，此时系统可能会重置编号，从最旧的保留命令（通常为 1）开始计数。当数字达到 HISTORYSIZE 或 128（取较大者）的值时，它可能会循环数字，从较小的数字（通常为 1）开始执行下一个命令。尽管有这种可选的循环，fc 仍维持着命令的时间顺序序列。例如，如果按顺序执行的四个命令编号分别为 32766、32767、1（循环）和 2，那么命令 32767 被视为命令 1 的上一个命令，尽管它的编号

当你编辑命令且没有指定 -l 选项时，生成的行将输入历史列表的末尾，然后由 sh 重新执行。fc 编辑命令不会输入历史列表。如果编辑器返回非零退出状态，则返回该状态。进入历史列表并重新执行之前的命令。在重定向时，命令行变量赋值或重定向操作符会影响 fc 本身以及之前的命令。

```
$ fc -s --2dev/null
```

# C Shell

使用 history 命令显示历史列表；如果你指定数字 n，则只显示历史。

# 历史替换

! 字符允许你从历史列表中替换命令行的一部分。语法为 `![-string][:replacement]`。

- !string: 执行以 string 开头的最近命令。
- !string:replacement: 执行包含 string 的最近命令，将其替换为 replacement。
- !! 执行上一个命令。
- !n: 执行最近的 n 个命令。
- !-n: 反向执行最近 n 个命令。
- !?: 执行匹配模式的最近命令。
- !?:replacement: 执行匹配模式的最近命令，将匹配项替换为 replacement。

# 事件标识符

事件标识符是对历史列表中命令的引用。冒号将事件规范与单词标识符分开。如果单词标识符以 * 或 % 开头，可以省略冒号。如果从上一个命令选择单词，可以省略事件规范中的第二个 ! 字符。例如，!!1 和 !1 都指向上一个命令的第一个单词，而 !! 和 !$ 都指向上一个命令的最后一个单词。单词标识符包括：

- # 目前输入的整个命令行。
- 0 第一个单词（命令）。
- n 第 n 个参数。
- ^第一个参数，即 1。
- $ 最后一个参数。
- % 最近 ? 搜索匹配的单词。
- x-y 单词范围；-y- 简化 0-y。
- * 所有参数，如果事件中只有一个单词。
- x* 简化 x-.

# 修饰符

在可选的单词标识符之后，你可以添加一个或多个以下修饰符，每个修饰符前都有一个冒号 (:)。

- h 移除结尾的路径名组件，留下头部。
- r 移除 .xxx 格式的结尾后缀，留下基名。
- e 移除除后缀以外的所有内容，留下扩展名。

