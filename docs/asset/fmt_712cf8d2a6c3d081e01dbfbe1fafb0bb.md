
空白字符由空格或制表符组成。在某些上下文中，空格是不允许的。空行没有影响。

内部字段分隔符（`IFS`）：`IFS` 是分隔字段的特殊变量。在某些命令中，它是允许的，有默认值。

## 第 5 章 变量介绍

变量是编程的核心。它们出现在脚本的各个部分，出现在算术运算和字符串解析中，是不可或缺的。变量的赋值、导出、取消设置、引用和操作。

变量的赋值。赋值出现在脚本的各个位置。语法错误。变量可以出现在双引号、单引号或不加引号的范围内。引用变量值。使用大括号 `${}` 引用变量。

# 高级 Bash 脚本指南

```bash
# 在 'read' 语句中（也是一种赋值类型）
echo -n "Enter \a\"
read a
echo "The value of \a\" is now $a"
echo
exit 0
```

### 示例 5–3. 变量赋值，普通与花哨

```bash
#!/bin/bash

a=23            # 简单情况
echo $a
b=$a
echo $b

# 现在，来点花哨的（命令替换）。

a=$(echo Hello!)   # 将 'echo' 命令的结果赋值给 'a'
echo $a
# 注意，在命令行中使用感叹号 (!) 
# 在命令行中将无法不起作用，
# 因为这会触发 Bash 的“历史机制”。
a=is -1         # 将 '-1' 命令赋值给 'a'
echo $a        # 然而，如果不加引号，会移除制表符和换行符。
echo
echo "$a"    # 带引号的变量会保留空格。
# （请参见“引用”章节。）

exit 0
```

使用 `$(..)` 机制进行变量赋值（比反引号更新的方法）

```bash
# 来自自 /etc/rc.d/rc.local
R=$(cat /etc/redhat-release)
arch=$(uname -m)
```

## 5.3. Bash 变量是无类型的

与其他编程语言不同，Bash 不按“类型”区分其变量。本质上，Bash 变量是字符字符串，但根据上下文，Bash 允许对变量进行整数操作和比较。决定因素是变量的值是否只包含数字。

### 示例 5–4. 整数还是字符串？

```bash
#!/bin/bash
# int-or-string.sh
# 整数还是字符串？

a=2334            # 整数。
let "a += 1"

echo "a = $a " 
echo
# 仍然是整数。
b=$(a/23)
# 转换为字符串。
echo "b = $b"
declare -i b
# 声明为整数没有帮助。
echo "b = $b"
# 仍然如此。

let b="+ 1"
echo "b = $b"
# 1
echo

c=2334
echo "c = $c"
d=$((c/23))
# 转换为整数。
echo "d = $d"
# 101
let d+=" 1"
# 101 + 1 =
echo "d = $d"
# 102

exit 0
```

无类型变量既是福也是诅咒。它们在脚本编写中提供了更大的灵活性（给你足够的绳子让你勒死自己），并且更容易写出代码行。然而，它们允许错误渗入，并鼓励了草率的编程习惯。

跟踪脚本变量的类型是程序员的负担。Bash 不会为你做这件事。

## 5.4. 特殊变量类型

### 局部变量 (local variables)
- 仅在代码块或函数内部可见的变量（参见函数中的局部变量）

### 环境变量 (environmental variables)
- 影响 `shell` 行为和用户界面的变量

![](img/1ce1edffaa36e4f698a85430e71c6d3b_33_0.png)

在更通用的背景下，每个进程都有一个“环境”，即一组包含进程可能引用的信息的变量。从这个意义上说，`shell` 的行为与其他进程一样。

每次 `shell` 启动，都会创建一个与其环境变量对应的变量。更新或添加新的 `shell` 变量会导致 `shell` 更新其环境，所有的 `shell` 进程（它执行的命令）都会继承这个环境。

