

# 高级 Bash 脚本指南

示例 11–6. 使用 `let` 进行算术运算。

```bash
#!/bin/bash

echo
let a=11      # 等同于 'a=11'
let a=a+5     # 等同于 let 'a = a + 5'
              # (引号和空格使其更具可读性)
echo 11 + 5   $a

let a <<=3    # 等同于 let 'a = << 3'
echo "$a"    # (16) 左移 3 位 $a

let a /=4     # 等同于 let 'a = a / 4'
echo 128 / 4  $a

let a -=5     # 等同于 let 'a = a - 5'
echo 32 - 5   $a

let a *=10    # 等同于 let 'a = a * 10'
echo 27 * 10  $a

let a %=8      # 等同于 let 'a = a % 8'
echo 270 modulo 8 = $a (270 / 8 = 33, 余数为 $a)

echo

exit 0
```

eval

eval arg1 [arg2] ... [argN]
翻译列表中的命令（用于在脚本内部生成代码）。

# 示例 11–7. 显示 eval 的效果

```bash
#!/bin/bash

y='eval ls -1'  # 类似于 y='ls -1'
echo $y        # 但由于 'echoed' 变量未加引号，换行符被移除
echo
echo "$y"     # 变量加引号时保留了换行符

echo; echo

y=eval df       # 类似于 y=df
echo $y       # 但换行符被移除。

# 当 LF 未被保留时，它可能更容易解析输出，
# 使用诸如 "awk" 等工具。

exit 0
```

# 示例 11–8. 强制退出

```bash
#!/bin/bash
```

第 11 章 内置命令与内置命令

# 高级 Bash 脚本指南

```bash
y='eval ps ax | sed -n '/ppp/p' | awk '{ print $1 }'
# 查找 'ppp' 的进程号。

kill -9 sy      # 杀死它

# 上述行可以替换为
# kill -9 ps ax | awk /ppp/ { print $1 }
```

```bash
chmod 666 /dev/tty3
# 执行 SIGKILL 会改变串口的
# 权限。将它们恢复到之前的状态。

rm /var/lock/LCK..tty3      # 移除串口锁文件。

exit 0
```

# 示例 11–9. "rot13" 的版本

```bash
#!/bin/bash
# 使用 'eval' 的 "rot13" 版本。
# 与 "rot13.sh" 示例对比。

setvar_rot13() {
    "rot13" 乱
    local varname=$1 value=$2
    eval varname=$(echo "$value" | tr a-z n-a-m)
}

setvar_rot_13 var "foobar"      # 通过 rot13 执行 "foobar"。
echo $var                      # sbone

echo $var | tr a-z n-a-m      # 回到原始变量。

# 此示例由 Stephane Chazelais 编写。

exit 0
```

eval 命令可能具有风险性，当存在合理的替代方案时通常应避免使用。`eval $COMMANDS` 执行 COMMANDS 的内容，其中可能包含令人讨厌的操作，如 `rm -rf *`。对他人编写的未知代码运行 eval 是危险的。

set

`set` 命令更改内部脚本变量的值。此命令用于帮助确定脚本的行为。它的另一个应用是重置脚本视为命令结果的位置参数（set 命令）。然后脚本可以解析命令输出的字段。

#  示例 11–10. 将 set 用于位置参数

# 高级 Bash 脚本指南

```bash
#!/bin/bash

# 脚本 "set-test"

# 使用三个命令行参数调用此脚本，
# 例如 ./set-test one two three。

echo "set 之前的位置参数:"
echo "命令行参数 = $1"
echo "命令行参数 = $2"
echo "命令行参数 = $3"

echo "set 之后的位置参数:"
# $1, $2, $3 重新初始化为命令的结果
echo "字段 #1 = $1"
echo "字段 #2 = $2"
echo "字段 #3 = $3"

exit 0
```

参见示例 10–2。`unset` 命令删除变量，实际上是将其设置为空。注意，此命令不影响位置参数。

```bash
unset PATH
echo $PATH
```

# 示例 11–11. “取消设置”变量

```bash
#!/bin/bash
# unset.sh
variable=hello # 初始化
echo "variable = $variable"
unset variable # 取消设置。
echo "variable = $variable" # variable 为空。

exit 0
```

`export` 命令使变量在运行的脚本或 shell 的所有子进程中可用。遗憾的是，没有方法可以将变量导出回调用或唤起该脚本的父进程。`export` 命令的一个重要用途是在启动文件中，用于初始化变量并让后续进程可以访问。

# 示例 11–12. 使用 export 将变量传递给嵌入式 awk

```bash
#!/bin/bash
# getopts 的另一个版本 "gettotal" 脚本
# 传递选项和参数到 awk。
# 使用环境变量传递列号。

ARGS=2
if [ $# -ne "$ARGS" ]; then # 检查参数数量
    echo "用法: $0"
    exit 1
fi

filename=$1
column_number=$2

# 到此为止

export column_number
# 将列号导出到环境变量，以便获取。

# 开始 awk 脚本。
awk '{ total += ENV["column_number"] } END { print total }' $filename
# awk 脚本结束。

# 感谢 Stephanie。

exit 0
```

可以在同一操作中初始化并导出变量，如 `export var=xxx`。

declare, typeset

`declare` 和 `typeset` 命令指定并或限制变量的属性。

readonly

readonly 将变量设置为只读，实际上将其视为常量。尝试更改变量将报错。这是 shell 对 C 语言 const 修饰符的功能。

getopts

这个强大的工具解析命令行参数到脚本。这是 C 程序员熟悉的 getopt 函数。它允许将多个选项和关联参数传递给脚本（例如 scriptname -abc -e）。

getopts 构建两个隐式变量。$OPTIND 是选项索引，$OPTARG（OptionArgument）是附加到选项的（可选）参数。声明选项名称后的冒号标记该选项具有关联参数。

gets 通常封装在 while 循环中，一次处理一个选项和参数，递减隐式的 $OPTIND 变量以进入下一个。

1. 参数必须带有减号 (-) 或加号 (+) 前缀从命令行传递给脚本。前缀 + 让 getopt 识别命令行参数作为选项。事实上，getopts 在遇到第一个缺少这些前缀的参数时将停止选项处理。
2. gets 与标准的 while 循环略有不同，它缺少条件括号。
3. gets 取代了过时的 getopt 命令。

```bash
while getopts ":abc:fg" opt
# 初始化。
# a, b, c, d, e, f 和 g 是预期的选项（标志）。
# 选项 e 后面的冒号显示它将有一个参数。
do
  case $opt in
    a) 对变量 'a' 执行操作。
    b) 对变量 'b' 执行操作。
    e) 对 'e' 执行操作，并对 $OPTARG 执行操作
        # 它是选项 'e' 传递的关联参数。
    g) 对变量 'g' 执行操作。
  esac
done
shift $((OPTIND - 1))
# 移动参数指针到下一个。

# 这些内容看起来并不那么复杂 <grin>
```
