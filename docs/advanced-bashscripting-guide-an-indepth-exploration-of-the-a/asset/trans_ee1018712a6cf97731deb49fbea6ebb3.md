

# 高级 Bash 脚本指南

```
MAXCOUNT=10
count=1
echo "$MAXCOUNT random numbers:"
echo "------------------"
while [ "$count -le $MAXCOUNT ]; do
  # 生成 10 ($MAXCOUNT) 个随机整数。
  number=$RANDOM
  echo $number
  let count += 1  # 计数加
done
echo "------------------"
```

# 如果你需要一个特定范围内的随机整数，请使用“取模”运算符。
# 它返回除法运算的余数。

```
RANGE=500
echo
number=$RANDOM
let "number %= $RANGE"
echo "Random number less than $RANGE  --- $number"
echo
```

# 如果你需要一个大于下限的随机整数，
# 请设置一个测试来丢弃所有低于下限的数字。

```
FLOOR=200
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
done
echo "Random number greater than $FLOOR  --- $number"
echo
```

# 可以结合上述两种技术来获取两个数字之间的随机数。

```
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
  let "number %= $RANGE"  # 将数字缩小到 $RANGE 范围内。
done
echo "Random number between $FLOOR and $RANGE  --- $number"
echo
```

# 生成二选一，即“真”或“假”值。

```
BINARY=2
number=$RANDOM
T=1
let "number >= 14"  可以提供更好的随机分布
# (右) 移出除了最后一个二进制位以外的所有内容。
if [ "$number" -eq $T ];
then
```

# 9.6. $RANDOM: 生成随机整数

```
echo "TRUE"
else
echo "FALSE"
fi

echo

# 可以模拟掷骰子。
SPOTS=7 # 取模 7 范围 0 - 6。
DICE=2
ZERO=0
diel=0
diel2=0

# 分别投掷，这样就能获得正确的概率。

while [ "$diel" -eq $ZERO ]; # 不能出现零。
do
    let diel = $RANDOM % $SPOTS # 掷第一个骰。
done

while [ "$diel2" -eq $ZERO ];
do
    let die2 = $RANDOM % $SPOTS # 掷第二个骰。
done

let throw = $diel + $die2
echo "Throw of the dice $throw"
echo
```

RANDOM 到底有多随机？测试此点的最佳方法是编写一个脚本，跟踪 RANDOM 生成的“随机”数的分布。让我们投掷几次 RANDOM 吧……

# 示例 9–22. 使用 RANDOM 掷骰子

```
#!/bin/bash
# RANDOM 到底有多随机

RANDOM=$RANDOM # 使用脚本进程 ID 重新种子随机数生成器。

PIPS=6 # 骰子有 6 个点。
MAXTHROWS=600 # 如果你没别的事要做，可以增加这个值。
throw=0 # 投掷次数。

zeros=0 # 必须将计数初始化零。
ones=0 # 因为未初始化的变量是空，而不是零。
twos=0
trees=0
fours=0
fives=0
sixes=0

print_result ()
{
echo
echo "ones" = $ones
echo "twos" = $twos
echo "threes" = $threes
echo "fours" = $fours
echo "fives" = $fives
echo "sixes" = $sixes
echo
}
```

```
update_count() {
  case $1 in
    0) let "ones" += 1;; # 因为没有“零”，这对应于 1
    1) let "twos" += 1;; # 对应于 2，以此类推。
    2) let "threes" += 1;;
    3) let "fours" += 1;;
    4) let "fives" += 1;;
    5) let "sixes" += 1;;
  esac
}
```

```
while [ "$throw" -lt "$MAXTHROWS" ]
do
  let "diel" = RANDOM % $PIPS
  update_count $diel
  let "throw" += 1
done
```

# 假设 RANDOM 是相当随机的，得分分布应该均匀。
# 当 MAXTHROWS 为 600 时，所有结果都应该集中在 100 左右，正负 20。

# 请记住 RANDOM 是一个伪随机生成器，
# 而且它并不是特别特别优秀。

# 练习（简单）：
# ----------------
# 重写此脚本来抛掷 1000 次硬币。
# 选择是“HEADS”（正面）或“TAILS”（反面）。

exit 0

正如我们在上一个示例中看到的，每次调用 RANDOM 时都“重新种子” RANDOM 生成器是最好的。对 RANDOM 使用相同的种子会重复相同的数字序列。（这反映了 C 语言中 random() 函数的行为。）

# 示例 9-23. 为 RANDOM 种子

```bash
#!/bin/bash
# seeding-random.sh: 为 RANDOM 变量设置种子。

MAXCOUNT=25
# 生成多少数字。
random_numbers() {
  count=0
  while [ "$count" -lt "$MAXCOUNT" ]
  do
    number=$RANDOM
  echo -n "$number "
    let count += 1
  done
  echo
}
```

```bash
RANDOM=1
random_numbers
```

> 设置 RANDOM 会种子随机数生成器。

echo; echo

```
RANDOM=1
random_numbers
```

> 对 RANDOM 使用相同的种子……
# ...会复制相同的数字序列。
# 什么时候需要重复同一个“随机”数字序列？

echo; echo

```
RANDOM=2
random_numbers
```

> # 再次尝试，但使用不同的种子……
# 会产生不同的数字序列。

echo; echo

```
# RANDOM=$$ 根据脚本 ID 为 RANDOM 设置种子。
# 也可以从 'time' 为 RANDOM 设置种子。
```

