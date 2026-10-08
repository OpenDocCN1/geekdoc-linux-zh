

# 高级 Bash 脚本指南

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

# 27-2. 格式化诗

第 27 章 数组

# 高级 Bash 脚本指南

数组变量有自己独特的语法，甚至标准的 Bash 命令和操作符也有专门为数组设计的特殊选项。

# 示例 27-3. 多种数组操作

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
```

# 第 27 章 数组

# 高级 Bash 脚本指南

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

# 示例 27-4. 数组上的字符串操作

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

第 27 章 数组

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

第 27 章 数组

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
# (...) 是命令替换。
# 函数在子进程中运行。
# 函数将其输出（如果 echo 了输出）写入标准输出。
# 结合 "echo" 和命令替换，
# 可以读取函数的标准输出。
# name[] 符号指定了（等同于）"for-each"
# 操作。
# Bash 比你想象的要强大！
```

（注：此处原文有重复）
```
# name[] 符号指定了（等同于）"for-each"
# 操作。
# Bash 比你想象的要强大！
```

命令替换构造了数组的各个元素。

# 示例 27-5. 将脚本加载加载数组

```bash
#!/bin/bash
# script-array.sh: 将此脚本加载到数组。
# 灵感来自 Chris Martin 的邮件（感谢！）。
```

```bash
script_contents=$(cat "$0")      将此脚本的内容 ($0)
# 存储在数组中。
```

```bash
for element in $(seq 0 $(#script_contents[@]} - 1))
do
  # ${script_contents[$element]}
  # 给出数组中的元素个数。
```

```bash
#
# 问题：
# 为什么需要 seq 0？
# 尝试将其更改为 1。
```

```bash
echo -n "$script_contents[$element]"
# 在单行内出脚本的每个字段。
# "$script_contents[$element]" 同样适用于 ${ ... }。
echo -n "# 使用 " - " " 作为字段分隔符。
done
```

