
# 第 25 章 别名

## 高级 Bash 脚本指南

### unalias 命令用于移除之前设置的别名 (`alias`)。

**示例 25-2. `unalias`：设置和取消别名**

```bash
#!/bin/bash

# unalias.sh

set -s expand_aliases # 启用别名展开。

alias llm='ls -al | more'

llm

echo

unalias llm # 取消别名。

llm

# 错误信息结果，因为 'llm' 不再被识别。

exit 0
```

```bash
bash ./unalias.sh
```

```
total 6
drwxrxr-x 2 bozo bozo 3072 Feb 6 14:04 .
drwxr-xr-x 40 bozo   2048 Feb 6 14:04 ..
-rw-r--r-- 1 bozo   bozo   199 Feb 6 14:04 unalias.sh
./unalias.sh: llm: command not found
```

# 第 26 章 列表结构

`and` 和列表（list）结构提供了连续处理命令的方法。这些可以高效地替换嵌套的 `if/then` 甚至 `case` 语句。

## 命令链

### `and` 和列表

```
command-1 && command-2 && command-3 && ... command-n
```
每个命令顺序执行，前提是上一个命令返回真值（零）。在遇到第一个假（非零）返回时，命令链终止（第一个返回假的命令是最后一个执行的命令）。

这是一个来自早期版本《永叶俄罗斯方块》游戏脚本的两个条件 `and` 列表的有趣用法：

```bash
equation()
{
  # 用于坐标倍倍和减半的核心算法
  [[ $(cdx) && ((y=cy+(ccy-cdy)*(2)) ]]
  eval $[1]+=$(x) ${y}
}
```

### 示例 26-1. 使用 `and` 和列表处理命令参数行

```bash
#!/bin/bash

# list

if [ ! -z "$1" ] && echo "Argument $1" && [ ! -z "$2" ] || \
  echo "Argument $2 = $2"
then
  echo "传递给脚本的参数至少有2 个。"
  # 所有链命令都返回真。
else
  echo "传递给脚本的参数少于2 个。"
  # 链命令中至少有一个返回假。
fi

# 注意 "if [ ! -z $1" ] 是有效的，但它所谓的等效写法
# "if [ -n $1" ] 却并不有效。
#   然而，加引号可以修复此。
#   if [ -n "$1" ] 是有效的。
#     ^  小心！
#   最好始终对待测试的变量加上引号。

# 这使用“纯”if/then 语句实现了相同的功能。
if [ ! -z "$1" ]
then
  echo "Argument $1 = $1"
fi

if [ ! -z "$2" ]
then
  echo "Argument $2 = $2"
  echo "传递给脚本的参数至少有2 个。"
fi

else
  echo "传递给脚本的参数少于2 个。"
fi

# 使用“and 列表”会更长且更笨拙，
```

### 示例 26-2. 使用 `and` 列表的另一个命令行参数测试

```bash
#!/bin/bash

ARGS=1            # 预期的参数数量。

E_BADARGS=85      # 如果参数数量错误时的退出值

test -ne $ARGS && $0
^^^^^^^^^^^^^^ condition #1 exit $E_BADARGS
echo "Usage: `basename $0` $ARGS argument(s)" $E_BADARGS

# 如果 condition 1 测试为真（传递给脚本的参数数量错误）
# 则执行行的剩余部分，脚本终止。
# 下一行仅在上述测试失败时才执行。

echo "传递给此脚本的参数数量正确。"

exit 0
```

当然，`and` 列表也可以为变量设置默认值。

```bash
arg1=$@ && [ -z "$arg1" ] || arg1=DEFAULT

# 如果有命令行参数，则将 arg1 设置为这些参数。
# ... 否则设置为 DEFAULT。
```

### `or` 和列表

```
command-1 | command-2 | command-3 ... command-n
```
每个命令顺序执行，只要上一个命令返回真。在第一个假时，链终止（第一个返回假的命令是最后一个执行的）。这显然是“and 列表”的反面。

### 示例 26-3. 在 `and` 列表中使用列表

```bash
#!/bin/bash
# delete.sh, 不简单的。

E_BADARGS=85

if [ -z "$1" ]; then
  echo "Usage: `$0`"
else
  file=$1 # 设置文件名。
fi
```

