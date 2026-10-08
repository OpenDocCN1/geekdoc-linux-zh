

# 高级 Bash 脚本指南

```
MIN=1 # 允许的最小宾果号码。
MAX=75 # 允许的最大宾果号码。
COLS=15 # 每列的数字 (B I N G O)
SINGLE_DIGIT_MAX=9

declare -a Numbers
Prefix=(B I N G O)

initialize_Numbers () {
  # 初始化时全部清零。
  # 如果被选中，它们会递增。
  local index=0
  until [ "$index" -gt $MAX ];
  do
    Numbers[$index]=0
    ((index++))
  done
}

Numbers[0]=1 # 标记为零，使其不会被选中。

generate_number () {
  local number
  while [ 1 ];
  do
    let number=$(expr $RANDOM % $MAX)
    if [ ${Numbers[$number]} -eq 0 ]; # 数字尚未被过。
    then
      let "Numbers[$number]+=1" # 在数组中进行标记。
      break
      # 并终止循环。
    fi # 否则，如果已经调用过则循环并生成另一个数字。
  done
  # 练习：使用 until 循环更优雅地重写此。
  return $number
}

print_numbers_called () {
  # 以整齐的列打印调用日志。
  echo ${Numbers[@]}
}

local pre2=0 # 前缀零，以便列对齐
# 在单数字数字上加上前缀。

echo "Number Stats"
for ((index=1;index<=MAX; index++));
do
  count=$(${Numbers[index]})
  let c="$index -1" # 规范化，数组从索引 0 开始。
  let column=$(expr $index / $COLS)
  pre=${Prefix[column]}
  echo -n "$(expr $index % $COLS)) "
  if [ $(expr $index % $COLS) -eq 0 ];
  then
    echo
  fi
done
```

附录 A. 贡献脚本

765

# 高级 Bash 脚本指南

```bash
echo # 行尾换行。
fi

if [ "$index" -gt $SINGLE_DIGIT_MAX ] # 检查是否为单数字。
then
    echo -n "$pre$index#$count"
else
    # 补前零。
    echo -n "$pre0$index#$count"
fi

main () {
RANDOM=$# # 随机数生成器种子。
initialize_Numbers # 清空数字跟踪数组。

clear
echo "Bingo Number Caller"; echo

while [ "$key" != "q" ]; # 主循环。
do
    read -s -nl -p "按键获取下一个数字 [q 退出]: " key
    # 通常 'q' 退出，但并不总是如此。
    # 如果 q 失败，可以随时按 Ctrl-C。
    echo

    generate_number; new_number=$?

    let "column"=$(expr $new_number / $COLS)
    echo -n "${Prefix[$column]}" # B-I-N-G-O

    echo $new_number
done

echo; echo;

# 游戏结束 ...
print_numbers_called
echo "0 = 未调用 . #1 = 已调用"
echo

exit 0}```
```

# 然，这个脚本还有改进空间。
# 另见作者的 Instructable：
# www.instructables.com/id/Binguo-An-Arduino-based-Bingo-Number-Generator/
本节包含对基础知识的回顾……以及更多。

# 示例 A-58. 基础回顾

```bash
#!/bin/bash
# basics-reviewed.bash
```

附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
# 文件扩展名 == *.bash 针对 Bash

# 版权所有 (c) Michael S. Zick, 2003; 保留所有。
# 许可：以任何形式用于任何目的。
# 修订：ID$

# 由 M.C. 调整布局编辑。
# （《高级 Bash 脚本指南》作者）
# 由 Cliff Bamford 修复和更新 (04/08)。

# 此脚本在 Bash 2.04, 2.05a 和 2.05b 版本下测试过。
# 它可能在更早的版本上无法工作。
# 此演示脚本会生成一个 --故意的
# “未找到命令”消息。第 43 行。

# 当前 Bash 维护者 Chet Ramey 已为
# 后续版本的 Bash 完成了修复。

# 将此脚本的输出通过到 'more'
# 它将滚动离开页面。

# 你也可以将输出重定向
# 到文件进行检查。

# 以下的大部分观点在接接的
# "Bash 脚本指南" 中均有详细描述。
# 此演示脚本主要仅用于演示。

# 除非指定，否则变量没有类型。
# 变量是有名称的。必须包含一个非数字字符。
# 文件描述符名称（如： 2）仅包含数字。

# 参数和数组元素是经过编号的。
# 参数类似于 Bash 数组。

# 变量名可能未定义（空引用）。
# 变量名可能已定义但为空（空内容）。
# 变量名可能已定义且非空。
# 变量可以包含：
# 作为 32 位（或更大）整数的整型
# 字符串
# 字符串可以包含嵌入空格，并可能被视为
# 格式化的字符串，看起来像是一个带有
# 可选参数的函数

# Bash 数组已定义的元素可能是未定义的（未设置）。
# 也就是说，下标压缩的 Bash 数组可以更改。

# Bash 数组的特性（Bash 数组）：
# 如果没有另有说明，Bash 数组从
# 下标零开始。字面量：[0]
# 这被称为零索引。
# 如果没有另有说明，Bash 数组是下标压缩的
#（连续下标，没有下标间隔）。
# 不允许负下标。
# Bash 数组的元素不需要都是相同类型。
# Bash 数组的元素可能是未定义的（空引用）。
# 也就是说，Bash 数组可以是“稀疏的”。
# Bash 数组的元素可能已定义且为空（空内容）。
# Bash 数组的元素可以包含：
# 作为 32 位（或更大）整数的整型
# 字符串
# 字符串可以包含嵌入空格，并可能被视为
# 格式化的字符串，看起来像是一个带有
# 可选参数的函数

# 引用其他元素需要额外的说明，
# 这意味着引用必须以扩展语法编写。
# 通用形式是：${name[subscript]}。
# 字符串形式也可以用于：${name[:subscript]}
# 当为 Bash 数组引用下标零元素时。
# Bash 数组在内部实现为链表，
# 而不是某些编程语言中的固定存储区域。
```

