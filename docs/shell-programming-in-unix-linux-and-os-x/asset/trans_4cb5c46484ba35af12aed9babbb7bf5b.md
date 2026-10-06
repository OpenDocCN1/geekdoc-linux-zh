

shell 将输入到 shell 的每一行作为 `wc` 的标准输入流，直到遇到包含 `ENDOFDATA` 的行为止。

内联输入重定向（In-line input redirection——某些程序员称为“在此文档”（here documents））在 shell 程序内部使用时是一项强大的功能。它允许你直接在程序中为命令指定标准输入，无需将其写入单独的文件，或通过 `echo` 将其引入命令的标准输入。

以下是该功能在 shell 程序中用用的一个常见示例：

```
$ cat mailag
mail * <<END-OF-DATA
```

注意：

我们的每月用户小组会议
将于2016 年 3 月 4 日周五晚上 8 点
在 1A-308 会室举行。请尽量参加。

```
END-OF-DATA$$
```

要将此消息发送给存储在 `users_list` 文件中的小组所有成员，你可以调用：

```
mailmsg $(cat users_list)
```

shell 对重定向的输入数据执行参数替换，执行反引号命令，并识别反斜杠字符。

在此文档内的特殊字符通常会被忽略，但如果你在这些行中使用美元符号、反引号或反斜杠，它们可能会被解释。要让它们被忽略，请在它们前面加上反斜杠字符。或者，如果你想让 shell 保持所有输入行完全不变，可以在 `<<` 之后的文档结束词前加上反斜杠。

让我们强调一下这两者的区别：

```
$ cat <<FOOBAR
> $HOME
> ******
> \foobar
> `date
> FOOBAR Terminates the file
/users/steve
*****
$foobar
Wed Oct 2 15:23:15 EDT 2002
$
```

## 第 12 章 遗留问题

由于 shell 将直到 `FOOBAR` 为止的所有行都作为 `cat` 的输入，它替换了 `HOME` 的值而不是 `foobar`；后者前面有一个反斜杠。`date` 命令也被执行了，因为反引号被 shell 解释。

为了避免 shell 解释行的内容，请使用反斜杠作为文档结束词：

```
$ cat <<FOOBAR
 > "date"
> $HOME
> FOOBAR
> \\
> "date"
> $HOME
$
```

在选择 `<<` 之后的词时要小心。通常，只需确保它足够独特，这样它在随后的数据行中意外出现的概率就微乎其微。

你现在知道了 `<<` 序列，但还有一个大多数现代 shell 都能理解的序列：如果 `<<` 之后的第一个字符是连字符 (`-`)，则输入中的任何领先制表符都将被 shell 移除。这对于视觉上对数据行进行缩进以提高可读性，同时使其以正常的左对齐形式出现非常有用：

```
$ cat <<END
> Indented lines
> because tabs are cool
> END
```

缩进的行
因为 tab 很酷
$

## Shell 存档

内联输入重定向功能的最佳用途之一是创建 shell 存档文件。通过这种技术，可以将一个或多个相关程序放入单个文件中，然后然后使用标准的 Unix 邮件命令发送给其他人。当收到存档时，可以通过将其作为 shell 程序调用来对其“解包”。

例如，这里是 rolo 使用的 `lu`、`add` 和 `rem` 程序的存档版本：

```
$ cat rolonubs
#
# Archived programs used by rolo.
#
```

echo Extracting lu

```
cat >lu \THE-END-OF-DATA
#
# 在电话簿中查找某人
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: lu name"
    exit 1
fi

name=$1
grep $name $PHONEBOOK

if [ $? -ne 0 ];
then
    echo "I couldn't find name in the phone book"
fi
THE-END-OF-DATA

echo Extracting add
cat >add \THE-END-OF-DATA
#
# 将某添加到电话文件的程序
#

