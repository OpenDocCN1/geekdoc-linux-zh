
注意：
# 如果你通过键盘 (STDIN) 获取数据，
# 那么头部空格 (SPACE) 会自动
# 删除（只要你使用默认的 IFS）。
### 注意：`remove_blank_lines.ksh`
### 注意：`read_input_from_keyboard.ksh`
### 注意：`IFS.ksh`

# 关于 SED：
# `'sed'` 是一个流编辑器；它是一个标准的 UNIX 工具。
# `'s/'` 意味着“替换”
# `'s/...'` 以“搜索”开始：`metacharacters.ksh`
# `'\s'` 意味着“空白”，例如，或 TAB
# `'\+'` 意味着“前一个字符出现一次或多次”。
# 在 `sed` 中，`'\$'` 前面必须有一个反斜杠 (`\`)。
# `'s/$'` 在 `sed` 中意味着“行尾”
### 注意结束。

# 关于 IFS，内部字段分隔符：
# 关于 `IFS` 的细节在 `script.ksh` 中。
# `IFS` 的默认设置为 (TAB 和换行符)。
# 使用默认的 `IFS` 时，空白会被删除。
### 注意结束。

# 初始化：
`IFS=' '` 我们正在将内部字段分隔符设为空。

`clear` 清除屏幕。
`print "$0"` 是脚本。
`print "目的："`
`print "1. 删除行首的制表符和空格。"`
`print "2. 删除行尾的制表符和空格。"`
`print "输入："`
`print "下划线 (_) 用于显示数据的开始和结束："`
`print "示例 1 显示了如何通过结合 'echo'、管道 (|) 和 'sed' 从字符串或记录中删除首尾空白："`

# 注意：在某些系统上，你可能需要使用 `'echo -e'` 而不是 `'echo'`。
```bash
string=$(echo "\tcount Ivanovich \tcount")
```
# 删除字符串中的头部空格：
```bash
temp=$(echo "$string" | sed -e 's^[[:space:]]*//')
```
# 删除字符串中的尾部空白：
```bash
after=$(echo "$temp" | sed -e 's/[[:space:]+$//')
```
`print "之前：${temp}"`
`print "之后：${after}"`

`print "示例 2 显示了如何从文件中读取的记录中删除首尾空白："`

# 首先，我们将创建一个小文件（包含 2 条记录）作为我们的输入：
# `'$($)'` 是我们脚本的 PID/进程 ID：
```bash
print "\tcount Ivanovich \tcount" > /tmp$.input
print "\tcount Ileanaovich\tcount" >> /tmp$.input
```

```bash
while read -r record
do
# 删除记录中的头部空白和尾部空白：
echo "$record" | sed -e 's^[[:space:]]*//' -e 's/[[:space:]+$//' >> /tmp$.output
done < /tmp$.input
```

`print "之前："`

```bash
while read -r record
do
print "_${record}"
done < /tmp$.input
```

```
之后：
while -r record
print "_${record}"
done < /tmp$.output
```

# 删除测试文件：
`rm /tmp$.input`
`rm /tmp$.output`

`print "\n完成。脚本：$0\n"`

输出：`remove_leading_and_trailing.ksh`
脚本是如何执行的：`./remove_leading_and_trailing.ksh`
输出如下：

此脚本 `./remove_leading_and_trailing.ksh`。
目的：

+   1. 删除行首的制表符和空格。
2. 删除行尾的制表符和空格。

注意：
下划线 (_) 用于显示数据的开始和结束：

示例 1 显示了如何通过结合 `'echo'`、管道 (`|`) 和 `'sed'` 从字符串或记录中删除首尾空白：

之前：Count Ivan Ivanovich III
之后：Count Ivan Ivanovich III_

示例 2 显示了如何从文件中读取的记录中删除首尾空白：

之前：Count Ivan Ivanovich III
Countess Ileana Ivanovich

之后：Count Ivan Ivanovich III
Countess Ileana Ivanovich

# 441

# (我们假设今天是 4 月 15 日):

```bash
mv larrys_$current_date
```

```bash
print "\n这里是我们重命名的文件:\nls -l larry_$current_date
```

```bash
# 现在我们将创建一个名为 /home/larry/SMITH 的目录
mdir -m755 /home/larry/SMITH # 权限将为 755。
```

```bash
print "\n这是我们创建的目录:\nls -ld /home/larry/SMITH
```

```bash
# 然后我们将将其移动/重命名为 /home/larry/JONES
mv /home/larry/SMITH /home/larry/JONES
```

```bash
print "\n我们将 /home/larry/SMITH 重命名为 /home/larry/JONES:\nls -ld /home/larry/JONES
```

```bash
\n完成。脚本: $0\n"
```

OUTPUT: `rename.ksh.OUTPUT`
脚本的执行方式: `./rename.ksh`
输出如下:

注释: 这是脚本 `./rename.ksh`。
目的: 展示如何重命名（移动）文件或目录。

当前日期: 3 月 28 日

这是我们重命名的文件：
-rw-r--r-- 1 larry larry 1382 Mar 28 16:41 larry Mar28

这是我们创建的目录：
drwxr-xr-x 2 larry larry 4096 Mar 28 16:41 /home/larry/SMITH

我们将 /home/larry/SMITH 重命名为 /home/larry/JONES:
drwxr-xr-x 2 larry larry 4096 Mar 28 16:41 /home/larry/JONES

完成。./rename.ksh

程序: `return_variable_from_subroutine.ksh`

```bash
#!/bin/ksh
```

# 程序: `return_variable_from_subroutine.ksh`

# 目的: 展示如何从子程序（函数）返回变量。

# 编写者: Larry Smith。由 __date__ 修订

# 难度: 中等

# 用法: 示例: `./return_variable_from_subroutine.ksh`

###

```bash
# ksh 和 bash 中的 "return" 语句不如 perl
# 中的那样的灵活；例如，我们在 perl 中可以做到：
# "return(yesterday_month,$(yesterday_day_day)"（换句话说，
# 我们可以返回两个值，直到它们被
# 调用的地方）。
```

```bash
# 在 ksh 和 bash 中，return 语句只能返回一个值
# 该值必须是整数。
return 语句在 ksh 和 bash 中使用时，用于
# 退出子程序（但不退出脚本）
# 或者返回状态码（0=成功；1 或更高=有问题）。
# 然而，如示例 1 所示，你可以在不使用 'return' 命令
# 的情况下从函数/子程序中接收数据。
###
```

```bash
# 要找到此脚本的主逻辑，请在 'MAIN_LOGIC' 中查找。
### 结束笔记。
```

第 442 页

```bash
clear # 清空用户屏幕。
print "注释: 这是脚本 $0。"
print "目的: 展示如何从子程序（函数）返回数据"
```