```bash
[ ! -f "$file" ] && echo "File found."
# AND 列表，如果文件存在则。
# 注意后续行。
```

```bash
[ ! -f "$file" ] || rm -f "$file"
# OR 列表，如果文件存在则删除。
# 注意逻辑。
```

```bash
[ ! -f "$file" ] || echo "File deleted"
# AND 列表，如果文件存在则输出。
```

```bash
exit?
# 如果 or 列表返回真，它将执行。
```

`and` `or` 列表的退出状态是最后一个命令的退出状态。复杂的 `and` `or` 列表可能会变得晦涩，可能需要调试。

```bash
false && true || echo false # false
```
# 结果相同

```bash
( false && true ) || echo false # false
```
# 但是

```bash
false && ( true ) # (空)
```

# 注意语句从左到右的评估。
# 最好避免这种复杂性。
# 感谢，S.

参见示例 A-7 和 7-4 关于使用 `and` 列表测试变量的说明。

# 第 27 章 数组

新版本的 Bash 支持一维数组。数组元素可以使用 `variable[xx]` 符号进行初始化。或者，脚本可以通过显 `declare` 语句引入整个数组。要引用（检索）数组元素的内容，使用大括号符号，即 `${element}`。

## 示例 27-1. 简单数组用法

```bash
#!/bin/bash

area[11]=23

area[13]=37

area[51]=UFO

# 数组成员不需要连续或相邻。
# 数组的某些成员可以留空初始化。
# 数组中的间隙是可以的。
# 事实上，稀疏数据的数组（稀疏数组）
# 在表格处理软件中非常有用。

echo -n "area[11]" = ""
echo ${area[11]} # 需要大括号。

echo -n "area[13]" = ""
echo ${area[13]}

echo "Contents of array[51] are ${area[51]}"

# 未初始数组变量的内容会打印为空（空变量）。
echo -n "area[43]" = ""
echo ${area[43]}
echo "area[43] unassigned"
echo

# 将两个数组变量的和赋值给第三个
area[5]=${area[11]} + ${area[13]}
echo "area[5]" = area[11] + area[13]
echo -n "area[5]" = ""
echo ${area[5]}

area[6]=${area[11]} + ${area[51]}
echo "area[6]" = area[11] + area[51]
echo -n "area[6]" = ""
echo ${area[6]}

# 这会失败，因为不允许向字符串加整数。

echo; echo; echo

--------------------------------------
# 另一个数组，“area2"
```

```bash
# 数组变量赋值的另一种方法...
# 名=( XXX YYY ZZZ ... )

area2=( zero one two three )

echo -n "area2[0] = ""
echo ${area2[0]}

# 啊，从 0 开始索引（数组的第一个元素是 [0]，而不是 [1]）。
echo -n "area2[1] = ""
echo ${area2[1]} # [1] 是数组的第二个元素。

--------------------------------------------------------------------------------
echo; echo; echo

--------------------------------------------------------------------------------
# 另一个数组 "area3"
# 数组变量赋值的另一种方法...
# array_name=([xx]=XXX [yy]=YYY ...)

area3=([17]=seventeen [24]=twenty-four)

echo -n "area3[17] = ""
echo ${area3[17]}

echo -n "area3[24] = ""
echo ${area3[24]}

--------------------------------------------------------------------------------
exit 0
```

正如我们所看到的，初始化整个数组的一种方便方法是 `array=(element1 element2 ... elementN)` 符号。

```bash
base64_charset=((A..Z) [a..z] (0..9) + /=)

# 使用扩展括号展开
# + 初始化数组的元素。
# 摘自 vladz 的 "base64.sh" 脚本
# 位于“贡献脚本”附录中的 +。
```

Bash 允许对变量进行操作，即使这些变量没有显式声明。

```bash
string=ABC123ABCabc

echo ${string[#]} # ABC123ABCabc
echo ${string[*]} # ABC123ABCabc
echo ${string[0]} # ABC123ABCabc
echo ${string[1]} # 无输出！
echo ${string[@]} # 为什么？

# 1
# 数组只有一个元素。
# 字符串本身。
```
# 感谢 Michael Zick 指出。
再次证明了 Bash 变量是无类型的。

## 示例 27-2. 格式化诗

