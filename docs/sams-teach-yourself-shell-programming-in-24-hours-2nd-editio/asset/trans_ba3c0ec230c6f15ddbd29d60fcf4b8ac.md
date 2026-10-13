
你可能会想知道引用规则在这里如何适用。如果反斜杠去掉了其后字符的特殊含义，那输出中不应该只看到 n 吗？

双引号内的反斜杠只有在其前面是以下四个字符之一时才是特殊的：

- $
- `
- "
- \

双引号内的 \n 被视为两个普通字符，传递给 echo 命令作为参数。printf 命令启用了它自己的特殊字符集，这些字符由前面的反斜杠表示。传递给 printf 的 \n 告诉 printf 显示一个换行符。在此示例中，\n 必须被引用，以便反斜杠能够传递给 printf，而不是在 printf 看到它之前被移除。看看当你不引用反斜杠时会发生什么：

```
$ printf Line 1\nLine 2\n
```

这会显示：

Line 1\nLine 2n

\n 未被引用，因此 shell 在 printf 看到参数之前移除了反斜杠。因为 printf 看到的是 n 而不是 \n，所以它只是显示 n，而不是期望的换行符。

## 用于 cpio 和 find 的通配符引用

还有像 printf 这样的其他命令，它们有自己的特殊字符，必须被引用才能使 shell 不加改动地传递它们。cpio 是一个用于保存和恢复文件的命令。它允许你使用文件名扩展元字符来选择要恢复的文件。为了使 cpio 实际接收到这些元字符，它们必须像以下示例中那样被引用：

```
$ cpio -icdvum 'usr2/*' < /dev/rmt0
```

-icdvum 包含传递给 cpio 的选项，用于指定它应如何从磁带设备 (/dev/rmt0) 恢复。字符串 usr2/* 表示从磁带上的 usr2 目录恢复所有文件。再次说明，如果通配符未被引用，此命令有时仍能正确工作，因为如果在当前路径中找不到匹配的文件，shell 扩展就不会发生（在本例中，如果当前目录中没有 usr2 子目录）。最好引用这些 cpio 通配符，以确保命令每次都能正常工作。

![](img/3def70414996f811615f713b2077a154_172_0.png)

> 在使用 cpio 命令从 /dev/rmt0 等磁带设备恢复文件之前，请咨询您的系统管理员，以确保您拥有使用此类设备的足够权限。

第 18 章“其他工具”中介绍的 find 命令也支持自己的通配符。例如，在以下命令中

```
find / -name 'ch*.doc' -print
```

ch*.doc 是一个通配符模式，告诉 find 显示所有以 ch 开头并以 .doc 后缀结尾的文件名。与 shell 文件名扩展不同，此 find 命令会检查系统上的所有目录以查找匹配项。然而，通配符必须使用单引号、双引号或反斜杠进行引用，以便通配符传递给 find 而不是由 shell 扩展。

## 摘要

在本章中，你了解了三种引用类型以及何时使用它们：

- 反斜杠
- 单引号
- 双引号

此外，你还学习了几条引用规则：

- 反斜杠去掉了其后字符的特殊含义。
- 执行命令前，进行引用的字符会被移除。
- 单引号移除了所有被包含字符的特殊含义。
- 引用普通字符是无害的。
- 单引号字符串内部不能插入单引号。
- 双引号移除了大多数被包含字符的特殊含义。
- 引用可以忽略词边界。
- 不同类型的引用可以在一个命令中组合使用。
- 引用空格以将它们嵌入单个参数中。
- 引用换行符以在下一行继续命令。
- 使用引用来访问包含特殊字符的文件名。
- 引用正则表达式通配符。
- 引用反斜杠以启用 echo 转义序列。

## 问题

1. 给出一个 echo 命令来显示此消息：

`It's party time!`

2. 给出一个 echo 命令来显示包含以下字段的一行：

- 变量 `$USER` 的内容
- 一个空格
- 单词 "owes"
- 五个空格
- 一个美元符号 ($)
- 变量 `$DEBT` 的内容（该变量仅包含数字）
- 示例输出:
  `fred owes     $25`

