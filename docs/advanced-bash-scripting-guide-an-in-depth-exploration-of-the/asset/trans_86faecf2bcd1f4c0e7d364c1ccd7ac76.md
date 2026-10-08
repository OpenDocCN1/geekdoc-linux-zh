

# 高级 Bash 脚本指南

```bash
# 以及“长”对角线的和也等于同一个数字。
# 由于是“正方形”，数组的行数和列数相同。
# 这个数字被称为“阶”。
# 一个 3 阶幻方的例子是：
# 8 1 6
# 3 5 7
# 4 9 2
# 所有行、列和两条长对角线的和都等于 15。
```

```bash
# 全局变量
MAXSIZE=31 # 31 行 31 列。
R_usage=90 # 调用错误。
dimension=-
  declare -i square
```

```bash
usage_message () {
  echo "用法: $0 order"
  echo " 其中 \$order（正方形大小）必须是一个奇数整数"
  echo " 范围在 3 - 31 之间。"
  # 实际上可以支持到 159 的正方形，
  # 但较大的正方形在终端窗口中无法进行格式化显示。
  # 尝试增加上面的 MAXSIZE。
  exit $SE_USAGE
}
```

```bash
calculate () {
  # 这里是实际工作的地方。
  local row col index dimaj k cell_val=1
  dimension=$1
  let dimaj=$dimension * 3; let dimaj=$dimension / 2; # 1.5 截断。
  for ((j=0; j < dimension; j++)) {
    for ((k=0; k < dimaj; k++)) {
      # 计算索引，转换为一维数组索引。
      # Bash 不支持多维数组。很遗憾。
      let col=$col + $j + dimaj; let col %=$dimension
      let row=$j * 2 - $col + $dimension; let row %=$dimension
      let index=$row*($col) + $col
      square[$index]=$cell_val; ((cell_val++))
    }
  }
}
```

```bash
# 纯数学计算，不需要可视化。
```

```bash
# 输出正方形，一次打印一行。
print_square () {
  local row col idx d1
  let d1=$dimension - 1  # 调整以零索引数组。
}
```

```bash
for row in $(seq 0 $d1); do
  for col in $(seq 0 $d1); do
    let idx=$row * $dimension + $col
    printf "%$3d" "${square[$idx]}"; echo -n ""
  done
done      # 在 80 列的终端窗口中整齐显示最多到 13 阶。
echo      # 每行后换行。
done
}

###########################################################
if [[ -z "$1" ] || [ "$1" -gt MAXSIZE ];
then
    usage_message
fi

let test_event = $1 % SEVEN
if [ $test_event -eq 0 ];
then
    # 无法处理偶数阶正方形。
    usage_message
fi

calculate $1
print_square # echo "\${square[@]}" DEBUG

exit $?
###########################################################

- 练习：
- 1) 添加一个函数来计算每行、每列和长对角线的和。这些和必须匹配。这是特定阶数正方形的“幻和”。
- 2) 让打印函数自动计算元素之间应分配多少空间以优化显示。这可能需要对 "printf" 行进行参数化。
- 3) 添加适当的函数生成具有“偶数”行/列的幻方。这并非易事(!)。请参考上方 Kwon Young Shin 的 URL 获取帮助。

# 附录 A 贡献脚本

## 附录 A 贡献脚本

### 示例 A-47. 十五数字

```bash
#!/bin/bash
 fifteen.sh

# 经典的“十五数字”
# 作者：Antonio Macchi
# 由 ABS Guide 作者进行轻微编辑和注释。
# 经许可在 ABS Guide 中使用。（感谢！）
```

> Sam Loyd 或 Noyes Palmer Chapman。
这个游戏在 19 世纪后期非常流行。

## 目标：重新排列数字，使其从 15 按顺序读取 -

| 1 | 2 | 3 | 4 |
|---|---|---|---|
| | 5 | 6 | 7 | 8 |
| 9 | 10 | 11 | 12 |
| 13 | 14 | 15 | |

```bash
####################
# 常量 #
SQUARES=16 #
FAIL=70 #
E_PREMATURE_EXIT=80 #
####################
```

```bash
########
# 数据 #
########
Puzzle={ 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 " " }
```

```bash
####################
# 函数 #
################
```

```bash
function swap
{
  local tmp
  tmp=${Puzzle[$1]}
  Puzzle[$1]=${Puzzle[$2]}
  Puzzle[$2]=$tmp
}
```

```bash
function Jumbo
{ # 在每回合开始时洗乱碎片。
  local i pos1 pos2

  for i in {1..100}
  do
    pos1=$(( ($RANDOM % $SQUARES ))
    pos2=$(( ($RANDOM % $SQUARES ))
    swap $pos1 $pos2
  done
}
```

```bash
function PrintPuzzle
{
  local il i2 puzpos
  puzpos=0

  clear
  echo "Enter quit to exit."; echo # 比 Ctrl-C 好。

  echo "","------" # 上边框。
  for il in {1..4}
  do
    for i2 in {1..4}
    do
      printf "|%2s" "${Puzzle[$puzpos]}"
      ((puzpos++))
    done
    echo "|" # 右边框。
    [ $il -eq 4 ] || echo "--------------------"
  done
  echo "----'----'--------" # 下边框。
}
```