分配给环境的空间是有限的。创建过多的环境变量或占用过多空间的变量会导致问题。

```bash
bash eval `seq 10000 | sed -e 's/.*/export var=ZZZZZZZZZZZZZZZ'`

bash du

bash: /usr/bin/du: Argument list too long
```

（感谢 S. C. 的说明，以及提供上面的示例。）

如果脚本设置了环境变量，它们需要被“导出”（`export`），这会报告给脚本本地的环境。这就是 `export` 命令的功能。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_34_0.png)

脚本只能将变量导出到子进程，即只导出到该脚本启动的命令或进程。从命令行调用的脚本无法将变量导出回命令行环境。子进程无法将变量导出回产生它们的父进程。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_34_1.png)

### 位置参数 (positional parameters)
- 从命令行传递给脚本的参数 – `$0`, `$1`, `$2`, `$3`... `$0` 是脚本本身的名字，`$1` 是第一个参数，`$2` 是第二个，`$3` 是第三个，依此类推。在 `$9` 之后，参数必须括在括号中。

### 示例 5–5. 位置参数

```bash
#!/bin/bash

# 调用此脚本时至少传入 10 个参数

./scriptname 1 2 3 4 5 6 7 8 9 10

echo "The name of this script is $(basename $0)"

if [ -z "$1" ]; then
    echo "The first argument is missing"
fi

if [ -z "$2" ]; then
    echo "The second argument is missing"
fi

if [ -z "$3" ]; then
    echo "The third argument is missing"
fi

if [ -z "$4" ]; then
    echo "The fourth argument is missing"
fi

if [ -z "$5" ]; then
    echo "The fifth argument is missing"
fi

if [ -z "$6" ]; then
    echo "The sixth argument is missing"
fi

if [ -z "$7" ]; then
    echo "The seventh argument is missing"
fi

if [ -z "$8" ]; then
    echo "The eighth argument is missing"
fi

if [ -z "$9" ]; then
    echo "The ninth argument is missing"
fi

if [ -z "${10}" ]; then
    echo "The tenth argument is missing"
fi
```

无类型变量是福也是诅咒。它们在脚本编写中提供了更大的灵活性（给你足够的绳子让你勒死自己），并且更容易写出代码行。然而，它们允许错误渗入，并鼓励了草率的编程习惯。

跟踪脚本变量的类型是程序员的负担。Bash 不会为你做这件事。

## 第 6 章 引用 (Quoting)

引用意味着对字符串加引号。这可以防止 `shell` 对特殊字符进行重新解释或扩展。

### 示例 6–1. 打印特殊变量

```bash
#!/bin/bash

# weirdvars.sh: 打印特殊变量。

var="\\(\$\\\\\$\

echo

IFS=''

echo $Svar       # 将 '${Svar}' 转换为空格。

echo "$Svar"    # 输出 '${Svar}'

exit 0
```

单引号（`''`）的操作方式与双引号（`""`）类似，但它不允许引用变量，`$` 的特殊含义会被关闭。在单引号内，除了 `\` 之外的每一个特殊字符都会被字面量解释。可以将单引号（“全引用”）视为一种比双引号（“部分引用”）更严格的引用方法。

由于即使是转义字符（`\`）在单引号内也会被字面解释，因此尝试在单引号内嵌套单引号将无法得到预期的结果。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_39_0.png)

```bash
echo "Why can't I write 's between single quotes"

echo

# 变通方法。

echo "Why can't I write ''''s between single quotes"

# ---------- ------------------------------------------------------

# 三个单引号字符串，带有转义和带引号的单引号

# 本示例由 Stephane Chazelas 提供。
```

转义是一种对单个字符的引用方法。位于字符前的转义字符（`\`）告诉 `shell` 对该字符进行字面量解释。

![](img/1ce1edffaa36e4f698a85430e71c6d3b_39_1.png)

对于某些命令和实用程序（如 `echo`、`sed`），转义一个字符可能会产生相反的效果——它可以开启或关闭该字符的特殊含义。

#### 用于 `echo` 和 `sed` 时的某些转义字符的特殊含义

| 字符 | 含义 |
| :--- | :--- |
| `\n` | 意味着换行 |
| `\v` | 意味着回车 |
| `\t` | 意味着制表符 |
| `\w` | 意味着垂直制表符 |
| `\b` | 意味着退格 |
| `\a` | 意味着“警报”（鸣响或闪烁） |
| `\07xx` | 翻译为 `\07xx` 的八进制 ASCII 等效值 |

### 示例 6–2. 转义字符

```bash
#!/bin/bash

# escaped.sh: 转义字符

echo echo

echo "\v\v\v\v"      # 打印 \v\v\v\v

# 使用 'echo' 的 -e 选项来打印转义字符。

echo -e "\v\v\v\v"    # 打印 4 个垂直制表符。

echo -e "\042"         # 打印 " （引号，ASCII 字符42）。

# '$X' 结构使得 -e 选项不再必要。

echo '$\n'               # 换行。

echo '$\a'               # 警报（鸣响）。

# Bash 2 及更高版本允许使用 '\xxx' 结构。

echo '$\t \042 \\t'     # 由制表符包围的引号 (")。

# 将 ASCII 字符赋值给变量。

------------------------------------------------------

quote='\042'             # 将 " 赋值给变量。

echo "\$quote This is a quoted string, \$quote and this lies outside the quotes"

echo

# 在变量中拼接 ASCII 字符。

triple_underscore='\137\137\137'  # # \137 是 '_' 的八进制 ASCII 码。

echo "\$triple_underline UNDERLINE \$triple_underline"
```

```bash
ABC=$'101\102\103\010' # 101, 102, 103 是 A, B, C 的八进制。

echo $ABC

echo; echo

escape=$'\033' # 033 是 escape 的八进制。

echo \"escape\" echoes as \$escape" 无可见输出。

echo; echo

exit 0
```

查看 [示例 35–1](#) 获取关于 `$'` 字符串扩展结构的另一个示例。

`\"` 赋予引号以字面含义

```bash
echo "Hello" # Hello

echo \"Hello\", he said. # \"Hello", he said.
```

`\$` 赋予美元符号以字面含义（`$` 后的变量名不会被引用）

```bash
echo "$variable01" # 结果为 \$variable01
```

`\\` 赋予反斜杠以字面含义

> `\\` 的转义和引用行为取决于其本身是否被转义、引用，或者出现在[命令替换](#substitution) 或[在此文档](#document) 之中。

```bash
echo \z # 简单的转义引用

echo \z # \z

echo \'z' # \z

echo \"z\' # \\z

echo \"z" # \z

echo \"z" # \z
```

```bash
echo \'z\' # 命令替换

echo \'z\' # \z

echo \\\"z\\\' # \\z

echo \\\\\"z\\\' # \\\\\z

echo \\\\\\\\\"z\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\z

echo echo \"z" # \z

echo echo \"z" # \z
```

```bash
cat <<EOF # 在此文档

\z

EOF
```

# 这些示例由 Stephen Chazelas 提供。

此详细的“`if`-`test`”解释由 Stephane Chazelas 提供。

### 示例 7–1. 什么是真？

```bash
#!/bin/bash

echo

echo "Testing \"0\"

if [ 0 ] # 0

then

echo "0 is true."

else

echo "0 is false."

fi # 0 is true.

echo

echo "Testing \"1\"

if [ 1 ] # 1

then

echo "1 is true."

else

echo "1 is false."

fi # 1 is true.

echo

echo "Testing \"-1\"

if [ -1 ] # 负1

then

echo "-1 is true."

else

echo "-1 is false."

fi # -1 is true.

echo

echo "Testing \"NULL\"

if [ ] # 空条件（空条件）

then

echo "NULL is true."

else
```
