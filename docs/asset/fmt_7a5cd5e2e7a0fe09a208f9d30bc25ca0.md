
## 9.3. 参数替换

```bash
#!/bin/bash

var=abcd-1234-def
echo "var = $var"

t=${var#*}
echo "var (已删除从第一个 - 开始并包含在内的所有内容) = $t"
# t=${var#*-} 的效果完全相同，
# 因为 * 匹配第一个字符串，
# 且 * 匹配其之前的所有内容，包括空字符串。
#（感谢 S. C. 指出这一点。）

t=${var%*}}
echo "如果 var 包含 \", 则返回空字符串..." var = $t"

t=${var#-*}
echo "var (已删除从最后一个 - 开始的所有内容) = $t"
echo

path_name=/home/bozo/ideas/thoughts.for.today
# path_name="$path_name"
echo "path_name = $path_name"
t=${path_name#*/} 去掉前缀 = $t
# 在这种特定情况下与 t=$basename 效果相同。
# t=${path_name*:}; t=${t##*/} 是一个更通用的解决方案，
# 但有时仍然失败。
# 如果 path_name 以换行符结尾，则 $path_name 将不起，
# 但上面的表达式可以工作。
#（感谢 S.C.）

t=${path_name##/*}
# 与 t=dirname $path_name 效果相同
echo "path_name, 去掉后缀 = $t"
# 这些在某些情况下会失败，例如 "../////", # "foo/", "/*"
# 删除后缀，尤其是当 basename 没有后缀但 dirname 有后缀时，也会会让问题变得复杂。
#（感谢 S.C.）
echo

t=${path_name:11}
echo "path_name, 去掉前 11 个字符 = $t"
t=${path_name:11:5}
echo "path_name, 去掉前 11 个字符后，长度为 5 = $t"
echo

t=${path_name//bozo/clown}
echo "$ 将 \"bozo\" 替换为 \"clown\" 后 = $t"
t=${path_name#*/today/}
echo "删除了 \"today\" 的 path_name = $t"
t=${path_name//o/O}
echo "所有 o 都已大写的 path_name = $t"
t=${path_name//o/(o)}
echo "删除了所有 o 的 path_name = $t"
```

### 示例 9–17. 在字符串的前缀或后缀匹配模式

```bash
exit 0
${var/##patt/replacement}
```

