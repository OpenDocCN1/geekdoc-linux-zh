

## 表 4.11 GNU grep 选项，适用于所有变体（-G、-E 和 -F）（续）

| 选项 | 其作用 |
|---|---|
| -L, --files-without-match | 仅打印模式不匹配的所有文件名称。 |
| -l, --files-with-matches | 仅打印模式匹配的所有文件名称。 |
| -m #, --max-count=# | 如果文件是标准输入或普通文件，则在匹配指定数量（#）的行后停止读取该文件。 |
| -n, --line-number | 在输出的每一行前加上匹配发生所在的行号。 |
| -q, --quiet | 抑制正常输出。可替代 -n 使用。 |
| -r, -R, --recursive, --directories=recurse | 对于列出的目录，递归读取并处理这些目录中的所有文件；即从该目录向下树形结构中的所有目录。 |
| -s, --silent | 抑制关于不存在或无法读取的文件的错误消息。 |
| -v, --invert-match | 反转匹配的含义，以选择不匹配的行。 |
| -w, --word-regexp | 仅选择包含匹配项为单词的行。匹配项为包含字母、数字和下划线的字符串，且位于词边界。 |
| -x, --line-regexp | 仅选择完全匹配整行的匹配项。 |
| -y | -i 的过时同义词。 |
| -U, --binary | 将文件视为二进制。此选项仅在 MS-DOS 和 MS-Windows 上受支持。 |
| -u, --unix-byte-offsets | 报告 UNIX 风格的字节偏移。此选项只有在同时使用 -b 选项时才有效；它仅在 MS-DOS 和 MS-Windows 上受支持。 |
| -Z, --null | 在文件名的末尾放置 ASCII 空字符，而不是换行符。 |

## 4.13 带选项的 grep（UNIX 和 GNU）

grep 命令有许多选项控制其行为。并非所有 UNIX 版本都支持完全相同的选项，因此请务必查阅你的手册页以获取完整列表。

本节中的示例使用以下数据文件，为方便起见会定期重复。

| % cat datafile | | | | | | |
| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 23 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southern | SO | Suan Chin | 5.1 | .95 | 4 | 15 |
| southeast | SE | Patricia Hemenway | 4.0 | .7 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

### 示例 4.53

```
% grep -n "^south" datafile
3:southwest    SW    Lewis Dalsass    2.7  .8  2  18
4:southern     SO    Suan Chin        5.1  .95 4  15
5:southeast    SE    Patricia Hemenway 4.0  .7  4  17
```

### 解释

-n 选项在每一行前加上找到模式的行号，然后是该行。

### 示例 4.54

```
% grep -i 'pat' datafile
southeast    SE    Patricia Hemenway 4.0  .7  4  17
```

### 解释

-i 选项关闭大小写敏感。表达式 pat 中的字母无论是大写还是小写组合均无关紧要。

### 示例 4.35

```
% grep -v 'Suan Chin' datafile
```

| northwest | NW | Charles Main | 3.0 | .98 | 3 | 34 |
| western | WE | Sharon Gray | 5.3 | .97 | 5 | 22 |
| southwest | SW | Lewis Dalsass | 2.7 | .8 | 2 | 18 |
| southeast | SE | Patricia Hemenway | 4.0 | .77 | 4 | 17 |
| eastern | EA | TB Savage | 4.4 | .84 | 5 | 20 |
| northeast | NE | AM Main Jr. | 5.1 | .94 | 3 | 13 |
| north | NO | Margot Weber | 4.5 | .89 | 5 | 9 |
| central | CT | Ann Stephens | 5.7 | .94 | 5 | 13 |

### 解释

这里，-v 选项打印所有不包含模式 Suan Chin 的行。此选项用于从输入文件中删除特定条目时。要真正删除该条目，你需要将 grep 的输出重定向到临时文件，然后将临时文件的名称改回原始文件的名称，如下所示：

```
grep -v 'Suan Chin' datafile > temp
mv temp datafile
```

请记住，在将输出从 datafile 重定向时必须使用临时文件。如果你将 datafile 重定向到 datafile，shell 会“破坏”datafile。（参见第 25 页的“重定向”。）

### 示例 4.56

```
% grep -l 'SE' *
datafile
datebook
```

### 解释

-l 选项使 grep 仅打印找到模式的文件名，而不是文本行。

### 示例 4.57