## 术语

**转义** 对字符进行转义意味着在该字符前加上反斜杠（\）。转义可以移除 shell 命令中字符的特殊含义，也可以添加特殊含义，就像你在 echo 命令中看到的 \n 一样。反斜杠后面的字符称为转义字符。

**字面字符** 这些字符没有特殊含义，也不会导致额外操作。引用会使 shell 将通配符视为字面字符。

**元字符** 一个具有额外含义或导致 shell 或其他 UNIX 命令采取某种操作的字符。

**换行符** 这 literally 是 ASCII 值为 10 的换行字符。一般来说，换行符是 shell 的特殊字符，表示已输入完整的命令行，现在可以执行。

**引用** literally 将选定的文本用某种类型的引号括起来。当应用于 shell 命令时，引用通过将字符用单引号或双引号括起来或转义字符来禁用 shell 对特殊字符的解释。

![](img/3def70414996f811615f713b2077a154_174_0.png)

## 第 11 小时

### 流程控制

命令在 shell 脚本中执行的顺序称为脚本的流程。在你迄今为止查看的脚本中，流程始终相同，因为每次执行的是同一组命令。然而，大多数脚本需要根据一个或多个条件改变其流程。允许脚本流程有条件地改变的命令称为条件流程控制命令，或简称流程控制命令。

shell 中可用的两个主要流程控制语句是：

- if 语句
- case 语句

if 语句通常用于命令的条件执行，而 case 语句则允许根据多个模式中哪一个最先匹配变量来执行任意数量的命令序列。在本小时中，你将学习流程控制和两个条件语句。

### if 语句

if 语句根据给定条件为真还是假来执行操作。if 语句使用命令的返回码来确定条件是真还是假。返回码为零被视为真，而非零返回码被视为假。if 语句的语法如下：

```
if list1
then
list2
elif list3
then
list4
else
list5
fi
```

elif 和 else 语句都是可选的。如果有 elif 语句，就不需要 else 语句，反之亦然。if 语句可以用任意数量的 elif 语句编写。

因为 if 语句被视为一个列表，所以它也可以写在一行上：

```
if list1 ; then list2 ; elif list3 ; then list4 ; else list5 ; fi ;
```

通常这种形式仅用于简短的 if 语句。

if 语句的执行如下：

- 1. list1 is executed.
- 2. If the exit code of list1 is 0 (true), list2 is executed and the if statement terminates.
- 3. Otherwise, list3 is executed.
- 4. If the exit code of list3 is 0 (true), list4 is executed and the if statement terminates.
- 5. If the exit code of list3 is non-zero, list5 is executed.

### if 语句示例

以下示例说明了 if 语句的使用：

```
if uencode cherry.gif cherry.gif > cherry.uu ; then
echo "Encoded cherry.gif to cherry.uu"
else
echo "Error encoding cherry.gif"
fi
```

查看通过此语句的控制流程：

- 1. First, the command
- `uencode cherry.gif cherry.gif > cherry.uu`
- is executed.
- 2. If this command is successful, the command
- `echo "Encoded cherry.gif to cherry.uu"`
- is executed and the if statement exits.
- 3. Otherwise the command
- `echo "Error encoding cherry.gif"`
- is executed, and the if statement exits.

你可能已经注意到，在此示例中 if 和 then 语句都出现在同一行。大多数 shell 程序员更喜欢这样编写 if 语句，以便使语句更简洁、更易读。

### 常见错误

使用 if 语句时可能出现的四个常见错误是

- 在单行形式中省略 then 语句前的分号 (`;`)。
- 使用 else if 或 elseif 而不是 elif。
- 使用 elif 语句时省略 then 语句。
- 在 if 语句末尾写 if 而不是 fi。

这些情况下生成的错误消息因系统而异。在以下示例中显示了一个典型的错误消息；你系统上的实际错误消息可能使用略有不同的措辞。

以下示例说明了第一种类型的错误：

```
if uencode cherry.gif cherry.gif > cherry.uu then
echo "Encoded cherry.gif to cherry.uu"
else
echo "Error encoding cherry.gif"
fi
```