如果 `var` 的前缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
${var/*#patt/replacement}
```

如果 `var` 的后缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
#!/bin/bash
# 字符串前缀/后缀的模式替换。

v0=abc1234zip1234abc # 原始变量。
echo v0 = $v0 # abc1234zip1234abc
echo

# 在字符串的开头（beginning）匹配。
v1=$(v0/##ABCDEF) # abc1234zip1234abc
echo v1 = $v1 # ABCDE1234zip1234abc
||

# 在字符串的结尾（end）匹配。
v2=$(v0%#ABCDEF) # abc1234zip123abc
echo v2 = $v2 # abc1234zip1234ABCDEF
|----|

echo
echo

# 必须在字符串的开头/结尾匹配，
# 否则没有替换结果。
v3=$(v0#/12300) # 匹配，但不在开头。
echo v3 = $v3 # abc1234zip1234abc
# 无替换。
v4=$(v0%#12300) # 匹配，但不在结尾。
echo v4 = $v4 # abc1234zip1234abc
# 无替换。
```

```bash
exit 0
${!varprefix*}, ${!varprefix@}
```

匹配所有以 `varprefix` 开头的已声明变量。

```bash
xyz23=whatever
xyz24=

a=${!xyz*} # 扩展以 "xyz" 开头的声明变量名
echo "a = $a@" # a = xyz23 xyz24
a=${!xyz24} # 同上。
echo "a = $a@" # a = xyz23 xyz24
```

## 9.4. 变量类型：declare 或 typeset

`declare` 或 `typeset` 内置命令（它们是同义词）允许限制变量的属性。这是一种弱类型检查。

```bash
exit 0
${var/##patt/replacement}
```

如果 `var` 的前缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

```bash
${var/*#patt/replacement}
```

如果 `var` 的后缀匹配 `replacement`，则将 `patt` 替换为 `replacement`。

### 示例 9–17. 在字符串的前缀或后缀匹配模式

```bash
#!/bin/bash
# 字符串前缀/后缀的模式替换。

v0=abc1234zip1234abc # 原始变量。
echo v0 = $v0 # abc1234zip1234abc
echo

# 在字符串开头（beginning）匹配。
v1=$(v0/##ABCDEF) # abc1234zip1234abc
echo v1 = $v1 # ABCDE1234zip1234abc
||

# 在字符串结尾（end）匹配。
v2=$(v0%#ABCDEF) # abc1234zip123abc
echo v2 = $v2 # abc1234zip1234ABCDEF
|----|

echo
echo

# 必须在字符串的开头/结尾匹配，
# 否则没有替换结果。
v3=$(v0#/12300) # 匹配，但不在开头。
echo v3 = $v3 # abc1234zip1234abc
# 无替换。
v4=$(v0%#12300) # 匹配，但不在结尾。
echo v4 = $v4 # abc1234zip1234abc
# 无替换。
```

```bash
exit 0
${!varprefix*}, ${!varprefix@}
```

匹配所有以 `varprefix` 开头的已声明变量。

```bash
xyz23=whatever
xyz24=

a=${!xyz*} # 扩展以 "xyz" 开头的声明变量名
echo "a = $a@" # a = xyz23 xyz24
```

# 高级 Bash 脚本指南

## 9.5. 生成随机整数

```bash
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

如果你需要一个特定范围内的随机整数，请使用“取模”运算符。

它返回除法运算的余数。

```bash
RANGE=500
echo
number=$RANDOM
let "number %= $RANGE"
echo "Random number less than $RANGE  --- $number"
echo
```

如果你需要一个大于下限的随机整数，请设置一个测试来丢弃所有低于下限的数字。

```bash
FLOOR=200
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
done
echo "Random number greater than $FLOOR  --- $number"
echo
```

可以结合上述两种技术来获取两个数字之间的随机数。

```bash
number=0  # 初始化
while [ "$number" -le $FLOOR ];
do
  number=$RANDOM
  let "number %= $RANGE"  # 将数字缩小到 $RANGE 范围内。
done
echo "Random number between $FLOOR and $RANGE  --- $number"
echo
```

生成二选一，即“真”或“假”值。

```bash
BINARY=2
number=$RANDOM
T=1
let "number >= 14"  可以提供更好的随机分布
# (右) 移出除了最后一个二进制位以外的所有内容。
if [ "$number" -eq $T ];
then
```

## 9.6. $RANDOM: 生成随机整数

```bash
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

`RANDOM` 到底有多随机？测试此点的最佳方法是编写一个脚本，跟踪 `RANDOM` 生成的“随机”数的分布。让我们投掷几次 `RANDOM` 吧……

### 示例 9–22. 使用 RANDOM 掷骰子

```bash
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

```bash
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

```bash
while [ "$throw" -lt "$MAXTHROWS" ]
do
  let "diel" = RANDOM % $PIPS
  update_count $diel
  let "throw" += 1
done
```

假设 `RANDOM` 是相当随机的，得分分布应该均匀。

当 `MAXTHROWS` 为 600 时，所有结果都应该集中在 100 左右，正负 20。

请记住 `RANDOM` 是一个伪随机生成器，而且它并不是特别特别优秀。

练习（简单）：重写此脚本来抛掷 1000 次硬币。选择是“HEADS”（正面）或“TAILS”（反面）。

正如我们在上一个示例中看到的，每次调用 `RANDOM` 时都“重新种子” `RANDOM` 生成器是最好的。对 `RANDOM` 使用相同的种子会重复相同的数字序列。（这反映了 C 语言中 `random()` 函数的行为。）

### 示例 9-23. 为 RANDOM 种子

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

设置 `RANDOM` 会种子随机数生成器。

```bash
RANDOM=1
random_numbers
```

对 `RANDOM` 使用相同的种子……会复制相同的数字序列。

什么时候需要重复同一个“随机”数字序列？

```bash
RANDOM=2
random_numbers
```

再次尝试，但使用不同的种子……会产生不同的数字序列。

```bash
# RANDOM=$$ 根据脚本 ID 为 RANDOM 设置种子。
# 也可以从 'time' 为 RANDOM 设置种子。
```

# 第 10 章 循环与分支

## 高级 Bash 脚本指南

```bash
echo # 用引号括起整个“列表”将创建一个单个变量。
for planet in "Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune Pluto"
do
  echo $planet
done
exit 0
```

每个 `[list]` 元素可以包含多个参数。这在分组处理参数时非常有用。在这种情况下，请使用 `set` 命令（参见示例 11-10）来强制解析每个 `[list]` 元素，并将每个组件赋值给位置参数。

### 示例 10-2. 每个 [list] 元素中包含两个参数的 for 循环

```bash
#!/bin/bash
# 重新回顾行星。

# 将每个行星的名称与其到太阳的距离关联。
for planet in "Mercury 36" "Venus 67" "Earth 93" "Mars 142" "Jupiter 483"
do
  set --"$planet" 解析并设置位置参数。
  # "-" 可以防止在 $planet 为空或以连字符开头时出现意外情况。

  # 可能需要保存原始的位置参数，因为它们会被覆盖。
  # 这种方法的一种是使用数组
  original_params=("$@")

  echo "$1" $2,000,000 miles from the sun
  # --two 在参数 $2 后面拼接了两个零
done

# （感谢 S.C. 提供的额外说明。）
exit 0
```

变量可以为 `for` 循环提供 `[list]`。

### 示例 10-3. Fileinfo：对变量中包含的文件列表进行操作

```bash
#!/bin/bash
# fileinfo.sh

FILES="/usr/sbin/privatepw
/usr/sbin/pwck
/usr/sbin/go500gw
/usr/bin/fakefile
/sbin/mkreiserfs
  # 你感兴趣的文件列表。
  /sbin/ypbins
  # 顺便加入了一个虚拟文件 /usr/bin/fakefile。"
```

```bash
echo
for file in $FILES
do
  if [ ! -e "$file" ]; then    # 检查文件是否存在。
    echo "$file does not exist."; echo
    continue
    # 继续处理下一个。
  fi

  ls -l $file | awk '{print $9}'    file size: "$5" # 打印两个文件。
  whatis basename $file    # 文件信息。
  echo
done
```

`for` 循环中的 `[list]` 可以包含通配符（globbing），即使用通配符进行文件名扩展。

### 示例 10–4. 使用 for 循环操作文件

```bash
#!/bin/bash
# list-glob.sh: 使用“globbing”在 for 循环中生成 [list]
echo
for file *
do
  ls -l "$file" # 列出 $PWD（当前目录）中的文件。
  # 回想通配符 "*" 匹配一切
  # 但在“globbing”中，它不匹配隐藏文件（点文件）。

  # 如果模式没有匹配到文件，它将扩展为。
  # 为了防止这种情况，请设置 nullglob 选项
  # (shopt nullglob)
  # 感谢 S.C.
done
echo
for file in []*
do
  rm -f "$file" # 删除 $PWD 中以 "j" 或 "x" 开头的文件。
  echo "Removed file \$file"
done
echo
```

在 `for` 循环中省略 `[list]` 会导致循环对 `$@` 操作，即传递给脚本的命令行参数列表。示例 A–14 是此这一点特别巧妙的说明。
