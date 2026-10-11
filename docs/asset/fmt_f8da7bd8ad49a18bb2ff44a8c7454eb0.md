
# 使用 vi 或 Emacs 编辑器创建 `.myfuncs` 文件

1. 使用 `vi` 或 `Emacs` 编辑器在你的源目录内创建 `.myfuncs` 文件。

2. 输入以下函数的代码：

```bash
sort_name()
{
    sort +1 -t: corp_phones
}

sort_date()
{
    sort +6 -t: corp_phones
}

sort_dept()
{
    sort +4 -t: corp_phones
}
```

3. 保存文件并退出编辑器。

## 将 `.myfuncs` 文件加载到内存

你的下一个任务是将 `.myfuncs` 文件加载到内存中，以便其函数可以被执行。为此，输入一个点（`.`），后跟一个空格，再后跟包含函数的文件名称。

### 加载 `.myfuncs` 文件

1. 在命令行中，输入 `. myfuncs` 并按 Enter。屏幕上不会显示任何内容，但函数已被加载到内存中。

2. 测试一些函数。输入 `sort_name` 并按 Enter。你会看到按个人姓名排序的电话记录。

3. 输入 `sort_dept` 并按 Enter。你会看到按部门编号排序的电话记录。

你可以通过 `.bash_profile` 或 `.bashrc` 文件在登录时自动加载函数。这样，它们对于任何需要它们的 shell 脚本始终可用。

### 修改你的 `.bashrc` 文件以加载 `.myfuncs` 脚本

1. 将你的 `.bashrc` 文件加载到 `vi` 或 `Emacs` 编辑器中。

2. 在文件末尾，添加以下命令：

```bash
. ~/source/.myfuncs
```

3. 保存文件并退出编辑器。

4. 注销并重新登录以加载函数。

5. 测试 `sort_name`、`sort_dept` 以及其他函数。

你的最后一项任务是按员工姓氏排序显示电话号码列表。你可以通过使用存储在 `.myfuncs` 文件中的 `sort_name` 函数来实现这一点。

## 对电话列表进行排序

要对电话列表进行排序，请对 `phlist1` 进行少量修改，以加载函数，然后调用 `sort_name`，将排序后的输出重定向到一个临时文件。该排序后的临时文件将作为 `Awk` 程序的输入，用于显示记录。修改后的代码还将使用 `CLEAR` 变量。

要对电话列表进行排序：

1. 确保你在源目录中。使用 `vi` 或 `Emacs` 编辑器将代码添加到 `phlist1` 脚本中。添加和修改的部分以粗体显示。

```bash
#!/bin/bash
#==============================================================
# Script Name: phlist1
# By:      JQD
# Date:    March 1999
# Purpose:Use awk to format a colon-separated set of fields
#        in a flat file and display to the screen
# Command line:     bash phlist  <enter>
# ==============================================================
echo "$CLEAR"
cursor 2 20; echo "Corporate Phone List"
cursor 3 20; echo "==================="
cursor 5 0;
sort_name > sorted_phones
awk -F': ' '{ printf "%-12s %-12s %s\t%s%s$10.10s $s\n",
$2, $3, $4, $1, $5, $6, $7 }' sorted_phones

cursor 23 1; echo "Review"
cursor 23 8; read prompt
```

2. 此代码假设你已经修改了 `.bashrc` 文件，以便在登录时加载 `.myfuncs` 中的函数。保存文件并退出编辑器。

3. 通过输入 `phlist1` 并按回车键来测试文件。你的屏幕将与图 7-33 相似。观察完屏幕后按回车键。

![](img/6d8286a85e2d8ad63e16f1801102da59_285_0.png)

**图 7-33：** 修改后的 plist1 脚本的输出

添加调用其他排序函数的代码将是本章末尾的一项练习。

