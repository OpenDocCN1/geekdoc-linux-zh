
| value: "John Doe" | value: "Name required" |

图 15.5 替换验证

# 15.2 字符串处理

在处理字符串时，通常需要只编辑或处理字符串的部分内容。Korn shell 允许一组有限的字符串处理操作：复杂字符串、字符串长度确定、子字符串提取以及字符串中字符确定。

## 压缩字符串

一个常见的问题是文本文件中的额外空格。额外空格的产生有很多原因。两个非常常见的原因是文件中删除了单词以及在创建文件时输入了空格。只要 `print` 的参数没有加引号，就可以使用 `print` 命令轻松删除文本行中的额外空格。脚本 15.5 是一个非常简单的脚本，它获取第一个参数并将其打印回显示器。

### 脚本 15.5 压缩字符串参数

```
1 #!/bin/ksh
2 # Script:strDltSpaces.scr
```

（续

### 脚本 15.5 压缩字符串参数

```
3 # 此脚本使用 print 删除字符串中的额外空格。
4 # $1 是文本字符串
5 line=$1
6 print $line
$ strDltSpaces.scr "Too many spaces here."
Output:
Too many spaces here.
```

这个脚本唯一的问题是它只压缩一行。为了让它真正有用，我们需要将其放入循环中。正式版本在脚本 15.6 中。

### 脚本 15.6 压缩文件

```
1 #!/bin/ksh
2 # Script:strDltFile.scr
3 # 压缩文件中所有的行
4 # $1 是文件
5
6 cat $1 | while read line
7 do
8 print $line
9 done
$ strDltFile.scr spaces.dat
Too many spaces in this text.
script will delete the extra spaces.
```

## 字符串长度

要在 Korn shell 中确定字符串的长度，我们使用以下代码：

```
$(string)
```

在脚本 15.7 中，我们确定字符串的长度并将其打印。这段代码可以很容易地整合到另一个脚本。

### 脚本 15.7 字符串长度

```
1 #!/bin/ksh
2 # 返回字符串的长度
3 print "Enter a string: \c"
```

（续

```
4 read strIn
5 strlen=${#strIn}
6 print The string length is: $strlen
Output:
Enter a string: Now is the time
```

## 定位子字符串

使用 `egrep` 在字符串中定位子字符串相对容易。我们在脚本 15.8 中演示了这种方法。

### 脚本 15.8 使用 egrep 查找子字符串

```
1 #!/bin/ksh
2 # Script: strstrGrep.scr
3 # 使用 grep 判断子字符串是否在字符串中
4 # $1 是字符串；$2 是子字符串
5
6 if [[ $# -ne 2 ]]; then
7 print Two parameters are required.
8 print Usage: strstrGrep.scr string substring
9 exit 1
10 fi
11
12 if print $1 | egrep "$2" > /dev/null
13 then
14 print "$2" found in "$1"
15 else
16 print "$2" not in "$1"
17 fi
```

```
$ strstrGrep.scr "Now is the time" "Now"
"Now" found in "Now is the time"
$ strstrGrep.scr "The time is now" "is"
"is" found in "The time is now"
$ strstrGrep.scr "The time is now" "it"
"it" not in "The time is now"
$ strstrGrep.scr "The time is now"
Two parameters are required.
Usage: strstrGrep.scr string substring
```

脚本 15.8 分析：记住 `egrep` 不接受字符串作为输入；它处理的是文件。因此，我们需要将字符串转换为单行文件，以便 `egrep` 能够对其处理。这是在第 13 行完成的。`print` 命令在标准输出上创建一个文件，然后将其传递给 `egrep` 命令。一旦有了输入行，`egrep` 就可以测试其是否包含子字符串。

## 15.2 节 字符串处理

尽管这是一个测试脚本，但我们包含了验证以确保存在参数。我们还打印了参数以便验证结果。我们测试了三次。第一次测试位于字符串开头的字符串；第二次测试位于字符串中间的字符串。第三次测试使用了一个不在字符串中的子字符串。为了完成验证，我们将对字符串末尾的子字符串进行测试。

最后一个讨论点是语句末尾的重定向 (`> /dev/null`)。因为我们不需要 `egrep` 命令的输出，我们简单地将其放入 UNIX 垃圾桶。

## 提取子字符串

要从一个字符串中提取另一个字符串，我们使用 match 命令 (`expr`)。其语法如图 15.6 所示。冒号后面有三个正则表达式：第一个指的是我们想要提取的子字符串之前的字符。第二个是用于匹配子字符串的正则表达式。第三个正则表达式用于子字符串之后的字符。第一个或第三个表达式（或两者）都可以为空。例如，如果我们想从字符串（行）的开始，第一个表达式将为空。同样，如果我们想包含最后一个字符，则第三个表达式将为空。

img/6e4cdc423ec4060ea72b32fff220_

图 15.6 `expr` Match 命令

在脚本 15.9 中，我们通过首先将系统日期存储在变量中，然后使用 match 命令提取小时。提取通用格式出现在第 7 行。

### 脚本 15.9 从日期提取小时和分钟

```
bin/ksh
# Script: substr.scr
# 从系统日期提取 hh:mm

str=$(date)
print The date is $str
substr=$(expr "$str" : '........\(..)\*)
print The time is "$substr"
Output:
The date is Mon Jul 10 11:08:54 PDT 2000
The time is "11:08"
```

表 15.2 显示了多次提取的脚本代码。记住每次提取都需要三个正则表达式。在某些情况下，第一个或最后一个表达式为空。研究这些模式并确保你清楚理解每一个。

### 表 15.2 子字符串提取示例

| 命令 | 解释 |
|---|---|
| `expr "string" : '\(..)\''` | 提取前三个字符。 |
| `expr "string" : '*(...)\'` | 提取最后四个字符。 |
| `expr "string" : '*...\''` | 提取第5、6、7个字符。 |
| `expr "string" : '\*.*\''` | 提取留下4个的字符。 |
| `expr "string" : '.*([a]).*[z])'` | 提取以a开始以z结束的字符串。 |

## 剥离字符串

有时我们需要删除字符串的一部分并保留其余。这个过程被称为剥离字符串。Korn shell 定义了四种字符串处理结构，用于从字符串的开头或结尾剥离字符（表 15.3）。

### 表 15.3 剥离字符串示例

| 命令 | 解释 |
|---|---|
| `${var*pattern}` | 从字符串开始，剥离匹配模式的最短部分。 |
| `${var##pattern}` | 从字符串开始，剥离匹配模式的最长（贪婪）部分。 |
| `${var%pattern}` | 从字符串结束，剥离匹配模式的最短部分。 |
| `${var%%pattern}` | 从字符串结束，剥离匹配模式的最长（贪婪）部分。 | |

## 使用其他工具

我们不仅限于使用 `expr` 命令和 `grep` 家族。在提供更好替代方案的情况下，我们也可以使用 `sed` 或 `awk`。它们的语法基本上相同。然而，无论我们使用哪种过滤器，都有几点是我们需要的：

- 1. 这些工具中的每一个都需要一个文件作为输入。如果我们想将它们应用于一个字符串，必须先使用 `print` 命令将字符串转换为单行文件。这会将字符串转换为一个可以作为输入文件的单行文件。
- 2. 这些工具中的每一个都会创建一个输出文件。如果输出必须是字符串，我们使用命令替换将输出文件转换为字符串。
- 3. 当我们需要将本地变量的值传递给命令时，我们必须使用正则表达式，而不是单引号。当一个以 `$` 符号头的变量在双引号中使用时，它的值将成为字符串的一部分；`$` 和变量名（如 `var`）被视为字符串。
