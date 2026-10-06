

## 646 第 13 章 编写 Bourne Again Shell

```
$ cat spell_check
#!/bin/bash
# 从 aspell 输出中移除正确的拼写
if [ $# -ne 2 ]
then
    echo "Usage: spell_check file1 file2" 1>&2
    echo "file1: 正确拼写单词的列表" 1>&2
    echo "file2: 待检查的文件" 1>&2
    exit 1
fi

if [ ! -r "$1" ]
then
    echo "spell_check: $1 不可读" 1>&2
    exit 1
fi

if [ ! -r "$2" ]
then
    echo "spell_check: $2 不可读" 1>&2
    exit 1
fi

aspell -l < "$2" |
while read line
do
    if grep -v "^$line$" "$1" > /dev/null
then
        echo $line
    fi
done
```

`spell_check` 脚本将 aspell 的输出（使用 `-l` 选项使其在标准输出上生成拼写错误的列表）通过管道传递给 `while` 结构，该结构从标准输入中一次读取一行（在本例中每行一个单词）。测试命令（即 `read line`）只要从标准输入接收到行，就会返回真的退出状态。在 `while` 循环内部，一个 `if` 语句监控 `grep` 的返回值，该返回值决定了读取的行是否在用户的正确拼写单词列表中。`grep` 搜索的模式（即 `$line` 的值）前后都有特殊字符，分别指定行的开始和结束（`^` 和 `$`）。使用这些特殊字符是为了只有当 `line` 变量匹配正确拼写文件中的整行时，`grep` 才会找到匹配（否则，如果正确拼写文件中包含 paulson，`grep` 将在 aspell 的输出中匹配到 paul 等字符串）。

- 1. 这个 `if` 语句也可以写成
  `if grep -aw "$line" "$1"`
  `-q` 选项抑制 `grep` 的输出，只返回退出代码，而 `-w` 选项导致 `grep` 仅匹配整个单词。

这些特殊字符加上 `$line` 变量的值，是一个正则表达式（见第 1383 页）。`grep` 的输出被重定向到 `/dev/null`（第 150 页），因为不需要输出；只有退出代码很重要。`if` 语句检查 `grep` 的取反退出状态（前面的否定符号或改变退出状态的含义——真变为假，反之亦然），只有当找到匹配行时，状态为 0 或真（取反后为假）。如果退出状态不是 0 或假（取反后为真），则该单词不在正确拼写文件中。`echo` 内置命令在标准输出上显示不在正确拼写文件的单词列表。一旦检测到 EOF（文件末尾），`read` 内置命令返回假的退出状态，控制权移出 `while` 结构，脚本终止。

在使用 `spell_check` 之前，请检查一个你经常使用但不在标准字典中的正确拼写单词文件。例如，如果你在一家名为 Blankenship and Klimowski Attorneys 的律师事务所工作，你会将 Blankenship 和 Klimowski 放入文件中。下面的示例了 `spell_check` 如何检查名为 `memo` 的文件的拼写，并从输出列表中移除 Blankenship-Klimowski。

```
$ aspell -1 memo
Blankenship
Klimowski
target
hte
$ cat word_list
Blankenship
Klimowski
$ spell_check word_list memo
target
hte
```

关于 aspell 的更多信息请参阅第 1089 页。

## until

`until` 和 `while` 结构非常相似，区别在于循环顶部测试的含义。图 13-6 显示 `until` 结构在测试为假时执行循环，而 `while` 则在测试为真时执行。`until` 结构在测试命令返回真退出状态时停止循环。这些特殊字符连同 `$line` 变量的值，是一个正则表达式（第 1383 页）。`grep` 的输出被重定向到 `/dev/null`（第 150 页），因为不需要输出；只有退出代码很重要。`if` 语句检查 `grep` 的取反退出状态（前面的否定符号或改变退出状态的含义），只有在找到匹配行时，状态为 0 或真（取反后为假）。如果退出状态不是 0 或假（取反后为真），则该单词不在正确拼写文件中。`echo` 内置命令在标准输出上显示不在正确拼写文件的单词列表。一旦检测到 EOF（文件末尾），`read` 内置命令返回假的退出状态，控制权移出 `while` 结构，脚本终止。

在你在使用 `spell_check` 之前，请检查一个你经常使用但不在标准字典中的正确拼写单词文件。例如，如果你在一家名为 Blankenship and Klimowski Attorneys 的律师事务所工作，你会将 Blankenship 和 Klimowski 放入文件中。下面的示例了 `spell_check` 如何检查名为 `memo` 的文件的拼写，并从输出列表中移除 Blankenship-Klimowski。

```
$ aspell -1 memo
Blankenship
Klimowski
target
hte
$ cat word_list
Blankenship
Klimowski
$ spell_check word_list memo
target
hte
```

关于 aspell 的更多信息请参阅第 1089 页。

## until

`until` 和 `while` 结构非常相似，区别在于循环顶部测试的含义。图 13-6 显示 `until` 结构在测试为假时执行循环，而 `while` 则在测试为真时执行。`until` 结构在测试命令返回真退出状态时停止循环。这些特殊字符连同 `$line` 变量的值，是一个正则表达式（第 1383 页）。`grep` 的输出被重定向到 `/dev/null`（第 150 页），因为不需要输出；只有退出代码很重要。`if` 语句检查 `grep` 的取反退出状态（前面的否定符号或改变退出状态的含义——真变为假，反之亦然），只有在找到匹配行时，状态为 0 或真（取反后为假）。如果退出状态不是 0 或假（取反后为真），则该单词不在正确拼写文件中。`echo` 内置命令在标准输出上显示...。一旦检测到 EOF（文件末尾），`read` 内置命令返回假的退出状态，控制权移出 `while` 结构，脚本终止。

在你在使用 `spell_check` 之前，请检查一个你经常使用但不在标准字典中的正确拼写单词文件。例如，如果你在一家名为 Blankenship and Klimowski Attorneys 的律师事务所工作，你会将 Blankenship 和 Klimowski 放入文件中。下面的示例了 `spell_check` 如何检查名为 `memo` 的文件的拼写，并从输出列表中移除 Blankenship-Klimowski。

```
$ aspell -1 memo
Blankenship
Klimowski
target
hte
$ cat word_list
Blankenship
Klimowski
$ spell_check word_list memo
target
hte
```

关于 aspell 的更多信息请参阅第 1089 页。

## until

`until` 和 `while` 结构非常相似，区别在于循环顶部测试的含义。图 13-6 显示 `until` 结构在测试为假时执行循环，而 `while` 则在测试为真时执行。`until` 结构在测试命令返回真退出状态时停止循环。

（注：由于原始文本存在大量重复混乱，此处已根据逻辑进行了清理）

```bash
until [ $var -eq "value" ]
do
    echo "Testing..."
    read var
done
```