在本章中，你学会了使用流程图和伪代码来规划算法和程序。你还学会了使用 `test` 命令创建复杂的决策表达式。你进一步掌握了使用 `grep`、`tr` 和 `sed` 命令格式化输出的技能。此外，你还学习了高级编程技术，例如在数据输入屏幕中将光标重新定位到之前的字段，以及创建 Shell 函数。

## 摘要

- 为了加快清屏速度，将 `clear` 命令序列赋值给 Shell 变量 `CLEAR`，该变量可以在你的登录脚本 `.bashrc` 中设置。由于每次执行时不需要在文件中查找序列，因此清屏速度更快。

- 算法是一组产生所需结果的指令或命令序列。遵循流程图和伪代码中表达的逻辑流程可以开发算法。

- Shell 函数可以通过隔离那些可以在该程序及其他程序中复用的代码来简化程序代码。

## 命令摘要

`test` 命令的选项和参数

| 选项 | 含义 | 示例命令 |
| :--- | :--- | :--- |
| `-eq` | 等于 | `test a -eq b` |
| `-gt` | 大于 | `test a -gt b` |
| `-lt` | 小于 | `test a -lt b` |
| `-ge` | 大于或等于 | `test a -ge b` |
| `-le` | 小于或等于 | `test a -le b` |
| `-ne` | 不等于 | `test a -ne b` |
| `-z` | 测试零长度字符串 | `test -z string` |
| `-n` | 测试非零长度字符串 | `test -n string` |
| `string1 = string2` | 测试两个字符串是否相等 | `test string1 = string2` |
| `string1 != string2` | 测试两个字符串是否不相等 | `test string1 != string2` |
| `string` | 测试非零长度字符串 | `test string` |
| `-e` | 如果文件存在则为真 | `test -e file` |
| `-r` | 如果文件存在且可读则为真 | `test -r file` |
| `-w` | 如果文件存在且可写则为真 | `test -w file` |
| `-x` | 如果文件存在且可执行则为真 | `test -x file` |
| `-d` | 如果文件存在且是目录则为真 | `test -d file` |
| `-f` | 测试文件是否存在且是常规文件 | `test -f file` |
| `-s` | 如果文件存在且大小大于零则为真 | `test -s file` |
| `-c` | 测试文件是否存在且是字符特殊文件（即面向字符的设备，如终端或打印机） | `test -c file` |
| `-b` | 测试文件是否存在且是块特殊文件（即面向块的设备，如磁盘或磁带驱动器） | `test -b file` |
| `-a` | 逻辑与 | `test expression1 -a expression2` |
| `-o` | 逻辑或 | `test expression1 -o expression2` |
| `!` | 逻辑非 | `test !expression` |

## 复习题

1. 算法是 _________ 。

    a. 替代标准 UNIX 命令名称的名称

    b. UNIX 命令的替代名称

    c. 总是输入到系统范围的初始化文件 `/etc/profile` 中

    d. 由产生所需结果的命令序列组成的推导公式

2. 可以通过函数名称后有 _______ 来识别 Shell 函数。

    a. 花括号

    b. 圆括号

    c. 方括号

    d. 引号

3. Shell 函数的命令包裹在 _______ 内。

    a. 花括号

    b. 圆括号

    c. 方括号

    d. 引号

4. Shell 函数很有用，因为 _______ 。

    a. 你可以在其他程序中重用代码

    b. 它减少了在 Shell 程序内部重复输入代码的需求

    c. 提高了你作为 Shell 程序员的 productivity

    d. 以上所有

5. 开发算法的正确顺序是什么？

    a. 流程图—算法—伪代码

    b. 流程图—伪代码—算法

    c. 算法—流程图—伪代码

    d. 没有唯一的正确顺序

6. 如何向 Shell 函数传递参数？

    a. 将它们包裹在函数名称后面的圆括号内。

    b. 使用位置变量 `$1`、`$2`、`$3` ... `$9`。

    c. 使用 `$?` Shell 变量。

    d. 使用 `$#` Shell 变量。
