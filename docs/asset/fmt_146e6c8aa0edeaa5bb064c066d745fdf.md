
# 脚本 18.12 创建数组：命令替换

输入：
`one`
`two`
`three four five`
输出：
整个数组：`one two three four five`
元素数量： 5
第一个元素：`one`
最后一个元素：`five`

# 使用字符串转换创建数组

创建数组的第三方法是赋值一个单词字符串。要将字符串转换为列表，我们将其括在括号中。我们在脚本 18.13 中演示了这种方法，我们将字符串作为参数1 传递给脚本。

# 脚本 18.13 创建数组：字符串转换

```bash
#!/bin/csh

# Script: aryString.scr

# 演示通过字符串转换创建数组

# 字符串在 argv[1] 中

set array = ($argv[1])

echo "The whole array: $array"

echo "The number of elements: $array"

echo "The first element: $array[1]"

echo "The last element: $array[$array]"

%aryString.scr one two three five

Output

整个数组：one two three four five

元素数量： 5

第一个元素：one

最后一个元素：five
```

# 解析输入

解析要求我们将字符串拆分为它的组成部分，以便我们对其进行分析。我们使用数组处理来解析任何用于处理的字符串。作为一个简单的例子，让我们统计一个文件中的单词数。脚本 18.14 演示了统计《乌鸦》第一节的单词数。

# 脚本 18.14 统计文件中单词数

```bash
#!/bin/csh

# Script: aryString.scr

# 演示通过字符串创建数组
```

## 第 18 章 • C SHELL 高级编程

脚本 18.14 统计文件中单词数——续

```bash
4 # 字符串在 argv[1] 中

6 set totalWords = 0

7 set line=$

9 while [ "$line" != ""]

10 set words =($line)

11 @totalWords += $words

12 set line=$

13 end
```

`echo Total Words: $totalWords`
`% aryParse.scr <TheRavenV1`
Output:
Total Words: 56

脚本 18.14 分析：正如我们在脚本 18.2 中看到的，这个脚本存在潜在问题。只要输入中没有空行，它就能工作。如果有空行，`while` 表达式将变为假，循环将停止。

## 18.9 脚本示例

在本节中，我们将演示一些完整的脚本应用。选择这些应用是为了演示本章介绍的不同技术。我们使用了与上一节讨论的相同的文档格式。

# 模拟 find 命令

我们一直在寻找某些东西。这个脚本通过添加解释命令失败原因的错误信息来增强 `find` 命令。你可能会发现参考第 108 页的“Find (find) File Command”有助于刷新对 `find` 命令的记忆。

我们的 `find.scr` 脚本需要一个或两个参数。如果只输入一个参数，它是要查找的文件，从我们的家目录开始。如果输入两个参数，第一个是起始目录，第二个是文件。解决方案在脚本 18.15 中。

# 脚本 18.15 查找文件

```bash
1 #/bin/bash -f
2 # NAME: find.scr
3 # TASK: 查找文件的路径
4 # AUTHOR:
5 # DATE WRITTEN:
6 # SYNOPSIS: find.scr searchpath file or find.scr file
7 # DESCRIPTION: 它查找文件的路径
```

## 章节 18.9 • 脚本示例 • 75

# 脚本 18.15 查找文件

```bash
8 #               argv[1] 是文件名
9 #               或 argv[1] 是路径 argv[2] 是文件名
10 # 退出值
11 #             成功为 0
12 #             参数数量错误为 1
13 #             路径不是目录为 2
14 #             未找到文件为 3
15 #
16 set noglob
17 if ( $argv < 1 || $argv > 2 ) then
18     echo "$0 needs or two arguments"
19     exit 1
20 endif
21
22 if ( $argv == 2 ) then
23     set srchPath = $argv[1]
24     shift
25     if ( ! -d $srchPath ) then
26         echo "$srchPath is not a directory"
27     endif
28 endif
29 else
30     set srchPath = $HOME
31 endif
32
33 if ( ! -d $srchPath ) then
34     echo "$srchPath is not a directory"
35     exit 2
36 endif
37 set temp = ./temp
38
39 find $srchPath -name argv[1] -print | tee $temp
40
41 if ( -z $temp ) then      # 测试输出是否为空
42     echo "cannot find $argv[1]"
43     exit 3
44 endif
45
46 rm $temp                  # 删除临时文件
47 exit 0
```

执行：
`% find.scr`
`% find.scr needs or two arguments`
`% find.scr x`
x is not a directory
`% find.scr file`
`/mnt/diska/staff/gilberg/unix/`
`/mnt/diska/staff/gilberg/unix/`

## 第 18 章 C SHELL 高级编程

脚本 18.15 查找文件——续

```
/mnt/diska/staff/gilberg/unix/
/mnt/diska/staff/gilberg/unix/files.bak/
/mnt/diska/staff/gilberg/unix/
% find.scr file
```

脚本 18.15 分析：该脚本相对简单。困难的部分是判断 `find` 命令是否成功。我们的解决方案是将输出通过 `tee` （见第 9 行）。如果文件为空，则没有输出。在执行 `find` 命令后。

# 总账系统

一个大型系统（如账本系统）需要许多脚本。大型系统由菜单系统驱动，直到一天结束时关闭。在这个应用中，我们演示了创建此类系统的基本概念。它不是一个完整的系统，而是一个带有主要组件存根（stubs）的骨架。系统的基本设计如图 18.1 所示。

![](img/6dc423ec0.png)

# 会计系统设计

当你学习会计脚本时，请注意它在概念上是简单的。我们使用 `cat` 显示菜单，然后使用 `switch` 命令执行请求的应用程序。每个应用都使用相同的设计来运行自身。被调用的脚本位于脚本 18.7（菜单）、脚本 18.8（会计）、脚本 18.9（总账）和脚本 18.10（工资）。

# 脚本 18.16 系统设计：主脚本

```bash
#!/bin/csh

# NAME: acctMain.scr
# TASK: 运行不同的会计程序
# AUTHOR:
# DATE WRITTEN:
```

存根是一个代表尚未开发的应用的空脚本。在这个应用中，存根简单地输出它们已执行的消息。

# 脚本 18.16 系统设计：主脚本

```bash
7 # SYNOPSIS: acctMain.scr
8 # DESCRIPTION: 使用菜单
10 # 退出值
11 # 成功为 0
12
13 clear
14 set menu = ./acctMenu.scr
15 set acc = ./
16
17 while (1)
18 cat $menu
19 echo -n "Choose an option: "
20 set ans = $ans
21 switch ($ans)
22
23 case [aA]:
24 $(acc)/acctAcct.scr
25 break
26
27 case [gG]:
28 $(acc)/acctGL.scr
29 break
30
31 case [pP]:
32 $(acc)/acctPay.scr
33 break
34
35 case [qQ]:
```