数组变量有自己独特的语法，甚至标准的 Bash 命令和操作符也有专门为数组设计的特殊选项。

## 示例 27-3. 多种数组操作

```bash
#!/bin/bash

# array-ops.sh: 数组的更多乐趣。

array=( zero one two three four five )

# 元素 0 1 2 3 4 5

echo ${array[0]}      # zero

echo ${array:0}       # zero
                      # 第一个元素的参数扩展，
                      # 从位置 # 0（第一个字符）开始。

echo ${array:1}       # ero
                      # 第一个元素的参数扩展，

# 第 27 章 数组
# 高级 Bash 脚本指南
```

```bash
echo "------------------"
# 从位置 # 1（第二个字符）开始
echo ${#array[0]}      # 4
# 数组第一个元素的长度。

echo ${#array}         # 4
# 数组第一个元素的长度。
# （备用表示法）

echo ${#array[1]}      # 3
# 数组第二个元素的长度。
# Bash 中的数组具有从 0 开始的索引。

echo ${#array[*]}      # 6
# 数组中的元素个数。

echo ${#array[@]}      # 6
# 数组中的元素个数。

echo "----------------------------------"

array2=( [0]="first element" [1]="second element" [3]="fourth element" )

# 引号允许在单个数组内嵌入空格
echo ${array2[0]}      # first element
echo ${array2[1]}      # second element
echo ${array2[2]}      # 
echo ${array2[3]}      # fourth element
# 初始化中跳过，因此为空。

echo ${#array2[0]}      # 13 (第一个元素的长度)
echo ${#array2[*]}      # 3 (数组中的元素个数)

exit
```

许多标准的字符串操作都适用于数组。

## 示例 27-4. 数组上的字符串操作

```bash
#!/bin/bash

# array-ops.sh: 数组上的字符串操作。
# Michael Zick 编写脚本。
# 用于权限管理。
# 修复：2008年5月，8月28日。
# 通常情况下，任何字符串操作使用 ${name}...
# 都可以应用于数组中的所有字符串元素，
# 使用 ${name[@]} 或 ${name[*]} 符号。

array2={ one two three four }

# 尾部字符串提取
echo ${array2[@]:0}      # one two three four
# 所有元素。
```

# 高级 Bash 脚本指南

```bash
# 子字符串删除
echo ${array[@]:1:2}      # two
# element[0] 之后的所有元素

# 从开头删除最短匹配
echo ${array[@]}%f*}      # two three five
# 应用于数组的所有元素。
# 匹配 "Four" 并将其删除。

# 从开头删除最长匹配
echo ${array[@]}##t*}     # two four five
# 应用于数组的所有元素。
# 匹配 "three" 并将其删除。

# 从结尾删除最短匹配
echo ${array[@]}%%*h*}     # two four five
# 应用于数组的所有元素。
# 匹配 "three" 并将其删除。

echo "-----------------"

# 字符串替换
# 替换第一个匹配项的字符串。
echo ${array[@]}fv/         # one five
# 应用于数组的所有元素。

# 替换所有匹配项。
echo ${array[@]}ve/         # one four five
# 应用于数组的所有元素。

# 删除所有匹配项。
# 未指定替换项默认为删除...
echo ${array[@]}fi/          # one four five
# 应用于数组的所有元素。

# 替换开头匹配项。
echo ${array[@]}#/         # four five
# 应用于数组的所有元素。

# 替换结尾匹配项。
echo ${array[@]}%%/         # two three four
# 应用于数组的所有元素。

echo "-----------------"
```

# 高级 Bash 脚本指南

```bash
replacement() {
  echo -n "!!!!"
}
```

```bash
echo ${array[0]}/%$(replacement)}
# 元素!
# 这里的 stdout 是替换字符串。
# Q.E.D: 替换动作实际上是“赋值”。
```

```bash
echo "------------------------"
# 访问 "for-each":
echo ${array[0]}/${optional_arguments}
```

```
# !!! !!! !!! !!! !!! !!!
# 现在，如果 Bash 只会将匹配的字符串
# 传递给调用的函数 . . .
```

```
echo
exit 0
```

```
# 在求助于大锤 —— Perl、Python 或其他之前
# 回想一下：
```
