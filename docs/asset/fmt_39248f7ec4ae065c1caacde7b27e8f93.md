
```
syslog 1: netcheck 2
Name Mtu Network Address Ipkts Ierrs Opkts Oerrs Coll
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
lan0* 1500 none none 0 0 0 0 0
count has reached 9, run netcheck again to see lan0 status
```

（注：由于原文包含大量重复和乱码片段，已根据指令要求清理并翻译核心内容。）

# C Shell 编程

信息非常多，所以我从 `-v` 开始，如果反馈过多，我就将其消除。

接下来的示例是对早期的搜索程序进行的扩展，包含一个检查是否提供了三个参数的检查逻辑。在检查 `$#argv` 是否等于 3 时，我漏掉了左括号。这里是程序的列出以及显示错误的语法检查：

```
sys 1 1: cat search
!/usr/bin/csh
# search
# 用法: search  模式 文件
```

```
if ($#argv) != 3 then      # 如果提供的参数小于 3 个
    echo "Usage: search directory pattern files"
    # 则打印用法说明
else
    echo " "                  # 否则打印空行并
    cd $1                   # 切换搜索目录
    grep -n "$2" $3          # 在 $3 中搜索 $2
    echo " "                  # 打印行
endif
```

```
sys 1 2: csh -nv search
    if ($#argv) != 3 then
        Too many ('s
```

`csh -nv` 执行了带有详细输出的语法检查。首先，会打印相关的行，然后是一条告诉你是该行哪里错误的错误消息。在这种情况下，显然是我漏掉了左括号。

# 第 7 章 系统管理员的 Shell 编程

修复问题后，我可以使用 `-x` 运行程序，这会导致所有命令在执行之前立即回显。下面的示例显示了搜索程序的运行情况：

```
sysl 1: csh -xv ./search cwd grep hostck

if ($#argv != 3 ) then
if ( 3 != 3 ) then

echo ""
echo

cd $1
cd cwd
~/cshscripts
grep -n "$2" $3
grep -n grep hostck
22:/etc/ping $sys 64 1 | grep "1 packets received" > /dev/null
echo ""
echo

if
endif
```

你可以逐行跟踪正在发生的情况。以 `22` 开头的行是 `hostck` 文件中包含 `grep` 的那一行，也就是说，如果运行程序时不带 `-xv` 选项，你将收到的输出。

我建议只有在运行程序时得到意想不到的结果时，才對新的 Shell 程序执行语法检查 (`-n`) 并使用 `-x` 回显所有命令。当你编写的 Shell 程序遇到问题时，调试选项无疑会在某时刻帮到你。

## 需要多长时间？

你可以使用 `time` 命令查看你的 Shell 程序运行所需的时间报告。当你发出 `time` 命令时，你将得到如图 7-17 所示格式的报告。

```
sys1: time netcheck
1.3u 0.8s 0:03 70% % of CPU to real time used
--> 执行命令的实际时间
--> 使用的系统时间
--> 使用的用户时间
```

图 7-17 `time` 命令 示例

由于你编写的脚本可能会消耗大量的系统资源，你可能想要考虑研究 C shell 的某些作业控制功能。你可以使用的最简单的作业控制是在后台运行脚本，这样脚本的优先级就很低。通过输入脚本名称并在后跟 `&`，你将在后台运行脚本。如果你在后台运行多个脚本，可以通过执行 `jobs` 命令获取这些作业的状态。这是一个更高级的 C shell 主题，但取决于你编写的脚本的复杂程度，你可能想要研究作业控制。

## 第 7 章中使用命令的手页

本节包含在本章创建 Shell 程序时所用命令的手页副本。这使得在你扩展这些程序并创建你自己的 Shell 程序时，可以作为一个快速参考。

### awk

# awk

# awk - 扫描输入文件查找模式。

```
awk(1)
```

```
awk(1)
```

```
NAME
```

```
awk - 模式引导的扫描和处理语言
```

```
SYNOPSIS
```

```
awk [-F fs] [-v var=value] [program -f profile ...] [file ...]
```

```
DESCRIPTION
```

`awk` 扫描每个输入文件，匹配在程序中字面指定的或在作为 `-f profile` 指定的一个或多个文件中指定的任意模式的行。对于每个模式，可以有一个关联的操作，当文件中的某行匹配模式时就会执行该操作。每一行都会与每个模式-动作语句的模式部分进行匹配，并对每个匹配的模式执行关联的操作。任何 `var=value` 形式的文件都被视为赋值，而不是文件名。除非使用了 `-v` 选项，否则赋值在作为文件名打开时就会求值。

一个输入行由空白字符或正则表达式 `FS` 分隔的字段组成。字段标记为 `$1, $2, ...`；`$0` 指整行。

#### 选项

`awk` 识别以下选项和参数：

- `-F fs` 指定用于分隔字符的正则表达式。默认识别空格和制表符。如果使用了 `-F` 选项，开头的字段分隔符将不再被丢弃。
- `-f profile` 指定 `awk` 程序文件。可以指定最多 100 个程序文件。这些文件中的模式-动作语句按照文件指定的顺序执行。
- `-v var=value` 在执行 `BEGIN` 动作（如果存在）之前引发 `var=value` 赋值。

### 语句

模式-动作语句的形式为：

```
pattern { action }
```

缺失 `{ action }` 意味着该行；模式总是匹配。模式-动作语句由换行或分号分隔。

一个 `action` 是语句的序列。

```
if(expression) statement [else statement]
while(expression) statement
for(expression;expression;expression) statement
for(var in) statement
do while (expression)
break
continue
{statement ..} # 通常 var=expression
print([expression-list] > [expression])
printf format, [expression-list] > [expression]
return (expression)
```

- `next` # 跳过此行的剩余模式。
- `delete array [expression]` # 删除数组元素。
- `exit [expression]` # 立即退出；状态是

语句由分号、换行或右括号结束。一个 `expression list` 代表空白。字符串常量包含通常的字符。表达式使用 `+, *, /` 和连接。`SUBEXP`。变量可以是标量、数组元素（标记为 `x[i]`）或字段。数组可以包含任何字符串，不一定是数值（这允许关联内存）。允许多个下标如 `[i,j,k]`。部分由 `OFS` 连接。

`print` 语句将其参数打印到标准输出（如果存在 `>>file` 或存在 `| cmd`），由输出字段分隔符分隔，并输出记录分隔符终止。文件和 `cmd` 可以字面量或语句中的名称表示相同的打开文件。`print` 根据格式格式化其表达式列表（`printf`...

### 内置函数

内置函数 `close(expr)` 关闭由 `print` 或 `printf` 语句打开的文件或管道，返回对相同字符串值 `expr` 的调用。该函数在成功时返回零，否则返回。

常用的函数 `exp, log, sqrt, sin, cos, atan2` 是内置的。其他内置函数有：

```
length([{s}])	其关联参数的长度（字节）
作为字符串处理，如果没有参数则为 $0。
```

```
length([{s}])	其关联参数的长度（字符）
作为字符串处理，如果没有参数则为 $0。
```

```
rand()	返回一个 0 到 1 之间的随机数。
```
