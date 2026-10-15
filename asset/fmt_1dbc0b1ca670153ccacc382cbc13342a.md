
错误方法: `grep '-s' $TESTFILE`

错误方法: `grep -s'TESTFILE`

```
警告: 这两种方法都会导致终端挂起。
你需要同时按下 CTRL+C。
```

正确方法 1: `grep '-s' $TESTFILE`

正确方法 2: `fgrep '-s' $TESTFILE`

正确方法 3: `fgrep -h '-s'`

`--` 意味着命令中此点之后没有更多选项。
`-h` 意味着不显示找到字符串的文件名。
结果:
`-s` 是 `ksh`, `bash` 和 `perl` 中一个实用的选项

# 示例 3a

让我们来看看扩展 `grep`，`egrep`。"`grep -E' 也是一种扩展 `grep`。
该代码将显示文件中所有以 'How' 或 'Look' 或 '16' 开头的行
`grep '(How|Look/16)'` 意味着“或”。
在括号内部，'|' 意味着“或”。

你好？
查找 `02`, `0F`, `06`, `12`, `1F` 在前两个字节中
`16` 是很难的！

# 示例 3b

以下代码将显示文件中所有不是以 'How' 或 'Look' 或 '16' 开头的行
有效: `-v egrep '(How|Look/16)' $TESTFILE`
同样有效: `grep -v '(How|Look/16)' $TESTFILE`

```
结果:

01 这是文件的第一行。

1F 你好！

1F 行的第一个字节是空格

- 是 ksh, hash 和 perl 中一个实用的选项

最后一行。
```

# 示例 4

有时你想找到包含元字符/通配符的行。

如果你认为在使用 UNIX-LINUX `grep` 时，在元字符周围加上单引号会起，你是错的。

当你想要查找元字符时，请使用 `egrep`！

错误: `grep '(How|Look/16)' $TESTFILE`

开始 `egrep '(How|Look/16)' $TESTFILE`

```
结果:
grep 无法在行中间找到这个：(How|Look/16)
```

# 示例 5

这个示例展示了如何在字符串内部查找数据

（而不是在已读取的文件中查找数据）。

这也展示了如何使用 'i' 来忽略大小写。

（细节在脚本内部提供）。

你的字符串：larry, moe 和 CURLY JOE 是三个小子。

匹配: 你的字符串包含 'Larry'、'Moe' 或 'Carly Joe'。

```
完成。脚本: ./grep_egrep grep_fpkg.sh
```

# 程序: grep_for_control_characters.sh

```bash
#!/bin/bash
# 程序 grep_for_control_characters.sh
# 目的: 确定文件中哪些字符包含特定字符。
# 程序员: Larry Smith. 由 __ 于 ____ 修改
# 难度: 中等
# 使用: 示例: ./grep_for_control_characters.sh
# 注意:
# 为了查看所有字符及其八进制等值的列表，从命令行执行以下命令：
# main
# 你将在屏幕上看到类似这样的信息：
```

| 八进制 十进制 十六进制 字符 | | |

|---|---|---|---|

| 011 9 09 HT | '\t' | # HT = 水平制表符 |

| 012 10 AF | '\n' | # LF = 换行符 ("换行") |

```
# 040 32 20 SPACE
# 空格是八进制 \040
# 制表符是八进制 \011
# 换行是八进制 \012
# (n) 意味着“水平”
# 在打印语句中，使用 \t 表示
# 换行会自动发生。）





# $testFile / 删除/移除测试文件。

print "\DOONE. Script: $0\n"
exit
# 如果你好奇，可以尝试这个：
BELL=$(echo "\007")
TAB=$(echo "\011")
string="HI, STAB Larry! $BELL"

print "\nod -b" 显示每个字符的 ASCII 翻译结果："
print "$string | od -b"

print "\nod -b c" 输出**容易读得多**；它以人类可读的形式显示不可打印
字符；"
print "\t 以及 '警铃声' 是 \a:"
# 例如，一个 TAB 可能是 \a
# \t 是一个 TAB，而 '警铃声' 是 \a
print "$string | od -c"

# 注意：
八进制 十进制进制 字符：

| 八进制 | 十进制 | 字符 |
| :--- | :--- | :--- |
| 007 | 7 | BEL '\a' |
| 011 | 9 | HT '\t' |

OUTPUT: grep_for_control_characters.ksh.OUTPUT
脚本是如何执行的：./grep_for_control_characters.ksh
输出如下：

注释：这是脚本 ./grep_for_control_characters.ksh。
目的：确定文件中的哪些行包含特定的控制字符。

有几种方法可以在文件中找到不可打印的控制字符：

- 1. 'cat -A myfile'
  'cat -A' 显示如 TAB 和行尾（END OF LINE）之类的不可打印字符。
  注意：TAB 显示为 I，行尾显示为美元符号 $。

- 2. cat filename od -c
为了熟悉 `od` 命令的输出，
尝试一些简单的操作：
echo HI | od -c

LINUX 的 'od' 命令打印每个字节的八进制表示。
另请：'man ascii' 和 'man od'
更多信息请：'man od'
注意：你可以通过 grep 一个包含其八进制值的变量来查找 任何控制字符。例如，一个 TAB 的八进制是 011：
TAB=$(echo "011")

- 3. grep -c "$TAB" TestFile # 计算包含 TAB 的行数。
- 4. grep "$TAB" TestFile # 显示包含 TAB 的行。

这里是我们使用的 3 行测试文件：
这一行包含一个 TAB。
这一行包含两个 TAB。
这一行**不包含**一个 TAB。

TestFile 中的总行数：3
包含 1 个或多个 tab 的行数：2

以下记录包含 1 个或多个 tab：
这一行以 TAB 开头。
这一行包含两个 TAB。

完成。脚本：./grep_for_control_characters.ksh

# 程序：grep 查找 files_with_todays_date.ksh

```
#!/bin/ksh

# 程序：grep_for_files_with_todays_date.ksh

# 目的：列出今天创建或修改的文件名。

# 程序员：Larry Smith，修订于 __date__。

# 难度：易/中

# 用法：./grep_for_files_with_todays_date.ksh

# 注意：“方法 1”将查看当前目录下的子目录。

# -mtime -1 查看在过去 24 小时内修改过的所有文件。

# -atime -1 查看在过去 24 小时内访问（“读取”）过的所有文件。

# 另请：find.ksh

# 注意结束。

clear # 清除用户屏幕。

print "Content: 这是脚本 $0。"

print "PURPOSE: 列出今天创建或修改的文件名。"

print "METHOD 1:"

print "你当前目录的文件在过去 24 小时内修改过："

print "CURRENT: $PWD"

find . -type f -mtime -1 -exec ls -l {} \; -print "" 是当前目录。

# 关于当前命令的详情，请参脚本 "grep.ksh"。

print "METHOD 2:"

MMMM_DD=$(date +%Xd | sed 's/ /\2//g' 2>/dev/null)

# 见下文，关于 'sed' 命令的说明。

print "你当前目录的文件在 ${MMMM_DD} 修改过："

print "CURRENT: $PWD\n"

ls -l | grep "$MMMM_DD"

print "DONE: $0"
```
