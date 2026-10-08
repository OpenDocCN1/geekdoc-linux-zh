

# 高级 Bash 脚本指南

```bash
# 练习：
# -----
# 修改此脚本以每 20 分钟跟踪一次 /var/log/messages 的变化。
# 提示：使用 "watch" 命令。
```

与 `find` 命令一样，大括号 `{}` 作为替换文本的占位符。

# 示例 16-6. 将当前目录下的文件复制到另一个目录

```bash
#!/bin/bash
# copydir.sh

# 复制（详细）当前目录 ($PWD) 下所有文件
# 到命令行指定的目录。
E_NOARGS=85

if [ -z "$1" ];      # 如果未提供参数则退出。
then
    echo "Usage: basename $0 directory-to-copy"
    exit $E_NOARGS
fi

ls | xargs -i {} t cp ./$1
# -t 是 "verbose"（将命令行输出到 stderr）选项。
# -i 是“替换"字符串。
# {} 是输出文本的占位符。
# 这类似于在 "find" 中使用大括号对。

# 列出当前目录下的文件 (ls .)，
# 将 "ls" 的输出作为参数传递给 "xargs" (-i -t 选项)，
# 然后将这些参数 ({}) 复制 (cp) 到新目录 ($1)。

# 结果与 cp $1 完全等效，
# 除非文件名中嵌入了“空格”字符。

exit 0
```

# 示例 16-7. 按名称杀死进程

```bash
#!/bin/bash
# kill-byname.sh: 按名称杀死进程。
# 将此脚本与 kill-process.sh 进行比较。

# 例如，
# 尝试 "./kill-byname.sh xterm" -- 桌面上所有的 xterms 消失。

# 警告：
# -----
# 这是一个相当危险的脚本。
# 粗心运行（特别是作为 root）
# 可能会导致数据丢失和其他不良影响

E_BADARGSGS=66

if test -z "$1" # 未提供命令行参数？
then
    echo "Usage: basename $0 Process(es)_to_kill"
    exit $E_BADARGSGS
fi
```

```bash
PROCESS_NAME="$1"
ps ax | grep "$PROCESS_NAME" | awk '{print $1}' | xargs -i kill {} 2>/dev/null
```

```bash
#
# 注意：
# - 是 xargs 的“替换字符串”选项。
# - 大括号是替换的占位符。
# - 2>/dev/null 抑制不需要的错误消息。
# # grep "$PROCESS_NAME" 可以被 pidof "$PROCESS_NAME" 替换吗？

exit $?
```

```bash
# "killall" 命令与此脚本的效果相同，
# 但使用它并不很具有教育意义。
```

# 示例 16-8. 使用 xargs 进行词频分析

```bash
#!/bin/bash
# wf2.sh 对文本文件进行粗略词频分析。

# 使用 'xargs' 将文本行分解为单个单词。
# 将此示例与稍后的 "wf.sh" 脚本进行比较。

# 检查命令行上的输入文件。
ARGS=85
E_BADARGSGS=86
_NOFILE=86

if [ $# -ne "$ARGS" ];
# 传递给脚本的参数数量正确吗？
then
    echo "Usage: basename $0 filename"
    exit $E_BADARGSGS
fi

if [ ! -f "$1" ] # 文件是否存在？
then
    echo "File \$1 does not exist."
    exit $E_NOFILE
fi

################################################################
cat "$1" | xargs -n1 |
# 列出文件，每行一个单词。
```

第16章 外部过滤器、程序和命令

# 高级 Bash 脚本指南

```bash
tr A-Z a-z 
# 将字符转换为小写。
sed -e 's/\.//g' -e 's/,//g'
# 过滤掉点和逗号，
# 将单词之间的空格改为换行符
sort | uniq -c | sort -nr
# 最后删除重复项，前缀出现次数
# 并按数字排序###########################################################
```

# 这样做的作用与 "wf.sh" 示例相同，
# 但稍微笨重一些，而且运行速度更慢（为什么呢？）。

exit $?

高级用途表达式评估器：根据操作连接并评估参数（参数之间必须用空格分隔）。操作可以是算术、字符串或逻辑的。

```bash
expr 3 + 5
返回 8
```

```bash
expr 5 % 3
返回 2
```

```bash
expr 1 / 0
返回错误消息，expr: division by zero
```

不允许执行非法算术运算。

```bash
expr 5 \* 3
返回 15
```

在 expr 的算术表达式中使用时，乘法运算符必须进行转义。

增加一个值，其效果与 let y=y+1 和 y=$($y+1) 相同。这是一个算术扩展的示例。

```bash
z=$(expr substr $string $position $length)
从 Position 开始提取长度为 characters 的子字符串。
```

# 示例 16-9. 使用 expr

```bash
#!/bin/bash
# 展示 'expr' 的一些用法
# ==============================================
echo
# 算术运算符
# ---------------------
echo "Arithmetic Operators"
echo
a=$(expr 5 + 3)
```

# 16. 外部过滤器、程序和命令

```bash
a=$(expr $a + 1)
echo
echo "a + 1 = $a"
echo "(增加一个变量)"

a=$(expr 5 % 3)
# 取模
echo
echo "$5 mod 3 = $a"

echo
echo

# 逻辑运算符
----------------
```

```bash
# 如果为真返回 1，如果为假返回 0，
# 与 Bash 惯例相反

echo "Logical Operators"
echo
```

```bash
x=24
y=25
b=$(expr $x = $y)      # 测试相等
echo "b = $b"      # 0 ( $x -ne $y )

a=3
b=$(expr $a = 3)      # 1 ( $a = 3 )
```

