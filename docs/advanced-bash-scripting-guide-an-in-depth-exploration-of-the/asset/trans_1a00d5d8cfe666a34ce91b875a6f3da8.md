

# 高级 Bash 脚本指南

```bash
t=$$
if [ "$t" -ne $DUPE_CARD ]
then
    parse_cards $t
ucards_picked+1
# 临时改回从1开始的索引。为什么？
let "$u" %= $CARDS_IN_SUIT
if [ "$u" -eq 0 ]
    # 嵌套的 if/then 条件测试。
then
    echo
    echo
fi # 每个手牌用空行隔开。

let "cards_picked += 1"
done
echo

return 0
}
```

# 结构化编程：
# 将整个程序逻辑模块化为函数。

==================================
seed_random
initialize_Deck
initialize_Suits
initialize_Cards
deal_cards
==================================

exit

# 练习 1：
# 为此脚本添加注释以完善文档。

# 练习 2：
# 添加一个例程（函数），按花色排序打印每个手牌。
# 你可以根据喜欢添加其他额外功能。

# 练习 3：
# 简化并优化脚本的逻辑。

## 37.2. Bash 版本 3

2004年7月27日，Chet Ramey 发布了 Bash 第 3 版本。这次更新修复了许多 Bug 并添加了新功能。

一些较重要的新增功能：

# 高级 Bash 脚本指南

一个新的通用的 {a..z} 大括号扩展运算符。

```bash
#!/bin/bash

for i in {1..10}
# 比之前的更简单、直观
+# for i in $(seq 10)
do
    echo -n "$i"
done
echo

# 1 2 3 4 5 6 7 8 9 10
```

```bash
# 或者直接使用 .
echo (a..z)      # a b c d e f g h i j k l m n o p q r s t u v w x y z
echo (e..m)      # e f g h i j k l
echo (z..a)      # z y w v u t s r q p o n l k j i h g f e c b a
# 也可以反向工作。
echo (25..30)    # 25 26 27 28 29 30
echo (3..1)       # 3 2 1
echo (X..d)       # X Y Z [ ] a b c d
# 显示 Z 和 a 之间的（部分）ASCII 字符，
+# 但不要依赖这种行为，因为 .
echo {1..a}      # 1..a
# 为什么呢？
```

# 你可以添加前缀和后缀。
echo "Number#{1..4}" "..."
# Number #1, Number #2, Number #3, Number #4, ...

```bash
# 你可以拼接大括号扩展集。
echo {1..3}{x..z} "-..."
# 1x1 + 1y2 + 1z2 + 2x1 + 2y2 + 2z2 + 3x3 + 3y3 + 3z + +
# 生成一个代数表达式。
# 这可以用于排列。
```

```bash
# 你可以嵌套大括号扩展集。
echo {a..c},{1..3}
# a b c 1 2 3
# “逗号”运算符会将字符串拼接在一起。
```

```bash
#############################################################################
# （遗憾的是，大括号扩展不支持参数化。）
var1=
var2=
echo "${var1}\${var2}" # (1..5)
```

```bash
# 然而，正如 Emiliano G. 指出的，使用 "eval" 可以克服这一局限性。
start=0
end=10
for index in $(eval "\$start..\$end"); do
    echo -n "$index" # 0 1 2 3 4 5 6 7 8 9 10
```

第 37 章.Bash 版本 2, 3 和 4

549

# 高级 Bash 脚本指南

- ${!array[@]} 运算符，可展开为给定数组的所有索引。

```bash
#!/bin/bash
Array=(element-zero element-one element-two element-three)
echo ${Array[0]}      # 数组的第一个元素。
echo ${!Array[@]}     # 0 1 2 3
                      # 数组的所有索引。

for i in ${!Array[@]}
do
    echo ${Array[i]}      # element-zero
                         # element-one
                         # element-two
                         # element-three

                         # 数组中的所有元素。
done
```

在双括号测试表达式中的 =~ 正则表达式匹配运算符。（Perl 也有类似的运算符。）

```bash
#!/bin/bash
variable="This is a fine mess."
echo "$variable"

# 在 [[ 双括号 ]] 内使用 =~ 运算符进行正则匹配
if [[ "$variable" =~ T........fines* ]];
# 注意：从 Bash 3.2 版本开始，这种匹配表达式不再工作。
then
    echo "match found"
    # 找到匹配项
fi
```

```bash
#!/bin/bash
input=$1

if [[ "$input" =~ "[0-9][0-9][0-9][0-9]" ]];
# 注意：从 Bash 3.2 版本开始，这里不需要引号。
# NNN
then
    echo "match found"
else
    echo "no match"
fi
```

第 37 章.Bash 版本 2, 3 和 4

550

（注：由于原文后半部分存在大量逻辑断层和重复，上述内容已根据核心技术含义进行了对齐翻译。）