if [ "$# -ne 2 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: add name number"
    exit 1
fi

echo $1 $2 >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
THE-END-OF-DATA

echo Extracting rem
cat >rem \THE-END-OF-DATA
#
# 从电话簿中删除某人
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
```

## 第 12 章 遗留问题

```
echo "Usage: rem name"
exit 1
fi
```

name=$1

```
#
# 查找匹配条目的数量
#
```

```
matches=$(grep "$name" $PHONEBOOK | wc -l)

#
# 如果多于一个匹配，则发布消息，否则删除它
#
```

```
if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi
echo "I couldn't find name in the phone book"
```

if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi

echo "I couldn't find name in the phone book"
THE-END-OF-DATA

要将此消息发送给存储在 `users_list` 文件中的小组所有成员，你可以调用：

```
mailmsg $(cat users_list)
```

shell 对重定向的输入数据执行参数替换，执行反引号命令，并识别反斜杠字符。

在此文档内的特殊字符通常会被忽略，但如果你在这些行中使用美元符号、反引号或反斜杠，它们可能会被解释。要让它们被忽略，请在它们前面加上反斜杠字符。或者，如果你想让 shell 保持所有输入行完全不变，可以在 `<<` 之后的文档结束词前加上反斜杠。

让我们强调一下这两者的区别：

```
$ cat <<FOOBAR
> $HOME
> ******
> \foobar
> `date
> FOOBAR Terminates the file
/users/steve
*****
$foobar
Wed Oct 2 15:23:15 EDT 2002
$
```

## 第 12 章 遗留问题

由于 shell 将直到 `FOOBAR` 为止的所有行都作为 `cat` 的输入，它替换了 `HOME` 的值而不是 `foobar`；后者前面有一个反斜杠。`date` 命令也被执行了，因为反引号被 shell 解释。

为了避免 shell 解释行的内容，请使用反斜杠作为文档结束词：

```
$ cat <<FOOBAR
 > "date"
> $HOME
> FOOBAR
> \\
> "date"
> $HOME
$
```

在选择 `<<` 之后的词时要小心。通常，只需确保它足够独特，这样它在随后的数据行中意外出现的概率就微乎其微。

你现在知道了 `<<` 序列，但还有一个大多数现代 shell 都能理解的序列：如果 `<<` 之后的第一个字符是连字符 (`-`)，则输入中的任何领先制表符都将被 shell 移除。这对于视觉上对数据行进行缩进以提高可读性，同时使其以正常的左对齐形式出现非常有用：

```
$ cat <<END
> Indented lines
> because tabs are cool
> END
```

缩进的行
因为 tab 很酷
$

## Shell 存档

内联输入重定向功能的最佳用途之一是创建 shell 存档文件。通过这种技术，可以将一个或多个相关程序放入单个文件中，然后使用标准的 Unix 邮件命令发送给其他人。当收到存档时，可以通过将其作为 shell 程序调用来对其“解包”。

例如，这里是 rolo 使用的 `lu`、`add` 和 `rem` 程序的存档版本：

```
$ cat rolonubs
#
# Archived programs used by rolo.
#
```

echo Extracting lu

```
cat >lu \THE-END-OF-DATA
#
# 在电话簿中查找某人
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: lu name"
    exit 1
fi

name=$1
grep $name $PHONEBOOK

if [ $? -ne 0 ];
then
    echo "I couldn't find name in the phone book"
fi
THE-END-OF-DATA

echo Extracting add
cat >add \THE-END-OF-DATA
#
# 将某添加到电话文件的程序
#

if [ "$# -ne 2 ];
then
    echo "Incorrect number of arguments"
    echo "Usage: add name number"
    exit 1
fi

echo $1 $2 >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
THE-END-OF-DATA

echo Extracting rem
cat >rem \THE-END-OF-DATA
#
# 从电话簿中删除某人
#

if [ "$# -ne 1 ];
then
    echo "Incorrect number of arguments"
```

## 第 12 章 遗留问题

```
echo "Usage: rem name"
exit 1
fi
```

name=$1

```
#
# 查找匹配条目的数量
#
```

```
matches=$(grep "$name" $PHONEBOOK | wc -l)

#
# 如果多于一个匹配，则发布消息，否则删除它
#
```

```
if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" $PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook $PHONEBOOK
fi
echo "I couldn't find name in the phone book"
```

## Functions

现代 shell 支持函数——可以经常引用或重复使用的长或短命令序列。

要定义函数，你使用通用格式：

```
name () ... command; }
```

其中 name 是函数的名称，括号表示正在定义函数，括号之间的命令定义了函数体。每当执行函数时，都会执行这些命令。

注意，括号与第一个命令之间至少有一个空格字符，如果它们出现在同一行，则必须用分号分隔最后一个命令和花括号。

以下定义了一个名为 nu 的函数，显示登录用户的数量：

```
nu () { wc -l; }
```

像执行普通命令一样执行函数：在 shell 中输入它的名称：

```
$ nu
```

```
22
```

函数对于 shell 程序员非常有有用，可以减轻开发过程中大量的重复工作。一个关键特性：命令行函数后的参数会被分配给函数内部的位置参数 $1,$2, ...，就像任何其他命令一样。

这里有一个名为 nrrun 的函数，它在指定的文件上运行 tbl、nroff 和 lp：

```
$ nrrun () { tbl $1 | nroff -mm -tlp | lp; }
$ nrrun memo  Run it in memo
```

request id is laser1-33 (standard input)

```
$
```

函数仅存在于定义的 shell 中，无法传递给子 shell。由于函数在当前 shell 中执行，对当前目录或变量的更改在函数执行完成后仍保留，就像早早在书中探索过的 . 命令调用它一样：

```
$ db () {
> PATH=$PATH:/uxn2/data
> PS1=DB:
> cd /uxn2/data
 }
```

```
$ db
```

执行它

DB:

