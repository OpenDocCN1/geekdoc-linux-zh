
# 高级 Bash 脚本指南

## 第 27 章 数组

### 1. 数组元素计数

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。

element_count=${#array[@]}

echo $element_count
```

注意括号：

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。

element_count=${#array[@]}

echo $element_count
```

比较数字显示，第二种形式（`Stephanie Chazelas` 指出的）更快。正如 `Chazelas` 所解释的：`BigTwo` 是逐元素赋值的（因为有括号），而 `bigThree` 是作为一个单一字符串赋值的。因此，本质上，你拥有：

```bash
bigTwo=("0..." "1..." "2...")

bigThree=("0..." )
```

验证这一点：

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。

element_count=${#array[@]}

echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。`MSZ`：各位，很抱歉。

注意：第 32 行和第 44 行中的 `declare-a` 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 `declare -a` 语句可能会加快对数组操作的执行。

### 27. 数组的复制与合并

```bash
#!/bin/bash

## CopyArray.sh

# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {

    # 赋值命令构建器

    echo -n 'eval '

    echo -n "$2"          # 目标名称

    echo -n '${ # 源名称

    echo -n "$1"

    echo -n '[@]'

}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”

CopyArray=CpArray_Mac          # 语句构建器

Hype()

{

    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。

    local -a TMP

    local -a hype=( Really Rocks )

    $(CopyArray $1 TMP)

    TMP=${$TMP[@]} ${hype[@]}

    $(CopyArray TMP $2)

}
```

```bash
declare -a before=( Advanced Bash Scripting )

declare -a after

echo "Array Before = ${before[@]}"

Hype before after

echo "Array After = ${after[@]}"
```

吹过头了？

```bash
echo "What ${after[@]:3:2}"

declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )

# 子字符串提取

echo "Array Modest = ${modest[@]}"
```

`'before'` 发生了什么？

```bash
exit 0
```

### 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash

# array-append.bash

# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

`Paulo Marcel Coelho Aragoja` 建议使用 `for` 循环作为更简单的替代方案。

```bash
# for (( last = $number_of_elements - 1 ; last > 0 ; last-- ))
#    By C.Y. Hunt (感谢!)
# do
#   for (( i = 0; i < last; i++ ))
#     do
#       echo "${Countries[$i]}" "${Countries[$((i+1))]}" \ \
#       exchange $i ($((i+1)))
#     do
# done
```

由于“最重”的元素会浮到底部，我们每轮需要少进行一次比较。

```bash
echo $count: ${Countries[@]}" 在每轮循环结束时打印结果数组。

let count += 1

done

# 外层循环结束
# 全部完成。
```

```bash
exit 0
```

## 可以在数组中嵌套数组吗？

```bash
#!/bin/bash

# “嵌套”数组。
# Michael Zick 提供了这个示例，
# William Park 进行了修正和澄清。

AnArray=($is --inode --ignore-backups --almost-all \ \
--directory --full-time --color=none --time=status \ \
--sort-time -1 ${PWD}) # 命令选项。
# 空格是有意义的……且对上述内容不加引号。
```

```bash
SubArray=${AnArray[0]:11:1} ${AnArray[6]:5}

# 这个数组有六元素：
# SubArray=${AnArray[1]} [1]=${AnArray[6]} [2]=${AnArray[7]}
# [3]=${AnArray[8]} [4]=${AnArray[9]} [5]=${AnArray[10]}
```

```bash
# Bash 中的数组是（循环的）链表
# 类型为字符串（字符）。
# 所以，这实际上并不是嵌套数组，
# 但功能上是相似的。
```

```bash
echo "当前目录和日期最后状态:"
echo "${SubArray[@]}"
```

```bash
exit 0
```

### 示例 27-12. 嵌入数组与间接引用

嵌入数组结合间接引用创建了一些迷人的可能性

```bash
#!/bin/bash

## embedded-arrays.sh

# 嵌入数组与间接引用。
# 脚本由 Dennis Leeuw 创建。
# 经许可使用。
# 由作者修改。

ARRAY1=(
VAR_1=value1
VAR_2=value2
VAR_3=value3
)

ARRAY2=(
VARIABLE="test"
STRING="${VAR1}=value1VAR2=value2VAR3=value3"
ARRAY21=${ARRAY1[*]}
) # 在此数组内嵌入 ARRAY1。

function print () {
OLD_IFS="$IFS" # 输出每个数组元素
IFS=$'\n' # 分行打印。
TEST1="ARRAY2[*]"
local ${!TEST1} # 查看删除此行会发生什么。
# 间接引用。
# 这使得 $TEST1 的组件
# 可以被此函数访问。
# 看看我们目前得到了什么。

echo
echo "$TEST1 = ${!TEST1}" # 仅变量名。
echo;
echo "${!TEST1} = ${${!TEST1}}" # 变量的内容。
# 这就是间接
# 引用的作用。

echo
echo ""
echo
# 打印变量
echo "Variable VARIABLE: $VARIABLE"
# 字符串元素
IFS="$OLD_IFS"
TEST2="${!2}"
local ${!TEST2} # 间接引用（同上）。
echo "String element VAR2: $VAR2 from STRING"
# 打印数组元素
TEST2="ARRAY21[*]"
```

```bash
local ${!TEST2} # 间接引用（同上）。
echo "Array element VAR1: $VAR1 from ARRAY21"
print
echo
exit 0
```

如脚本作者提到的，“你可以轻松扩展它来在 `bash` 中创建哈希。”读者的（困难）练习：实现它。使用数组实现脚本版本的埃拉托尼筛法。当然，这种计算资源密集型应用应该用 `C` 等编译语言编写。作为脚本，它的运行速度极其缓慢。

### 示例 27-13. 埃拉托尼筛法

```bash
#!/bin/bash

# sieve.sh (ex68.sh)
# 埃拉托尼筛法，寻找质数的古代算法。
# 运行速度比对应的 C 语言程序慢几个数量级。

LOWER_LIMIT=1 # 从 1 开始。
UPPER_LIMIT=1000 # 到 1000（如果你有时间，可以设置更高）。

PRIME=1
NON_PRIME=0

let SPLIT=UPPER_LIMIT/2 # 优化：仅测试到上限一半的数字。为什么？

declare -a Primes # Primes[] 是一个数组。

initialize() {
# 初始化数组。
i=$LOWER_LIMIT
until [ $i -gt $UPPER_LIMIT ]; do
  Primes[$i]=$PRIME
  let i += 1
done
# 假设所有数组成员都是有罪的（质数），直到证明无辜。
}

print() {
# 打印 Primes[] 数组中标记为质数的成员。
i=$LOWER_LIMIT
until [ $i -gt $UPPER_LIMIT ]; do
  if [Primes[$i]} -eq $PRIME ]; then
    printf "%8d" "$i" # 每个数字 8 个空格对齐
  fi
  let i += 1
done
}

sift () {
# 筛掉非质数。
i=$LOWER_LIMIT+1 # 从 2 开始。
until [ $i -gt $UPPER_LIMIT ]; do
  if [Primes[$i]} -eq $PRIME ]; then # 已经筛过的（标记为非质数）。
    t=$i
    while [ $t -le $UPPER_LIMIT ]; do
      let t += 1
      Primes[$t]=$NON_PRIME # 标记为非质数的倍数。
    done
  fi
  let i += 1
done
}

#===========================
# main ()
# 顺序调用函数。

initialize
sift
print # 这就是所谓的结构化编程。
#============================

echo

# 以下代码因为 'exit' 不执行。
# Stephane Chazelas 改进的 Sieve 版本运行快一些。
# 必须带命令行参数调用（质数限制）。

UPPER_LIMIT=$1 # 来自命令行。
let SPLIT=UPPER_LIMIT/2 # 到上限一半。

Primes=$(seq $UPPER_LIMIT)

i=1
until (( i += 1 )); do # 只需要一半。
  if [ -nPrimes[$i]} ]; then
    t=$i
    until (( t += i ) > UPPER_LIMIT); do
      Primes[$t]=;
    done
  fi
done

echo ${Primes[*]}
exit $?
```

### 示例 27-14. 优化的埃拉托尼筛法

```bash
#!/bin/bash
# 优化的埃拉托尼筛法
# Jared Mattin 编写脚本，ABS 作者微调。
# 在 ABS Guide 中使用（感谢他！）。

# 基于高级 Bash 脚本指南。
UPPER_LIMIT=$1 # 质数的上限。

Primes=$(seq $UPPER_LIMIT)

typeset -i t
Primes[$i-1]=$i # 1 不是质数。
until (( i += 1 )) > $((UPPER_LIMIT)/i); do # 只需要 i 方式。
  if [Primes[t*(i-1)] -eq $i ]; then # 为什么？晦涩但有启发性，下标中使用算术扩展。
    until (( t += i) > UPPER_LIMIT )); do
      Primes[t]=;
    done
  fi
done
# echo ${Primes]}
echo # 改回原始脚本进行漂亮打印（80 列显示）
printf "%s\n" "${Primes[@]}"
echo; echo

exit $?
```

将这些基于数组的质数生成器与不使用数组的方案进行比较，示例 `A-15` 和示例 `16`。

数组在某种程度上可以模拟 `Bash` 无原生支持的数据结构。

### 27-15. 模拟栈

```bash
#!/bin/bash
# stack.sh: 栈模拟

# 类似于 CPU 栈，栈按顺序存储数据项，
# 但按相反顺序释放它们，后进先出。

BP=100 # 栈基指针。
# 从 100 开始。

SP=$BP

declare -a stack # 栈数组。

push() {
  if [ -z "$1" ]; then
    return
  fi

  let SP -- "$1" # 移动栈指针。
  stack[$SP]=$1
}

pop() { # 从栈弹出元素。
  if [ $SP -eq $BP ]; then # 栈为空？
    return
  fi

  Data=${stack[$SP]}
  let SP += 1 # 移动栈指针。
  return
}

status_report() { # 查看发生了。
echo "--------------------------------"
echo "--------------------------------"
echo "REPORT"
echo "Stack Pointer = $SP"
echo "Just popped \"\$Data\" off the stack."
echo "--------------------------------"
echo
}

#=================================================
# 现在玩点。
echo

# 看看能否从空栈中弹出东西。
pop
status_report
echo

push garbage # 垃圾入，垃圾出。
pop
status_report

value1=23; push $value1
value2=skidoo; push $value2
value3=LAST; push $value3

pop # LAST
status_report
pop # skidoo
status_report
pop # 23 # 后进先出！

# 注意栈指针每次 push 递减，
# 每次 pop 递增。
echo
```

```bash
exit 0

# ==========================
```

## 练习：

- 1) 修改 `push()` 函数，允许通过单次函数调用向栈中推入多个元素。
- 2) 修改 `pop()` 函数，允许通过单次函数调用从栈中弹出多个元素。
- 3) 为关键函数添加错误检查。即，根据操作执行的成功或失败返回错误代码，并采取适当措施。
- 4) 以此脚本为起点，编写一个基于栈的 4 功能计算器。

对数组 `sub` 进行复杂的操作可能需要中间变量。对于涉及此类操作的项目，请再次考虑使用更强大的编程语言，如 `Perl` 或 `C`。

### 示例 27-6. 复杂的数组应用：探索一个奇特的数学序列

```bash
#!/bin/bash

# Douglas Hofstadter 臭名昭著“Q序列”
# Q(1) = Q(2) = 1
# n>2 时 Q(n) = Q(n-1) + Q(n-2)

# 这是一个具有奇异且不可预测行为的“混沌”整数序列。
# 该序列的前 20 项是：
# 1 2 3 3 4 5 6 6 8 8 8 9 10 10 11 12
```

```bash
# 参见 Hofstadter 的书《Gödel, Escher, Bach: An Eternal Golden Braid》，
# 第 137 页。

LIMIT=100
# 要计算的项数。
WIDTH=20
# 每行打印的项数。
Q[1]=1
# 序列的前两项为 1
```

```bash
echo
echo "Q-series [$LIMIT terms]:"
echo -n "${Q[1]}"
# 输出前项。
echo -n "${Q[2]}"

for ((n=3; n<=$LIMIT; n++)); do # 类似 C 的循环表达式。
  do # n>2 时 Q[n] = Q[n-1] + Q[n-2]
  # 需要将表达式拆分为中间项，
  # 因为 Bash 不擅长处理复杂的数组算术。
```
